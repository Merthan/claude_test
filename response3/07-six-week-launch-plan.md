# Six weeks to a free release, then the January push

## Short answer

Release free in the second week of December, push in late January, and spend the six weeks in between on reliability, gating, legal copy, eight-language assets and a beta with people who rehearse for a living. The plan below assumes your estimate that polish is a month of work and adds the two weeks that store reviews, hardware tests and a beta always cost. Confidence: medium; the iOS speech build is the item most likely to move a date.

## Week 1 (3 to 9 November): decisions and the tests that decide architecture

- Send the stipend emails and checks from doc 04 (incubators, EXIST, Prototype Fund, NLnet by 3 November if you chose open source).
- The three companion hardware tests from response 2: macOS vendor-collection read and the Input Monitoring question, HID output reports on both hosts and both phones, Windows focus behaviour for full-screen views. Each has a decision rule; apply it.
- Round 8: start the Android build and the identity check; the one-week rule from doc 01 applies.
- Fix `words[].e`; build the played-clip fix.
- Decide screen B with the reel as the post-take screen; decide the context question.
- Compile the Swift bridge on a Mac. If no Mac is at hand, rent one by the hour from a cloud Mac provider for a week; it is cheaper than a delay.

## Week 2 (10 to 16 November): the coach in the app

- Memory and duration gating; the increased-memory entitlement on iOS; a 4 GB iPhone and a 4 GB Android in the test set.
- Model and voice model as downloads from R2 behind the Worker (or Play's on-demand assets on Android), Wi-Fi by default, resumable, checked.
- "Only my voice is kept" default, the consent notice, the opt-in for server corrections with the provider named.
- English-only filler wording; the findings gated by reliability; thumbs on every finding.
- The decode-during-the-talk spike: a day to find out whether the streaming path matches the batch path within tolerance. If yes, build it; if not, the progress screen.
- The screen kit basics (countdown, work timer, Q&A) in the companion and the viewer.
- Polls trimmed to the response 2 set plus the pulse check.

## Week 3 (17 to 23 November): language, legal, assets

- Rehearsal memory on the phone if it is the one-to-two-day item it appears to be; otherwise the first update.
- Localization of UI and store listings in the eight coach languages; the voting page too.
- Licences screen, privacy policy, Impressum, the GDPR one-pager (now with the coach's on-device paragraph), the business waitlist page, a coach page on the website.
- Store assets: screenshots in eight languages (first screenshot: phone plus laptop with the spotlight; second: the Coach's notes screen; third: "nothing to install"; fourth: the reel; fifth: polls), a 20-second preview (gyro pointer, spotlight, the reel jumping to a moment, earbuds as a clicker).
- Export compliance answers prepared.

## Week 4 (24 to 30 November): the beta

- TestFlight external testing and Play closed testing.
- Testers: two or three Berlin Toastmasters clubs (one evening visit each, a founding-user code), r/Toastmasters and r/PublicSpeaking posts, r/powerpoint and r/macapps for the remote, friends with the phones in your test matrix. Aim for 30 to 60 testers; the Toastmasters members will rehearse ten times and tell you exactly what is wrong with the fillers count.
- Crash, memory and reconnection triage; the coach's thumbs data starts here.
- Submit the Windows companion to the Microsoft Store and notarize the Mac build.

## Week 5 (1 to 7 December): submission

- Fix what the beta broke; re-run the identity gate and the obfuscation for real on the shipping tree.
- Submit to App Review with manual release (free, Pro and Pro+ badged and unpriced; the review notes explain the audio session for media buttons and the on-device model download) and to Play.
- Website live with the viewer, the remote, the downloads and the coach page.
- Draft the Batch V application and the EXIST one-pager while waiting for review.

## Week 6 (8 to 14 December): release

- Release on both stores, free. No promotion beyond the testers and one honest post in the communities that gave testers.
- Watch reconnection rates, the coach's memory failures by device, download completion, and the thumbs.
- Record the January push material now, while the app is fresh: the reel, the AirPods clicker, the spotlight, a two-minute "rehearse a thesis defence" walkthrough.

## January

- Fix the December findings in one update (round 8 if it slipped, rehearsal memory if it slipped).
- The push in the week of 19 January (semester presentations, US spring start): Reddit, Show HN (the on-device speech pipeline is the story), Product Hunt, German teacher networks, LinkedIn for the coach, the university emails round one.
- Stipend applications in the January to February window; exmatriculation only after written confirmation.
- The standalone coach app starts in February (doc 05).

## Definition of done for the free release

- Reconnection works without a code after the first pairing on both platforms; the three backups are reachable from the pairing screen in two taps.
- The coach runs on every phone it is offered on and is hidden on the others; a 30-minute talk's report is on screen within seconds (decode during the talk) or within a known time with a progress screen.
- Fillers appear for English only, with the sentence for other languages.
- Nothing leaves the phone unless the user opted in, and the privacy page says exactly that.
- Eight languages in the UI and the listings; the licences screen complete.
- Every paid feature badged; no prices.
- Polls, screens and the gadget control work on the companion and the viewer.

## Risks that move the date

- The iOS speech build (never compiled; memory on 4 GB phones; Core ML left off).
- Round 8's Android build and identity check.
- App Review on the audio session or the downloaded model (both are fine with clear notes, but a rejection costs a week).
- Microsoft Store review time for a tray app with overlays.
- A beta that finds a reconnection problem you cannot reproduce; keep the per-OS diagnostics screen honest and ship anyway if the backups work.

## What I am not sure about

- **Six weeks is tight** if round 8 and the iOS build both fight back; the free release can slip into January without harming the push.
- **Toastmasters club visits** depend on their meeting calendars; email the clubs in week 1, not week 4.
