# AnyPresent briefing 06: Features, bloat, and the roadmap

## Short answer

Bloat will not cost you downloads. It will cost you the thing you are shortest of: test and support time across six platforms. So the scoping rule is "ship what makes the first presentation succeed and the effects shine, on both phones and both desktops, by mid-January", then add surfaces (web, watches) and depth (notes, jump to slide) in monthly releases driven by what users ask for. Do not build an all-in-one presentation suite; stay the delivery layer that works with whatever slides people already have. Confidence: high.

## The constraint, stated honestly

Code is cheap for you. Each feature still adds a row to a matrix of iOS and Android, times macOS and Windows, times PowerPoint, Keynote, Google Slides and PDF, times Bluetooth stacks that misbehave. Every row generates support email about connections. A solo founder's week has room for the product, the marketing in doc 03, the stipend work in doc 07, and connection support. It does not have room for a watch app that three people use and that breaks on Wear OS 5.

## v1, public launch (target mid-January 2027)

Phone (iOS and Android):
- Next and previous, start and end show, black screen.
- Gyro laser pointer (your best demo; it goes in the first screenshot).
- Spotlight and magnifier when the companion is present, with the watermark in the free tier.
- Timer with vibration marks and rehearsal mode.
- The connection ladder: keyboard mode, companion over Bluetooth, internet relay with QR or code pairing, and the direct iPhone-to-Mac link if it really is a few days of work.
- Android only: volume buttons and screen-off mode.
- Pro unlock, 7-day pass, old Pro app grandfathering on Android (doc 04).
- Diagnostics screen, "Before you present" checklist, "Test connection".
- Localization of UI and store listings in roughly ten languages.

Desktop companion (macOS and Windows):
- Tray app, auto-start, auto-update, proximity pairing, QR and code pairing, spotlight and magnifier, watermark logic, business license entry, "Try the spotlight".
- Notarized Mac build, Microsoft Store build for Windows (doc 09).

Website:
- Landing page, companion download, Impressum and privacy page, the GDPR one-pager, the first three articles.

Not in v1, on purpose: watches, notes, jump to slide, the web viewer and web remote, transcripts, fun pointers beyond two or three, iOS volume buttons, Linux.

## v1.1 (February to March 2027)

- **Web viewer plus web remote.** The install-free path for school PCs and Chromebooks, your SEO tool page, and the hedge against the iOS platform risk. PDF rendering in the browser, effects drawn in the page, pairing code, phone app and web remote as controllers. Animations unsupported, said once.
- **Wear OS controller** (next, previous, black screen, timer, vibration). You are an Android and Wear OS developer, Samsung orphaned non-Samsung Galaxy Watch users, WowMouse is gone. Test on the emulator for current Wear OS versions; your Wear OS 2 watch is not representative of what people own.
- Two or three more effects and fun pointers, mainly for the video clips.
- Whatever the first 500 users' reviews say is missing.

## v1.2 (April to June 2027)

- **Speaker notes and jump to slide through the presentation app, not through the file.** On macOS, Keynote and PowerPoint are scriptable (current slide, notes, go to slide); on Windows, PowerPoint exposes the same through automation. This is how a desktop-app competitor does it, it is reliable, and it avoids parsing PPTX files and sending twenty "back" presses. Google Slides in a browser has no such hook, so notes there wait for the viewer. PDF viewers give page numbers. Notes go to the phone in landscape and later to the watch.
- **Apple Watch controller**, after Wear OS has shown whether anyone uses a watch at all, and once you own a watch to test on.
- **Business features if inquiries have arrived**: custom branding on the spotlight, MSI and PKG installers, the IT one-pager.
- iOS volume buttons as a separate update with a review note, prepared to be rejected.

## Later, only with evidence

- **Transcripts with slide timestamps.** Local speech recognition on the desktop makes it privacy-clean and it is a plausible business and lecture feature. Build it when a business license buyer or a university asks, not before.
- **Linux companion.** When a university IT page asks for it.
- **Co-presenting** (two phones, one deck). Copresent is doing this for Google Slides; wait and see whether anyone wants it.
- **Analytics on presentations** (time per slide). Cheap once notes and slide sync exist; a Pro+ feature if a subscription ever makes sense.

