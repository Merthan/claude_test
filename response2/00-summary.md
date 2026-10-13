# Response 2 (13 October 2026): summary and direct answers

*Read in full: `prompt_13_10.txt` and `COMPANION-CONTEXT_2.md`. Checked online: Cloudflare's Durable Object WebSocket billing, Apple's and Google's on-device speech APIs, the current reading of Apple's rules 3.1.1 and 3.1.3(b), the incumbents' free poll tiers, the macOS Input Monitoring question for HID vendor reads, and Apple offer codes for discounted one-time purchases. Links are in the files that use them. No existing file was edited; everything new is in `response2/`.*

## The five things that matter most in this round

1. **Transcribe on the phone, not on the companion.** The phone is in the presenter's hand (the best microphone position), it already knows every slide change (it sends them), it works in Bluetooth-clicker mode and in rehearsal with no companion at all, and both platforms now offer on-device long-form recognition without bundling a model (iOS 26 SpeechAnalyzer, Android 12+ on-device recognizer with Android 13 segmented sessions). This removes a whole subsystem from the companion and keeps the privacy story intact. File 04.
2. **The companion is an upgrade of the Bluetooth connection, not a second connection.** Your companion reads the vendor collection of the same HID pairing the phone already made. So the user pairs once as a Bluetooth clicker, and installing the companion later adds effects, screens and polls to that same pairing with nothing to re-pair. That fact is the backbone of the connection UX you were missing: a "connection ladder" card that always shows what you have and the one step that gets you more. File 02.
3. **Three hardware tests are architecture decisions, not bug hunts.** Whether macOS demands the Input Monitoring permission to read the vendor collection (if yes, the Mac data channel moves to a GATT service or the direct link), whether HID output reports reach the phone on Windows and macOS (if not, two-way data needs GATT), and whether Windows focus stealing for the black screen works (plan B: the phone owns screen state, so focus games are not needed for the phone path). Run these three first. File 01.
4. **Polls: yes, in v1, limited, account-free.** Your position is "the fastest way to ask the room a question during any presentation", not "a Mentimeter replacement". That is real, because every incumbent needs a presenter account and preparation, and their free tiers are stingy (Mentimeter: 50 participants a month across the whole account). Add a continuous "pulse" check and a correct-answer flag, defer free text, and stop there. File 03.
5. **Three consumer products, not a ladder of tiers.** Pro once (bounded features), Pro+ as a subscription with a lifetime option (unbounded, ongoing-value features such as transcripts, slide info, large audiences), and cosmetics as separate purchases that even Pro users pay for. Business by license key on the companion. Apple's rule 3.1.1 is not triggered by the companion deciding not to draw its own credit. File 06.

## Direct answers, in the order of your notes

**Connection flow.** You are right that users must see what is still missing to reach the best mode. The answer is not another menu but a persistent connection card with a three-step ladder (clicker, full with companion, direct on Mac) and the two backups (by code, browser) labelled as backups with "slight delay" and a "Bluetooth is better" line. The companion needs no new pairing, which is the sentence to put under the card until the companion is seen. Troubleshooting on the pairing screen routes a failed Bluetooth pairing to the two backups inline. File 02.

**Start at login and always ready.** Both under an Advanced submenu, both with a confirmation sheet when switched off, and a truthful footprint number measured on hardware rather than "0.01%". File 02.

**Stable identity.** Confirmed by the design: the pairing secret is the identity, daily rooms are derived from it, and reconnection needs no new code. One fix: derive the day from server time in `welcome`, not the local clock. File 01.

**Presenter controls.** Your three-preset setup screen with a thumb illustration is the right call. Timer at the bottom edge, centred in landscape. No gestures, agreed. File 02.

**Watches.** W1 only, agreed. W2 would push people toward the relay you want to keep as a backup.

**Website viewer.** "Import locally" wording, PPTX accepted with a warning and the export guides, no thumbnails, keyboard shortcuts listed at the bottom. Agreed on all. File 02.

**Collecting data.** You do not need tracking. You get installs, crashes, countries, devices and conversion from the two store consoles for free, your own server already counts sessions and voters without any personal data, TestFlight and Play testing give you free-text feedback, and a voluntary form behind "feedback after five talks, 50% off Pro" gives you the free text that matters. File 07.

