# Companion context for Fable

As of 13 Oct 2026. From the chat that built the desktop companion and the server.

This file tells you what exists, which big decisions were made and why, where I departed from the specs I was given, and what is still open. Items marked ⚠ are the ones I am least sure about. Please double-check those first.

---

## 0. Status at a glance

**Deliverable:** `pointer-companion.zip`. It contains:
- a Rust tray app (Windows and macOS; Linux has console modes only)
- a Cloudflare Worker in `server/` (quiz sessions plus the internet relay, in one Worker)

**What has been verified:**
- 57 Rust unit tests pass.
- Every relay test vector in `internet-backup-implementation.md` §11 matches in Rust and in a separate Node implementation (`tools/fake-phone.mjs`).
- The server passes 31 quiz end-to-end checks and 9 relay smoke checks.
- A 20-check end-to-end run passes: the real companion binary, a local relay (wrangler dev), and the Node fake phone. It covers:
  - code pairing with matching SAS
  - commands with ACK
  - pointer playback
  - black screen and back
  - a duplicate command running once
  - BYE
  - QR pairing
  - unpairing from the phone side
  - a SAS mismatch storing nothing
  - concurrent pairings surviving
  - file permissions
- The live quiz client was tested against the local server.
- Clippy is clean for Linux, Windows (`-Zbuild-std` cross-check) and macOS (type-check via a fake-cc harness).
- The release binary is about 1.55 MB.

**⚠ Nothing has run on real Windows or Mac hardware yet.** Everything platform-specific is compiled and type-checked but not executed:
- focus stealing
- the GDI and AppKit rendering
- SendInput and CGEventPost
- DPAPI and the Keychain
- the blur screen
- the HID reads themselves

NEXT_STEPS.md §1 is the hardware checklist.

---

## 1. What was built

### 1.1 Bluetooth HID companion (the original v1 spec)
- **Device:** reads vendor collection `0xFFA7` / usage `0x5052`, report ID 3, via hidapi. Sends HELLO and parses STATE and DEVICE_INFO.
- **Effects:** drawn in a click-through overlay on the presentation monitor. The phone chooses one with EFFECT `0x04`.
  - spotlight
  - magnifier (in 4 edge styles)
  - spotlight + magnifier
  - magnifier + dim
  - red, green or blue laser dot
  - blur outside (experimental)
- **App behaviour:** tray icon, start at login, no admin rights.

### 1.2 HID additions (protocol minor 2, HELLO caps `0b0001_1111`)
- **`0x06` QUIZ_LINK:** the session code and host token, packed into 11 bytes (85 bits). An all-zero payload means "end the session". Test vector: K7Q4MZ + ABCDEFGHJKM → `F3 5C 42 BF 5A AC B9 07 A3 9C 14`.
- **`0x07` SCREEN:** 0 = slides, 1 = black, 2 = white, 3 = blur.
- **Caps:** bit 3 = quiz, bit 4 = screen. Phones should hide these features unless the bit is set.

### 1.3 Quizzes without text
- **Server:** a `SessionRoom` Durable Object per talk, with a SQLite vote table.
  - Live counts are coalesced to at most 4 updates per second.
  - Rate limits apply, sessions are cleaned up by TTL, and no personal data is kept.
- **Pages:**
  - Voting page at `anypresent.com/<CODE>` (English / German, light / dark).
  - `host.html`: a presenter test console with bot voters.
  - `icons.json`: the icon set shared with the companion.
- **Companion big screen** (software-rendered):
  - join screen (QR + code + live counter)
  - voting with results hidden and a "who voted" ring
  - live bars, closed, final reveal with a winner crown
- **Quiz kinds:** yes / no, single choice, multi-select, rating, reactions.
- **Looks:** 3 chart styles and 4 themes.
- **How the companion joins:** from a copied host link or from QUIZ_LINK over Bluetooth.

### 1.4 Screens and Esc
- Black, white and blur screens.
- Esc or any slide key closes every full-screen view. The views take keyboard focus so Esc doesn't end the PowerPoint or Keynote show.

