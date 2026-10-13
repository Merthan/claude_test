# Companion and server review

*Based on `COMPANION-CONTEXT_2.md` alone, as you asked. I judge the top-level decisions, not the code. Where I say "verified", I checked a public source and link it at the end.*

## Overall verdict

Good architecture, and more complete than a first companion usually is. The decisions that matter were made correctly: one Worker on your own domain, a Durable Object per talk with hibernating WebSockets, votes over the socket rather than HTTP, an end-to-end encrypted relay with short authentication strings and pairing keys in the OS keystore, daily room rotation, one command table for Bluetooth and internet with acknowledgements and de-duplication, capability negotiation in READY, "always ready" idle sockets, and a pairing QR that is also a universal link. The billing model the other chat assumed is correct per Cloudflare's pricing page. The fragile parts are the ones it flagged (focus stealing, the HID reads themselves) plus one it did not raise: the macOS permission that reading the vendor collection may trigger. Three hardware tests therefore decide architecture, and they should run before anything else.

## The three hardware tests that are decisions, not bug hunts

### Test 1: does macOS demand Input Monitoring to read the vendor collection?

Why it matters: on macOS, opening a HID device the system understands as a keyboard or mouse requires the Input Monitoring permission, and the prompt says the app wants to receive keystrokes from any application. That is the scariest prompt macOS has, and it contradicts the companion's no-scary-permissions promise. Your phone presents itself as a keyboard and mouse with an extra vendor collection. Whether macOS treats the vendor collection as a separate, permission-free device or as part of the keyboard is exactly what nobody online can confirm: an Apple engineer on the forums "suspects" a vendor-specific device type avoids the requirement but is not certain, and SDL's hidapi patch shows the only way to know is to try opening the device and watch for the not-permitted error.

Decision rule:
- If the vendor collection opens without a prompt on macOS 14 and 15 (and 26): keep HID as the Bluetooth data channel on both platforms. Simplest outcome.
- If macOS prompts: do not ship that prompt. Move the Mac data channel to a custom GATT service on the same Bluetooth connection (the phone adds a service next to its HID service; the companion talks to it through CoreBluetooth, which asks only the ordinary Bluetooth permission), or to the direct link over the local network. Keyboard and mouse input still flow through HID with no companion involvement, so the clicker path is unaffected either way.
- Windows: vendor collections of a Bluetooth keyboard are openable by ordinary processes and this is the standard way configuration tools talk to keyboards. Expect it to work; confirm.

### Test 2: do HID output reports reach the phone?

Why it matters: everything two-way over Bluetooth (HELLO, STATE, SCREEN_STATE, later slide info and notes text) depends on the host writing output reports to the phone. The context says HELLO is sent and SCREEN_STATE over HID waits on this test. iOS's peripheral workaround may or may not deliver output reports to the app; Android's HID device API does.

Decision rule:
- Works on both phones and both hosts: HID stays the only Bluetooth channel. No GATT.
- Fails on iOS: add the GATT service for the iOS-to-companion data direction (the same service Test 1 might require), keep HID for input. One extra transport, but the session layer is already transport-independent.
- Fails only on one host OS: route around it with the relay only for that combination and say so in the compatibility page. Do not build a third transport for one combination.

### Test 3: does focus stealing work for the full-screen views on Windows?

Why it matters: D4's design (AttachThreadInput plus SetForegroundWindow) is the known hack, and Windows' foreground-lock rules sometimes defeat it. If it fails, a "next" from the phone during a black screen advances an invisible slide.

My recommendation regardless of the result: let the phone own screen state. The phone opened the black screen, so it knows it is open (and `screen.state` tells it when the laptop closed it). A tap on "next" while a screen is open sends only "close screen" over the vendor channel, and the next tap sends the key. That is the same "first key closes, second moves" behaviour you designed, with no focus games on the phone path. Focus stealing then only serves a user pressing Esc at the laptop, which can be best-effort; if it proves flaky, a low-level keyboard hook (an ordinary process may install one) that swallows Esc and the slide keys while a screen is open is the robust plan B on Windows. On macOS the non-activating key panel is the right tool and usually works.

## Decision-by-decision verdicts

