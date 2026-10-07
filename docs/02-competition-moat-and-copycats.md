# AnyPresent briefing 02: Competition, the real moat, and whether people will just vibe-code it

## Short answer

The competition is weak in quality but strong in distribution, and that is the whole game. PPTControl is beatable on product today, and its September 2026 redesign shows it knows where it is weak. Yes, people will vibe-code basic clones; the hard parts and the distribution are what they will not finish. Your moat is "the one that keeps working and keeps ranking", which you build by shipping first, collecting ratings early, and owning the search terms and the content. Confidence: high.

## Competitor map, and what each one proves

| Segment | Who | What it proves for you |
|---|---|---|
| Phone presenter apps needing a desktop app | PPTControl (3.1 stars Android, 3.9 iOS, $4.99/month, $19.99/year, $49.99 lifetime, redesigned 2 September 2026 with a menu-bar Mac app and "better stability") | The category leader has a reliability problem and a subscription-first price list students resent. Both are openings. Its redesign also says the window on "we connect better" may narrow by the time you launch, so "nothing to install" plus auto-fallback, not stability alone, must be your headline. |
| Watch-based | Samsung PPT Controller (free, 4.3 stars, Samsung phones only since Android 15), WowMouse Presenter (removed 2026 after the Oura acquisition) | Galaxy Watch and Wear OS presenters are orphaned. A Wear OS mode is a specific, searchable gap, cheap for you as an Android developer. Not for launch, but soon after (doc 06). |
| Free first-party and extension remotes | Keynote Remote (Apple, free), Remote for Slides (Chrome extension, 100,000 users), Google Slides casting to Chromecast or AirPlay | Mac plus Keynote users are well served for free; your edge there is effects and working with everything else. Google Slides users are served by an extension that requires a Chrome setup and a code; your web viewer plus phone remote should be at least as easy. |
| Dead first-party | Microsoft Office Remote (retired, 2.2 million lifetime installs), Remote for PowerPoint Keynote (710,000), Clicker (290,000) | Millions of people wanted this and were abandoned. Microsoft is not coming back; its current "present from your phone" feature is for shows hosted on the phone itself behind a Microsoft 365 subscription. |
| "Nothing to install" keyboard and mouse apps | Appground Bluetooth Keyboard & Mouse (Android, 100,000 installs a month, 9.7 million lifetime, 4.3 stars, presenter mode paid), Bluetouch (iOS, 3.6 stars from ~165 ratings, reconnection complaints), btkbd (iOS, 15 ratings), BT Remote (iOS, open source, HID over GATT) | The adjacent market is 25 times larger. On iOS the incumbent is mediocre and the open-source app proves the trick is public knowledge. This is your second product (doc 06). |
| PC remotes with a desktop program | Remote Mouse (73,000 installs a month), Unified Remote (14 million lifetime, ~€85,000 revenue in 2025) | The "install a helper on the PC" model is accepted at scale. Your companion is not a barrier if it is small and trustworthy. The revenue line shows the ceiling for this family of apps. |
| Hardware | Cheap clickers (€8 to €16, ~30,000 a month on Amazon US top ten), Logitech Spotlight and Spotlight 2 (€105 to €130, ~500 a month) | Intent exists and is searched for. "Your phone is a €130 Spotlight" is a true and demonstrable claim. |
| Desktop effect tools | PowerToys and ZoomIt (free), Presentify ($14.99), PointerFocus ($12.50) | Effects alone are not a moat; everyone can draw a circle. Phone-driven effects (point with the phone, spotlight follows) are the Logitech experience, and that combination is what nobody offers for free. |
| New entrants | Copresent (July 2026, Product Hunt): browser-only Google Slides remote, attendees open a link, up to ten co-presenters | Validates the browser-first, zero-install direction and shows that new competitors appear every few months. It is Google Slides only. |

## Why PPTControl is beatable, and where the window could close

Beatable: a 3.1-star Android rating is a reliability verdict from users, subscription pricing in a few-times-a-year category is resented, and it requires its desktop app for everything. You can offer slide control in 60 seconds with nothing installed, and effects with a companion, and automatic fallback to the internet when Bluetooth misbehaves.

Window closing: their redesign claims better stability; if it is true, "we are more reliable" becomes a tie by the time you launch. What they cannot copy quickly is the no-install mode (requires the HID trick on iOS, which they do not have) and the auto-fallback ladder (architecture, not a feature). Lead with those.

## Will people immediately vibe-code alternatives?

Partly yes, and it matters less than it feels like. Split the product into what is a weekend with an LLM and what is not.

A weekend:
- An Android app that acts as a Bluetooth HID keyboard and sends arrow keys. Dozens already exist.
- A phone web page that talks to a small relay and a desktop script that presses keys.
- An Electron or Tauri overlay that draws a circle.