### 1.5 Testing menu
- Effect preview and pickers.
- **Mouse connection simulator:**
  - phone side: rate, positions per message, tremor filter, dead-band
  - network: latency 0–500 ms, jitter and Wi‑Fi stalls
  - playback: raw, buffer, adaptive, spline, predict
  - smoothing
  - stats panel: delay, wobble, frozen frames, requests, free / paid hours
  - hold Ctrl to compare, automatic A/B, "Analyze last 60 s" (replays your own movement through every rate)
  - the same tables from the command line with `--sim-report`
- Quiz previews with a simulated audience, and the screens.

### 1.6 Internet backup client (`src/relay/`)
Implements `internet-backup-implementation.md` from the other chat:
- frames, keys, Sealer / Opener with strict counters
- pairing by code (+ SAS) and by QR
- sessions that are always ready
- pointer playback, commands with dedup, CHUNK, BYE, unpair in both directions
- pairing keys stored with the OS's secure storage

The relay Worker (`relay-worker.ts`) is merged **unchanged** as `server/src/relay.ts` in the same Worker as the quizzes.

### 1.7 Docs and tools

| File | Contents |
|---|---|
| DECISIONS.md (A–F) | Decision log |
| PROTOCOL.md (A, B, C) | Part C fixes the points left open by the specs |
| PHONE_APP_SPEC.md | What the phone app must do; §3 is the full internet-backup spec |
| WEB.md | Website viewer and web remote |
| NEXT_STEPS.md | Ordered to-do list |
| TESTING.md | How to test |
| QUIZZES.md | Quiz details |
| CHANGES.md | Changelog |
| server/README.md, server/INTEGRATION.md | Server overview and deployment |

Tools: `tools/fake-phone.mjs` (a stand-in phone), VS Code tasks, and `docs/previews/` (PNG renders of every screen).

---

## 2. Big decisions and why (please double-check)

### D1. One Worker on anypresent.com for quizzes and the relay
**Decision:** quizzes and the relay share one Worker on `anypresent.com`. workers.dev is kept as a fallback: the `FALLBACK_SERVER` slot in `src/net.rs` (currently `None`), and the `ANYPRESENT_URL` environment variable overrides it.

**Why:**
- There is one URL to configure.
- Short QR codes on a domain the audience trusts.
- Some corporate and school filters block `*.workers.dev`.
- The free and paid quotas are per account anyway, so splitting into two Workers saves nothing.

**Note:** this differs from the other chat's context file, which assumed no domain.

### D2. Quiz = one session per talk, not per question
**Decision:**
- The audience scans one QR code once, at the start.
- Each talk gets one Durable Object, placed near the room.
- Votes go over a WebSocket (1/20 of a request each) instead of a POST (about 2 requests each).
- "Vote once" is enforced per browser random id, not per IP, because venues share one NAT.
- Results stay hidden until the presenter reveals them.

**Alternatives rejected:**
- A session per question: audiences would rescan constantly.
- Per-IP voting: it breaks on conference Wi‑Fi.

### D3. The companion renders the quiz big screen itself (tiny-skia), not a browser window
**Why:**
- It must sit above a full-screen slide show and take the keyboard.
- No web engine to bundle.
- The same pixels on Windows and Mac.
- Previews can be rendered on Linux for review.

**Cost:**
- About 1,500 lines of Rust.
- Text is drawn through GDI on Windows, so there is no colour emoji there. That is why the quizzes are icon-based.

**Alternative:** a WebView. It is easier to style, but focus and topmost behaviour above PowerPoint and Keynote is harder, and it adds a runtime.

### D4. ⚠ Full-screen views steal keyboard focus
**Decision:** full-screen views take the keyboard so that Esc closes our screen instead of ending the show.
- Windows: AttachThreadInput + SetForegroundWindow.
- macOS: a non-activating key panel.
- On close, focus returns to the slide show.
- The first slide key closes the screen; the next one moves the slide.

