# AnyPresent briefing 10: Open questions, what would settle them, and the next 30 days

## Short answer

Seven unknowns decide most of the plan. Three are answered by one conversation with your university's founder service this month, two by launching and measuring for 90 days, one by submitting a minimal iOS build to App Review in November, and one by offering a business license and counting replies. The next 30 days are about those conversations and about building toward a mid-January launch, not about deciding features.

## The unknowns, and what settles each

| # | Unknown | Decides | How to settle it | Cost | By when |
|---|---|---|---|---|---|
| 1 | Does a free public launch count as "business activity" for EXIST or the Berlin stipend? | Launch sequencing; whether paid features wait | Ask the Gründungsservice; if unclear, email Projektträger Jülich and the incubator | one hour | October |
| 2 | Which EXIST rate applies (student €1,000 vs graduate €2,500)? | €18,000 and whether EXIST beats Berlin | Same conversation | included | October |
| 3 | Do Berlin incubators in your reach accept solo founders in Batch IV? | Whether the fastest money is available | Same conversation plus one email to the incubator | one hour | October |
| 4 | Does App Review accept the iOS keyboard mode? | The iOS "nothing to install" promise and the second product | Submit a minimal build with manual release | two days | November |
| 5 | What install volume does ASO plus localization produce? | The revenue scenario, the day-90 decision | Launch, wait for month three | the launch | April 2027 |
| 6 | What is paid conversion with effects behind a watermark? | Pricing and packaging | 90 days of paywall data | included | April 2027 |
| 7 | Do businesses buy a desktop license at all? | Whether to build business features | Offer it on the website with a one-page sheet, count inquiries | one day | mid-2027 |

Smaller unknowns, listed in the documents that own them: the watermark's real viral effect (doc 03), Wear OS versus Apple Watch demand (doc 06), the in-place Android update's effect on ratings (doc 04), the direct iPhone-to-Mac link's real cost (doc 06), the tax classification of app sales (doc 09).

## The next 30 days, in order

Week 1
1. Email or call the founder service of the university where you are enrolled with the ten questions in doc 07. Ask which Berlin incubator you belong to and whether Batch IV is still open.
2. Register the sole proprietorship and book one Steuerberater session (doc 09).
3. Write the day-90 criteria from doc 01 into the decision log in doc 00, and the launch date: public launch in the week of 12 January 2027 (adjust once the stipend answer is in).
4. Put up anypresent.com with an Impressum, a privacy page and a one-paragraph description. Take the social handles.

Week 2
5. If Berlin Batch IV is open to you: start the application (short business plan from these documents, the prototype you have, the consultation). If not: start the EXIST Ideenpapier with the framing in doc 07 and ask the service for a mentor professor.
6. Decide the relay message schema so that the phone app, web remote, watch (via phone), companion and web viewer are interchangeable endpoints (the one architectural decision in doc 09).
7. ASO keyword research with store autocomplete in English and German; draft title, subtitle and keyword field (doc 03 and doc 08).

Week 3
8. Build the iOS v1 path to a reviewable minimum: keyboard mode, next and previous, gyro laser, timer, the one-screen onboarding. Prepare the submission with manual release, so Apple's answer arrives in November.
9. Start the Android in-place update of the old app (target SDK, rename, old Pro detection).
10. Companion: pairing, spotlight, magnifier, watermark, auto-update; begin the Microsoft Store account and the Mac notarization setup.

Week 4
11. Recruit 20 to 30 testers (friends, one Reddit post) for TestFlight and Play closed testing in November.
12. Write the GDPR one-pager in German (doc 03) and the business license one-pager (doc 04); both double as stipend application material.
13. Screenshots and a 15-second preview video from the working build.
14. Review this plan against the stipend answers and adjust the launch date and the paid-features date.

## What "done" looks like on 7 November

- You know your stipend path and have an application in progress or a clear "no".
- The iOS build is in App Review or about to be.
- The Android update and the companion are in closed testing.
- The website exists with legal pages, and the store listings are drafted in two languages with the rest queued.
- The decision log has dates and criteria in it.

## All sources checked for these briefings (7 October 2026)

Stipends
- https://www.ptj.de/foerdermoeglichkeiten/exist/gruendungsstipendium
- https://www.foerderdatenbank.de/FDB/Content/DE/Foerderprogramm/Bund/BMWi/exist-gruendungsstipendium.html
- https://www.bundesanzeiger.de/pub/publication/wtMJomkeGn4aOsMqSOs/content/wtMJomkeGn4aOsMqSOs/BAnz%20AT%2018.04.2023%20B1.pdf
- https://exist.de/wp-content/uploads/2026/06/EXIST-Gruendungsstipendiatenvertrag.docx
- https://www.berlin.de/sen/wirtschaft/gruenden-und-foerdern/gruendungs-und-startup-foerderung/finanzielle-foerderung/zuschuesse/20260420_uebersicht_aufruf_2_berlinde_final.pdf
- https://www.berlin.de/sen/web/presse/pressemitteilungen/2026/pressemitteilung.1653813.php
- https://www.gruenderkueche.de/events/berliner-startup-stipendium-batch-iii-mit-science-startups-berlin-2026-bewerbung/
- https://www.hwr-berlin.de/presse/pressemitteilungen/pressemitteilung-detail/detail/6823-von-tech-ueber-social-startups-bis-smart-city
- https://www.foerderdatenbank.de/FDB/Content/DE/Foerderprogramm/Land/Berlin/berliner-startup-stipendium.html

Apple rules and the iOS Bluetooth situation
- https://developer.apple.com/app-store/review/guidelines/#hardware-compatibility
- https://developer.apple.com/forums/thread/696271
- https://developer.apple.com/forums/thread/733916
- https://developer.apple.com/forums/thread/725238
- https://developer.apple.com/forums/thread/695844
- https://apps.apple.com/app/id1622635358 (Bluetouch)
- https://apps.apple.com/app/id6739158273 (btkbd)
- https://apps.apple.com/us/app/id6778921831 (BT Remote, open source)

Competitors and first-party remotes
- https://apps.apple.com/app/pptcontrol-desktop/id1627913245
- https://support.microsoft.com/en-gb/topic/office-remote-for-pc-7e3d9342-61c7-4bc2-8bc0-fa47542d1bce
- https://chatgate.ai/post/copresent
- https://chrome.google.com/webstore/detail/live-present-slides/detail/remote-for-slides/pojijacppbhikhkmegdoechbfiiibppi

Everything else in these briefings comes from the README's appendix (which I did not re-verify beyond the items above) or from my own reasoning, labelled with confidence levels.