**Hotkey effects.** Agreed, not now, for your reason.

**Slide thumbnails and notes.** Agreed on thumbnails: never over Bluetooth. Slide number, upcoming title and notes text are small and are the Phase 2 reason professionals pay. File 05.

**Rehearsal analytics.** Yes, in v1, as a local "presentation log" with timings only. File 04.

**On-device transcription.** Yes, on the phone, Phase 1.x once the core is stable, with the platform specifics and caveats in file 04. Live captions: skipped, agreed.

**Room mode.** Later, agreed, with the control-expiry design you asked about noted in file 07 so it is not forgotten. Accessibility: six cheap rules on the voting page now, a VPAT document only when an institution asks.

**Event mode.** Agreed, zero focus unless someone asks.

**Polls.** Market position, what to add, what to defer, metering: file 03. Slide following: never, agreed. Free-text answers: Phase 2 with a filter and a host-side hide.

**Keyboard and mouse sibling.** Bluetooth-only at launch; relay as a Pro+ feature with a rate cap if anyone asks. The arithmetic is in file 06.

**Effects free with credit.** Clarified in file 06: the standard effects are free with the credit, Pro removes the credit, and additional cosmetic effects are separate purchases for everyone, Pro included.

**Taking things away later.** Fine for new users; never for a user who already had it without a perk. Badge Pro features from day one so the later price is no surprise. File 06.

**Pro tiers for the €8 and the €200 user.** Pro once, Pro+ subscription or lifetime, cosmetics, business. File 06.

**Apple 3.1.1.** The rule governs the iOS app's own unlock mechanisms. The companion removing its own credit is not one. File 06 has the rules that keep you on the right side of it.

**Deeper PowerPoint and Keynote integration.** Worth it in Phase 2, text-only, capability-gated so nothing is shown where it is not available. File 05.

## Verdict on the companion and the server

The architecture is sound and further along than I expected: one Worker on your domain, a Durable Object per talk with hibernating WebSockets, an end-to-end encrypted relay with short authentication strings, daily room rotation, acknowledged and de-duplicated commands, capability negotiation, and a QR pairing link that doubles as a universal link. The billing assumptions are correct per Cloudflare's own pricing page. The fragile parts are exactly the ones the other chat flagged, plus one it did not: macOS may demand Input Monitoring to read the vendor collection, which would contradict your no-scary-permissions promise on the Mac. File 01 has verdicts on every decision and the three decision rules.

## The revised phase plan, given your preferences

- **Phase 1 (before the push):** remote on all six surfaces, effects and screens, polls (basic kinds, pulse check, correct-answer flag), presentation log with timings, countdown screen, group mode if the multi-pairing path makes it cheap, Pro badged and unpriced.
- **Phase 2 (after the push, during the funded year):** phone-side transcription and the log with text, PowerPoint and Keynote slide info, prepared poll sets and quiz mode with generated nicknames, free-text answers with a filter, Pro+ priced, business license.
- **Phase 3:** room mode for institutions with session-scoped control, AI overviews of your own talks (on-device where possible), institution licensing.

## Files

- `01-companion-and-server-review.md`: verdicts on D1 to D19, the three hardware tests as decision rules, changes before release, answers to the open-decisions list.
- `02-connection-ux-ladder.md`: the ladder card, home screen and copy, troubleshooting routing, settings UX, the Mac direct link, controls and viewer notes.
- `03-polls-and-audience.md`: market position with sources, what to add and defer, design rules, metering, the stop list.
- `04-transcription-and-intelligence.md`: phone-side transcription, platform specifics, the log, AI overviews on-device, how influential it really is.
- `05-powerpoint-keynote-integration.md`: the integration judged, what to show, how to avoid confusion, cost and transport.
- `06-monetization-tiers-and-apple-rules.md`: the catalogue, badging, feedback for discount, Apple's rules explained, the sibling app's relay cost.
- `07-data-feedback-and-other-features.md`: the data question answered, other features with verdicts, room-mode control design for later.