**Unverified on hardware.** This is the most fragile part of the app.

### D5. Blur screen
- **Windows:** a static blurred snapshot taken once (BitBlt). No permission is needed, but it does not update live.
- **macOS:** a live NSVisualEffectView. This avoids the Screen Recording permission.

### D6. ⚠ HID message numbers `0x06` / `0x07`
These were simply the next free numbers. Please check them against any planned HID messages (pairing over HID, notes, etc.) before the firmware ships.

### D7. Pairing QR = an https link with the secrets in the fragment
**Decision:** the pairing QR is `https://anypresent.com/pair#v=1&r=<room>&s=<secret>`. The spec said `<scheme>://pair?…`.

**Why:**
- A plain camera scan opens a real page (`public/pair.html` now, the web remote later).
- The native app can claim the link as a universal link / app link.
- The fragment is never sent to a server.

**Notes:**
- Phones should accept both forms.
- `PAIR_LINK_BASE` in `src/net.rs` can switch the host to `app.anypresent.com` later.

### D8. ⚠ QR pairing shows no SAS digits (as the spec says)
The confirmation is "Allow *Anna's iPhone* to control this computer?".

**Risk:** if the pairing screen is mirrored to a projector, someone in the audience could scan the QR first.

**Mitigations in place:**
- The pairing screen opens on the monitor with the mouse.
- The phone's name is shown in the prompt.

**Option:** show the SAS in the QR flow too. It costs one extra look at the phone.

### D9. Laser keep-alive (an extension of the spec)
**Decision:**
- While the laser is visible, phones repeat POINTER at least every 1 s even when still.
- The companion hides the laser after 3 s of silence. Internally it is a synthetic STATE with a 1.2 s heartbeat.

**Why:** otherwise a phone that dies or loses signal leaves a frozen laser dot on the slides.

**Cost:** about 180 extra requests per hour of holding the pointer still.

### D10. One COMMAND table for Bluetooth and the internet
- **Commands 1–8:** the HID INPUT_ACTION codes (arg = extra presses).
- **`0x01TT`:** "HID message TT with this payload". `0x0104` = EFFECT, `0x0106` = QUIZ_LINK, `0x0107` = SCREEN.
- **Delivery:** every COMMAND is ACKed. Duplicates are dropped by remembering 64 command ids per pairing for 2 minutes.

**Why:** the phone has one code path, and new HID messages work over the internet automatically.

### D11. Capabilities in READY decide what phones show
- **Companion caps:** `pointer.v1`, `command.v1`, `chunk.v1`, `effect.v1`, `quiz.v1`, `screen.v1`.
- **Screen state:** if a phone lists `screen.state.v1`, the companion sends APP `{"t":"screen.state","mode":0..3}` whenever a screen opens or closes here.
- **READY also carries:**
  - `platform`
  - `display`: the primary display, which is only approximate when the projector is a second monitor
- **Web clients:** use `platform: "web"`. The website viewer may send `slide.state`.

### D12. Always ready
**Decision:** while the app runs, it keeps one socket per pairing open.
- **Midnight:** from 23:50 to 00:10 UTC, both days' rooms are open. A live session is never cut at midnight.
- **Keep-alive:** protocol pings every 30 s (free); the connection counts as dead after 80 s.
- **Reconnects:** immediately after sleep (detected by a wall-clock jump), otherwise with 1–30 s backoff.
- **Another copy holds the room** (close code 4001): wait 300 s instead of fighting.
- **Locked screen:** no pause, because idle sockets cost nothing.

**Toggle:** Internet backup ▸ Always ready while running.

### D13. Adaptive playback buffer and pointer rate
- **Buffer:** `interval + 2.5 × jitter`, clamped to [33 ms, max(100 ms, 1.5 × interval + 20 ms)]. This extends the spec's formula so it still works at low message rates.
- **Simulator recommendation:** 20 messages/s × 3 positions per message. That gives about 104 ms of visible delay at 50 ms network latency and about 3,600 requests per hour of moving. Worth trying: 15 × 4.
- **Where the rate lives:** `POINTER_HZ` is set on the server and announced in `welcome`. Keep `MAX_MSG_PER_SEC` ≥ rate + 10.