Not a weekend, and where most clones die:
- An iPhone app that reliably pairs as a keyboard with Windows, macOS and Chromebooks. Bluetouch's reviews are a catalogue of how hard this is, and the trick is unblessed by Apple (see platform risks below).
- Overlay effects that survive fullscreen PowerPoint and Keynote, multiple monitors, HiDPI scaling and macOS window-level rules, on two operating systems, signed and notarized so they install without warnings.
- An auto-fallback ladder that switches to the internet relay silently mid-talk.
- A relay with pairing, abuse limits and reconnection logic.
- Store compliance on four stores, localization in ten languages, and above all the slog of connection support for a year.
- Ratings, keyword rank, SEO age, university help-page listings, brand.

The LLM era cuts both ways: it lowers a cloner's cost, and it lowers yours to keep improving. In a niche this small, few people will finish all of the above, and the graveyard in the table shows how quickly entrants are abandoned. Expect two to five new clones a year; expect most to be abandoned within months. Your defence is not code secrecy. It is: launch first, be the one with 4.4 stars and 2,000 ratings, own the top three search terms in the big storefronts, have the compatibility and how-to content that ranks, and never ship a connection regression.

One honest caveat: the moat is thin in absolute terms. A better-funded team that decides this niche is worth a year could out-execute a solo founder. The niche's size is your protection; it is not worth a funded team's year.

## First-party risk

Apple already ships Keynote Remote and could add PowerPoint-agnostic Mac control to iPhone Mirroring or Continuity. Microsoft killed Office Remote and shows no sign of returning. Google serves Slides by casting. Probability any of them ships something that makes AnyPresent redundant within two years: I would say under 10%. If it happens, the effects, the web viewer and the second product are what survive. Do not plan around it; do not ignore it either.

## Platform risks you should treat as strategic, not technical

1. **The iOS keyboard mode.** Apple's developer forums contain multiple reports that CoreBluetooth refuses to publish the standard HID service for a peripheral ("The specified UUID is not allowed for this operation"), yet Bluetouch, btkbd and the open-source BT Remote ship HID-over-GATT keyboards, and your proof of concept works. Whatever the workaround is, it is not documented or endorsed. Consequences: (a) it can stop working with any iOS release; (b) App Review may reject it under the private-API or "undocumented behaviour" rules at any submission; (c) hosts are inconsistent (one forum report describes a Mac that could not see Bluetouch). Strategic response: build the product so iOS without HID is still a good product (companion, direct link, relay, web viewer); isolate the HID code; submit a minimal iOS build for review early with manual release to learn Apple's current stance; test every iOS beta from June onward. Confidence that it works at launch: medium-high (you have it working, others ship it). Confidence that it still works in three years: low.
2. **Apple guideline 2.5.9** (apps that alter the function of standard switches such as volume will be rejected) is confirmed and enforced. Forum consensus is that listening without changing the volume and explaining it in review notes sometimes passes, and sometimes does not. Keep volume buttons out of the iOS launch build; try later as an update with a clear note, accept rejection without drama.
3. **Android OEM Bluetooth stacks.** Your old app's "failed to connect on some devices" is the HID Device profile being flaky on certain phones. The relay fallback and in-app diagnostics are the mitigation; you cannot fix OEM stacks.
4. **Windows Bluetooth quirks.** Windows sometimes needs "remove device and re-pair" for BLE HID. Bake that instruction into the troubleshooting flow.

## Sources checked 7 October 2026

- PPTControl Desktop listing (redesign, menu bar, macOS 13+): https://apps.apple.com/app/pptcontrol-desktop/id1627913245
- Apple developer forum threads on iOS as a HID peripheral: https://developer.apple.com/forums/thread/733916 and https://developer.apple.com/forums/thread/725238 and https://developer.apple.com/forums/thread/695844
- Bluetouch listing: https://apps.apple.com/app/id1622635358 ; btkbd listing: https://apps.apple.com/app/id6739158273 ; BT Remote (open source, HID over GATT): https://apps.apple.com/us/app/id6778921831
- Apple guideline 2.5.9 context: https://developer.apple.com/app-store/review/guidelines/#hardware-compatibility and https://developer.apple.com/forums/thread/696271
- Microsoft Office Remote retirement notice: https://support.microsoft.com/en-gb/topic/office-remote-for-pc-7e3d9342-61c7-4bc2-8bc0-fa47542d1bce
- Copresent (browser-based Google Slides remote, July 2026): https://chatgate.ai/post/copresent
- Remote for Slides: https://chrome.google.com/webstore/detail/live-present-slides/detail/remote-for-slides/pojijacppbhikhkmegdoechbfiiibppi

## What I am not sure about

- **How the iOS HID workaround actually works** and therefore how exposed it is. You know this better than I do; judge the risk by how far it strays from documented APIs.
- **PPTControl's real install and revenue numbers** on iOS. If they are much higher than Android, the category is larger than my estimate and so is your upside.
- **Whether Appground will enter iOS.** They have the scale to do it; they have not for years, which suggests the iOS trick is the barrier.
- **Copresent's traction.** If a browser-only remote gets real adoption, that argues for shipping your web viewer and web remote sooner.