## Never

- AI feedback on presentation quality. You are right; no data, unreliable output, and it would pull the product toward a different business.
- Slide editing or any "all-in-one suite". That competes with PowerPoint, Keynote, Canva and Gamma, needs a team, and throws away your actual advantage, which is working with all of them.
- Accounts, social features, cloud storage of decks.
- Rendering PPTX with animations in the browser. You already found no renderer that is good enough; the PDF recommendation is the right answer.
- Ads.

## Platform sequencing

1. **iOS first for App Review, not for launch.** Submit a minimal build with keyboard mode in November with manual release to learn whether Apple accepts the HID approach. This single submission removes the biggest unknown in the plan.
2. **Android in parallel**, as an in-place update of the old app (doc 04). Your expertise makes it the shorter path; do not let it slip because iOS is new and interesting.
3. **Companion on both desktops at launch.** Effects on one OS only would halve the screenshots' truth.
4. **Web viewer and remote in 1.1**, Wear OS in 1.1, Apple Watch in 1.2.
5. **Both phone platforms public within the same two weeks.** A launch push works once; spend it on both.

## The second product: "nothing to install" keyboard and mouse

You listed it as a maybe. I would treat it as the most important roadmap decision after launch, decided by data at day 90.

For it: Appground does 100,000 installs a month on Android alone, so the general-purpose market is about 25 times the presenter niche. On iOS the incumbent (Bluetouch) has 3.6 stars and reconnection complaints, and the only other entrants are tiny. You already have the hard part working on iOS. It shares the HID core, the pairing flow, the diagnostics and the localization. Cross-promotion between the two apps is free distribution in both directions.

Against it: Android is a commodity there (Appground owns it); iOS carries the same platform risk as your keyboard mode, concentrated; Apple's rule 4.3 against near-duplicates means the second app must be clearly a different product (trackpad, full keyboard, media keys, text paste) and not "AnyPresent without effects".

Decision rule at day 90: if AnyPresent's organic installs are below the Base case and App Review has accepted the HID approach, start the keyboard and mouse app immediately. If AnyPresent is at or above Base, finish 1.2 first and start it in the summer. If Apple has rejected the HID approach, the second product is dead and this question answers itself.

## Timeline in one table

| Month | Milestone |
|---|---|
| October 2026 | Stipend contacts and application (doc 07). Core build. Relay designed so phone app, web remote, watch, companion and web viewer are interchangeable endpoints. |
| November | Minimal iOS build to App Review (manual release). Closed beta on both platforms. Companion builds signed and in the Microsoft Store queue. Store assets and localization. |
| December | Soft launch, free tier only if the stipend rules require it. Bug fixing. Website with first articles. |
| Mid-January 2027 | Launch push (doc 03). |
| February to March | 1.1: web viewer and remote, Wear OS, effects. Video experiment. University emails. |
| April | Day-90 review (doc 01). Second-product decision. Stipend start if EXIST is approved early; paid features on if not already. |
| April to June | 1.2: notes and jump to slide via app scripting, Apple Watch, business features on demand. |
| Second half of 2027 | Second product or depth, decided by the review. |

## What I am not sure about

- **Whether the direct iPhone-to-Mac link is really "easy"**. If it costs more than a few days, drop it from v1; Bluetooth GATT plus relay covers the same users.
- **Wear OS before Apple Watch** is a bet on your skills and the orphaned-users gap, not on evidence of demand. If US iPhone users ask for Apple Watch loudly after launch, swap the order.
- **The web viewer's priority** rests on my reading that school PCs and Chromebooks are a large share of student presentations and that the platform hedge matters. If your first 500 users all present from their own laptops, it can slip to 1.2.
- **Notes via app scripting** need an accessibility or automation permission on macOS, which some users refuse. It is still better than file parsing.