| Decision | Verdict | Notes |
|---|---|---|
| D1 one Worker on anypresent.com, workers.dev fallback | Keep | Corporate and school filters blocking workers.dev is a real thing; the fallback is cheap insurance |
| D2 one session per talk, one Durable Object per talk, votes over WebSocket, vote-once per browser id, results hidden until reveal | Keep | Per-IP voting would break on venue NAT, as the other chat said. Browser-id voting is bypassable in a private window and that is fine for classroom polls; Mentimeter has the same limitation |
| D3 companion renders the big screen itself with tiny-skia, icon-based | Keep for v1 | The cost is no colour emoji on Windows; icons are fine. Design the big screen for a 1024 by 768 projector at the back of a room: huge type, high contrast, nothing that depends on colour alone. Test on an old projector, not a 4K monitor |
| D4 full-screen views steal keyboard focus | Change the model | Phone owns screen state (above). Keep focus stealing as best-effort for laptop-side Esc; keyboard hook as plan B |
| D5 blur: static snapshot on Windows, live effect view on macOS | Keep | Snapshot the presentation monitor, not the primary, when they differ |
| D6 HID message numbers 0x06, 0x07 taken as next free | Keep, add a registry | Put a table in PROTOCOL.md reserving ranges: phone-to-host messages in one range, host-to-phone (0x80 and up, as SCREEN_STATE already suggests) in another, and a block for slide info and notes so Phase 2 does not collide |
| D7 pairing QR is an https link with secrets in the fragment | Keep | Right call: a camera scan opens a real page, the app claims the link, the fragment never reaches the server. Host it on the app origin (D17) |
| D8 QR pairing shows no SAS digits | Keep for v1 | The phone-name confirmation on the PC stops a hijack unless the attacker names a phone like yours, and the QR is short-lived. Two rules make it adequate: the pairing window is never full-screen and always on the display with the mouse (done), and the QR is single-use with a short expiry. Room mode on shared PCs will need the digits; design that then |
| D9 laser keep-alive, hide after 3 s of silence | Keep | A frozen dot on the slides after a phone dies is the failure mode people remember. The cost is nothing |
| D10 one COMMAND table for Bluetooth and internet, ACK, dedup | Keep | Exactly right; new HID messages ride the internet for free |
| D11 capabilities in READY decide what phones show | Keep, extend in Phase 2 | Add a capability for slide info when the PowerPoint and Keynote integration exists, and send the bounds of the display that hosts the full-screen show when known, not just the primary display |
| D12 always ready, daily rooms, midnight overlap, reconnect rules | Keep, one fix | Derive the day from the server time in `welcome`, not from the local clock, or a PC with a wrong clock pairs into the wrong day silently. Default on; toggle under Advanced with an explanation (file 02) |
| D13 adaptive buffer, 20 messages a second times 3 positions | Keep | Try 15 times 4 for battery once on hardware; let the server tune the rate as designed |
| D14 pairing storage in DPAPI, Keychain, 0600 file | Keep, rename now | Registry path, Keychain service and bundle identifiers must say AnyPresent before any build leaves your machine; migrating stored pairings later is miserable for no gain |
| D15 Accessibility permission requested lazily on macOS for internet key injection | Accept | There is no permission-free way to press keys over the internet on macOS, and AppleScript into PowerPoint or Keynote only swaps one prompt for a per-app Automation prompt. Lazy is right: Bluetooth users never see it |
| D16 removed the earlier unencrypted Wi-Fi fallback | Right | And the lesson (never ship without a fallback) is the right lesson |
| D17 web viewer takes the companion role, web remote the controller role, separate origin app.anypresent.com, keys in IndexedDB | Keep, choose the separate origin | Isolating the remote's keys from the public voting pages' origin is cheap hygiene. Safari's seven-day eviction only means a web-remote guest re-pairs after a week, which is fine for a guest path |
| D18 GATT, Apple peer-to-peer, pairing methods 03 and 04 not built | Decide after Tests 1 and 2 | Build GATT only if a test demands it. Build the Mac direct link in Phase 1.5 regardless: on a Mac it can replace pairing entirely (file 02) |
| D19 billing assumptions | Verified correct | Incoming messages at 20 to 1, outgoing free, incoming protocol pings free, auto-responses not charged, no duration billing while hibernatable. Your idle sockets cost nothing |

## Changes I would make before release

1. **Rename everything to AnyPresent now** (registry key, Keychain service, bundle id, menu text, the "Pointer Companion" strings). Stored pairings and settings live under those names.
2. **Phone owns screen state** (Test 3). It also gives you the black-screen behaviour over the internet for free, since the companion already reports `screen.state`.
3. **Server time for daily rooms** (D12).
4. **Call them polls, not quizzes,** in user-facing text. A quiz implies right answers; most of what lecturers do is ask opinions. "Quiz mode" becomes the name of the correct-answer feature later.
5. **The voting page gets the six accessibility basics** (file 07) before the first audience sees it. It is the one surface strangers with disabilities will use, and it is cheap now and expensive later.
6. **Pairing window rules** from D8 written down as rules, not as current behaviour.
7. **A HID message registry** (D6).
8. **Document the always-ready socket in the privacy sheet** in one honest sentence: the companion keeps one idle encrypted connection per paired phone so the phone can reach it; nothing flows until a phone connects.

## Answers to the open-decisions list

1. Brand and app names: AnyPresent everywhere, now.
2. Connection UX: the ladder card in file 02, which is Concept C's auto-detect plus an explicit, persistent status rather than a one-time menu.
3. Web origin: app.anypresent.com.
4. Pointer rate: ship 20 times 3, try 15 times 4 on hardware for battery, keep it server-tunable.
5. Windows code signing: Microsoft Store for the signed package; direct download as the secondary route.
6. Business model: the companion is free, always. It is the distribution vehicle and the thing that draws the credit. Business pays through a license key entered in the companion (file 06).
7. HID numbers: registry as above.
8. Ping billing: verified free; nothing to check on the dashboard beyond a sanity look after the first week.
9. SAS in the QR flow: not for v1; required for room mode later.
10. Accessibility on macOS: accept, lazily.

## What I am not sure about

- **Test 1's outcome.** I would put it at even odds that macOS prompts. The decision rule covers both outcomes, which is why it is the first thing to run.
- **Whether the keyboard-hook plan B interacts badly with PowerPoint's own key handling** on some versions. It is the standard technique and usually fine; test with PowerPoint, Keynote-via-Parallels is irrelevant, and a PDF viewer.
- **The big screen's legibility** on low-resolution projectors; the previews were rendered on a desktop. One evening with a cheap projector settles it.

## Sources checked

- Cloudflare Durable Objects pricing (WebSocket 20:1 ratio, outgoing and protocol pings free, auto-responses not charged, hibernation duration): https://developers.cloudflare.com/durable-objects/platform/pricing and https://developers.cloudflare.com/durable-objects/api/state/
- macOS Input Monitoring and HID opens (SDL's hidapi change, Apple forum threads with DTS answers): https://discourse.libsdl.org/t/sdl-dont-enumerate-hid-devices-on-macos-if-we-dont-have-input-monitoring-permissions/38822 and https://developer.apple.com/forums/thread/724608 and https://developer.apple.com/forums/thread/804793