### D14. Pairing storage

| OS | Where |
|---|---|
| Windows | DPAPI-encrypted, under `HKCU\Software\PointerCompanion\Pairings` |
| macOS | Keychain: service "Pointer Companion", account "internet-backup" |
| Linux | `~/.config/pointer-companion/pairings.json`, mode 0600 |

Every change re-reads the store before saving (`Store::update`). This fixed a real bug found in the end-to-end run: a pairing made by `--pair` while the app was running got overwritten.

**⚠ macOS:** the Keychain prompts again after every ad-hoc-signed rebuild. Proper signing fixes this.

### D15. ⚠ macOS Accessibility permission (contradicts the original v1 "no input injection" goal)
**Decision:** permission is requested lazily, only when an internet phone with `command.v1` connects.

**Why:** changing slides over the internet requires pressing keys. Bluetooth needs no permission, because the mouse itself is the HID keyboard.

**Please confirm** you accept this departure from the original spec.

### D16. Removed my earlier Wi‑Fi fallback
My first Wi‑Fi fallback (a Rust relay and an unencrypted client) was deleted in favour of the encrypted Cloudflare relay spec from the other chat.

**Lesson:** for one update the companion had no internet fallback at all. That was a mistake. The spec'd client is now built.

### D17. Web apps (WEB.md)
- The **website viewer** takes the companion role; the **web remote** takes the controller role. Both use the same relay protocol.
- **Origin:** recommended to be separate, `app.anypresent.com`, so pairing keys are isolated from the public voting pages.
- **Browsers:** they cannot send protocol pings, so they use a text `ping` (the Worker's auto-response).
- **Libraries:** @noble/curves and @noble/ciphers for crypto; keys kept in IndexedDB.
- **iOS:** Safari evicts storage after 7 days without a visit; Add to Home Screen avoids that.
- **The server needs no change** for either web app.

### D18. Not built (deliberately)
- **GATT, Apple peer-to-peer, pairing methods 03 / 04:** `session.rs` is transport-independent, ready for them.
- **HTTP proxy support:** one place to add it in `net.rs`.
- **SCREEN_STATE over HID (`0x82`):** waits until HID output reports are tested on hardware.

### D19. ⚠ Billing assumption
**Assumed:**
- Outgoing WebSocket messages and protocol pings are free.
- An incoming message costs 1/20 of a request.
- The `setWebSocketAutoResponse` text ping is free.

**Conflict:** the other chat said the auto-response is "probably 1/20". Check it on the Cloudflare dashboard after a day of idle connections.

---

## 3. Open decisions for you

1. **Brand and app names.** Rename before release: the registry key, the Keychain service, the bundle id, and the menu texts.
2. **Connection UX:** concept A, B or C, as described in DECISIONS.md.
3. **Web origin:** `app.anypresent.com` or same-origin.
4. **Final pointer rate** (D13).
5. **Windows code-signing route.**
6. **Business model:** free vs. paid companion.
7. **HID number collisions** (D6).
8. **The ping billing check** (D19).
9. **SAS in the QR flow** (D8).
10. **Accept Accessibility on macOS** (D15).

## 4. Where to look
- **Decisions in depth:** DECISIONS.md, sections A–F.
- **Wire details and fixed open points:** PROTOCOL.md, part C.
- **What the phone must do:** PHONE_APP_SPEC.md §3.
- **Web apps:** WEB.md.
- **Deploying the server:** server/INTEGRATION.md.
- **What to do next:** NEXT_STEPS.md. Start with §1, the hardware tests.
- **Code entry points:**
  - `src/relay/mod.rs` (internet backup)
  - `src/hub.rs` (phone table)
  - `src/show.rs` (full-screen views)
  - `src/win/mod.rs`, `src/mac/mod.rs` (platform integration)
  - `server/src/index.ts` (routes)
