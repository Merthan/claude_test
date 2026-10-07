# AnyPresent briefing 09: Risks, legal and tax setup, and the things you did not ask

## Short answer

Three things you did not ask about will matter more than several things you did: your business and tax registration (a loose end since 2021 that any stipend application will touch), the durability of the iOS keyboard mode (doc 02), and the solo-founder support load. Below are the unasked items in order of consequence, each with the action I would take. I am not a lawyer or tax adviser; where I say "ask a Steuerberater", do that once, it costs about €150 to €300 and settles things for years. Confidence: high on what to check, medium on the specifics.

## 1. Legal and tax setup (do this in October)

The situation: an app has been sold since 2021, with ad income too, under your name, with "no legal setup". In Germany, selling software to the public on an ongoing basis is normally a trade (gewerblich), which means a trade registration (Gewerbeanmeldung) at the start of the activity, and all income belongs in your income tax return whether or not any tax results. Some software work can count as freelance (freiberuflich) instead; which applies to app sales is a question for a Steuerberater, not for me.

What this means in practice:
- The amounts are small (roughly €4,000 to €5,000 over five years) and as a student your income tax was probably zero, so the likely outcome is paperwork, not money. But it must be tidy before a stipend application asks "have you been commercially active?" and before the Berlin incubator or PtJ asks for a declaration.
- Register a sole proprietorship now (Berlin's Gewerbeanmeldung is online and costs about €15 to €30). Use the small-business VAT exemption (Kleinunternehmerregelung: up to €25,000 revenue in the previous year and €100,000 in the current year since 2025), so no VAT on your side.
- App-store sales in the EU are handled by Apple and Google as the seller of record, so VAT on consumer sales is their problem; you receive payouts. For website sales of business licenses, use a merchant of record (Paddle or Lemon Squeezy) so VAT, invoices and reverse-charge questions are theirs too.
- Ask the Steuerberater about the past years once; a late voluntary declaration of small amounts is routine.
- "Appless" can stay as a trade name; your real name and address must appear in the Impressum and in the stores' legal fields while you are a sole proprietor. A UG or GmbH only comes when a stipend requires founding or revenue justifies it.

Website obligations from day one: an Impressum (required in Germany for any non-private site), a privacy policy that truthfully says what the relay does and that no accounts or personal data exist, and a short terms page for the business license. Store privacy labels must match reality (see metrics below).

## 2. Platform risks, with the plan if each one bites

| Risk | Likelihood | If it happens |
|---|---|---|
| App Review rejects the iOS keyboard mode | Medium at first submission, low after acceptance | iOS becomes companion-first; the web viewer and relay carry the "nothing to install" story; Android keeps keyboard mode; the second product on iOS is dead |
| A later iOS release breaks the keyboard mode | Low per year, meaningful over five years | Same as above, but with existing users to migrate; isolate the code, test every beta from June, keep the status line honest |
| Apple rejects volume buttons (2.5.9) | High | Ship without it; try once as an update with a review note; on-screen controls are good enough |
| Android OEM Bluetooth stacks fail on some phones | Certain for a minority | Diagnostics, relay fallback, the "which phones" compatibility page |
| Windows SmartScreen warnings on the companion download | Certain without signing | Ship the Windows companion through the Microsoft Store (signed by Microsoft, deployable by IT), keep the direct download as secondary (doc 06); a standard code-signing certificate for individuals costs about €150 to €300 a year if you need one; Azure's cheaper Trusted Signing has had eligibility limits for individuals, so check before relying on it |
| Google Play policy changes (target SDK, Bluetooth permissions) | Annual | Budget one week a year for compliance updates; this is what killed the old listing's visibility |
| A relay abuse problem (code brute force, spam sessions) | Low | Rate limits per IP and per code, short code lifetimes, codes bound to a companion identity. Cheap, do it in v1 |

## 3. Support load

Connection support is the heaviest kind there is: every ticket is "it does not connect" with a different phone, computer, OS version and Bluetooth stack. Plan for it rather than being surprised:
- A troubleshooting page per OS, linked from the app's diagnostics screen and from every store reply.
- Reply templates for the five common cases (paired to another device, Windows re-pair, phone Bluetooth stack, companion not running, wrong window focused).
- An email address, not a chat or a Discord. Batch replies once a day.
- Budget two to four hours a week after launch. If it grows past that, the diagnostics screen is not good enough yet.

## 4. Metrics, and the privacy label

You cannot steer without a funnel: installs, first pairing attempt, pairing success by mode and host OS, first slide change, companion installed, effect used, paywall seen, purchase, rating prompt shown. Keep it anonymous and aggregated (a privacy-first analytics service or a few counters on your own Workers), with no identifiers and no account. Then say so honestly in the store privacy label: "usage data, not linked to you" is still a disclosure, and "data not collected" is only true if you collect nothing. Teachers and IT departments read these labels; an honest "anonymous usage counts, no personal data" is fine. Write it into the GDPR one-pager.

## 5. Costs for year one

| Item | Cost |
|---|---|
| Apple Developer Program | €99 a year |
| Google Play developer account | one-time, already paid |
| Domain | about €15 a year |
| Cloudflare | €0, later €5 a month (your decision, not recalculated) |
| Microsoft Store developer account | about €19 one-time |
| Windows code signing, only if direct downloads need it | €0 to €300 a year |
| Steuerberater, one session | €150 to €300 |
| Trade registration | €15 to €30 |
| Trademark (optional, later) | €290 |
| Apple Watch for testing (when you reach it) | €150 to €300 used |
| Screenshot template | €0 to €40 |
| **Total** | **roughly €500 to €1,400** |

A stipend's material budget covers all of it. Without a stipend it is still less than one month of Base-case revenue in year two.

## 6. Timing against the academic calendar

Student presentations cluster in late January to February (winter semester, German exams and US spring start), April to May, and late September to November. A mid-January launch catches the first wave; the web viewer in February and March catches the second; summer is dead and good for building 1.2 and the second product; late August to September is the "back to school" moment for a second push and the best time for a US education outreach round.

## 7. Chromebooks and school PCs

US K-12 runs on Chromebooks that cannot install your companion but accept Bluetooth keyboards and run Chrome. Keyboard mode plus the web viewer covers them completely. Mention "Works with Chromebook" in listings and content once you have tested it; it is a searched phrase and nobody else claims it.

## 8. Ratings strategy

Your old 3.77 stars were a reliability verdict. For the new app: prompt only after success (doc 03), answer every negative review with a fix or a path, and watch the rating by OS version so you catch a platform regression within days. A 4.4 star rating with a few hundred reviews is the single strongest asset in this niche, and it is what no clone can vibe-code.

## 9. Solo-founder bandwidth and burnout

You estimate v1 before December at 40 hours a week. I would add four to six weeks for the parts that are not code: store review cycles, signing and notarization, the Microsoft Store queue, screenshots, localization, the website, the stipend application, and testers' feedback. Plan mid-January for public launch and protect weekends. The failure mode for solo app founders in this niche is not running out of ideas; it is grinding on connection support and store compliance for a product that earns €400 a month and never making the day-90 decision. Write the criteria down (doc 01) and keep the appointment with yourself.

## 10. Exit options and the asset view

Small utility apps with steady revenue sell. At €1,500 a month with growth, buyers on acquisition marketplaces pay roughly 2.5 to 4 times annual revenue, so €45,000 to €70,000; at €500 a month, €10,000 to €20,000. App publishers who roll up utilities (the kind that own apps like Bluetouch's neighbours) are the other buyer. This is not a plan, but it is a floor under the "is it worth it" question: the work produces a sellable asset even in the Base case.

## 11. Things I would do differently from the brief

- Design the relay from the start so that any controller (phone app, web remote, watch via phone) and any target (companion, web viewer) speak the same message schema. That one decision makes the web viewer, the web remote and the watches cheap later and is the only architectural point in these documents.
- Submit the minimal iOS build to App Review in November rather than finishing everything first. Learning Apple's answer early is worth more than any feature.
- Treat the Microsoft Store as the primary Windows channel, for the free signing and the IT trust, rather than a signed installer on the website.
- Give the website viewer a real launch of its own, aimed at teachers.

## What I am not sure about

- **The exact tax classification** of your app sales (trade versus freelance) and anything about past years. One Steuerberater session settles it.
- **Azure Trusted Signing availability** for individual developers in Germany at the moment; check the current terms before relying on it.
- **How much support the diagnostics screen deflects.** If it works, support stays under two hours a week; if not, four or more.
- **Marketplace multiples** for apps with visible platform risk (the iOS keyboard mode) may be lower than the range above.
