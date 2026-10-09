# Monetization: accounts, the free launch phase, the locking line, cosmetics, business, the toast

## 1. Accounts: no in v1, and how Pro still travels

Decision: account-less in v1. Pro travels by session, not by identity.

- A Pro phone connected to the companion makes that companion session Pro: no toast, no effect credit.
- A Pro phone connected to the web viewer (by code or by scanning its QR) makes that viewer session Pro. The relay marks the session when a Pro controller joins. No account needed.
- A business license key entered in the companion or in the web viewer makes that machine or that browser Pro for everyone who connects.
- The web remote used alone is free with credit until the session gains a Pro phone or a license.

So "the website can never be Pro" is false under this model: the website is Pro whenever a Pro presenter is in the session.

Rule for the data model: store each purchase as a record that can later be linked to an optional identity (Apple's app account token, Google's obfuscated account id, and an optional email field). Do not build sign-in now. When a concrete need arrives (consumers who switch platforms, a company that wants "everyone at @company.com is Pro"), add magic-link email sign-in as an optional feature; on Workers that is a few days then, and zero now if the record exists.

Why not accounts now: friction before the first success, a GDPR surface that teachers notice, a backend to support, and a sign-in system you would have to maintain for years. None of that is worth it for a problem the session model already solves. Your "premium settings unlocked" worry about PC licenses also disappears: with effects free with credit, the PC license only removes the credit and the toast, so there is nothing on the phone to unlock from a computer.

## 2. The locking line

Principle: what the audience sees stays free, because that is what spreads. What only the payer values is paid. Reliability is never paid.

| | Free | Pro (one-time) | Pro+ (subscription, Phase 2) | Business (license key) | Institution |
|---|---|---|---|---|---|
| All connection modes, next, previous, black, white, timer | yes | | | | |
| Laser, spotlight, magnifier | yes, with credit | credit removed | | credit removed on licensed machines | free tier with toast; paid tier without, plus admin page |
| Connection toast on the big screen | shown | removed | | removed | see above |
| Group mode, web viewer, web remote, watch basics | yes | | | | |
| Three to five fun pointers | yes | full pack | | | |
| Custom shortcuts, extra effects, notes, thumbnails, jump to slide | | yes | | | |
| Transcription, recap, rehearsal analytics, live captions | | | yes | yes, per seat | yes, campus |
| Invoice, deployment packages, priority support | | | | yes | yes |
| Event mode | | | | per event | |

Watches: the basics are free. They are a headline feature for installs and reviews and the audience never sees them. A watch owner skews toward paying, so watch notes and timer alerts sit in Pro together with notes.

## 3. The free launch phase: yes, with four rules

Why: the stipend pays your year, so year-one revenue matters less than users, ratings and data; the free phase matches both programmes' "no business activity before the start" rule under any reading; and it lets you set Pro prices with data instead of guesses.

1. **The credit exists from day one** (the toast and the effect credit). Nobody will ever lose something they had; Pro will only ever remove something that was always there. This is what prevents "they took features away" reviews.
2. **Build the purchase infrastructure now, hidden.** Products, receipts, the Pro signal to the companion and the relay. Switching the price on is then a server flag and a store metadata change, not a review cycle.
3. **Badge the Pro features from day one** as "Pro, free during the launch phase", so everyone learns which features are Pro while they are still free, and the later price surprises nobody. When you switch the price on, add the new Pro features (thumbnails, jump, notes) at the same time, so the moment reads as "more", not "less".
4. **Promise early-user perks and keep them:** "Early users keep Pro." Mechanics: on iOS, offer codes on request at the switch-on moment; on Android, a local early-user flag plus "email us if you reinstall", because Google's 500 promo codes a quarter cannot cover thousands. The perk is cheap and buys loyalty and reviews.

Timing: price Pro on in month 3 to 5 after launch, once the stipend has started and the Phase 2 features are ready. Do not call the launch phase a "beta" in the App Store: Apple's guideline 2.2 rejects apps presented as betas or demos. "Launch phase" and "early access" are fine on both stores.

Cost of waiting: perhaps €1,000 to €2,000 of Pro revenue in the first months. Gain: installs, reviews and word of mouth during the launch wave, cleaner stipend compliance, and pricing data.

## 4. Fun and cosmetic pointers

Precedent: cosmetics are the most reliable low-ticket revenue in games and chat apps, and here the cosmetic is seen by the whole room.

Catalogue: three to five free fun pointers to seed spread and video clips; singles at €0.99 to €1.99; a pack at €4.99 that Pro includes; seasonal pointers (Halloween, Christmas, exam season); one deliberately absurd luxury pointer at €49.99 or €99.99 as a marketing stunt that you expect to sell almost never and to be talked about. Later: community-submitted pointers that you curate, which is engagement for free.

Rules: keep the Fun category visually separate so a business user never meets a cat pointer by accident; never set a fun pointer as a default; make the luxury item clearly a cosmetic so no reviewer reads it as a scam.

Expectation: low single-digit percent of revenue, a high share of social-video hooks.

## 5. Business: what they actually want

No credit, an invoice, a deployment package, no accounts to manage, a privacy sheet, and a human to email. Not their logo in the spotlight; you are right, dropped.

Mechanics: a license key sold on the website through a merchant of record (Paddle or Lemon Squeezy, which handle VAT and invoices), entered once in the companion or the web viewer, valid per machine or per seat count. The phone app never shows a key field (Apple's rule 3.1.1 forbids your own unlock mechanisms inside the app); it only displays "Licensed by this computer".

Tiers: Business (per seat, with Pro+ included), Institution (campus or school, with the admin page), Event (per event). Prices in section 7.

Waitlist page now: a Business page with three fields (email, organization type, team size) and three survey questions (what they present with, whether they can install software, what they pay for today). It doubles as evidence for the application.

## 6. The connection toast: the primary free-tier credit

Your idea, and I would make it the main credit, because it appears in every companion session and the screen is usually already projected when the phone connects.

Design: bottom centre, two to three seconds, the system style of an "AirPods connected" notice: a small icon, "AnyPresent connected · anypresent.com", then a fade. Once per session on connect, once more on reconnect, never during a slide change. Pro removes it; a licensed machine removes it; the institutional free tier keeps it.

Measure: direct traffic to the site and the "saw it on a screen" option in the "how did you hear about us?" question. Test a variant with the URL only.

## 7. Pricing anchors and the mistakes that cost money later

- **Do not price Pro below €7.99.** Raising a price later is possible (owners keep what they bought), but reviews remember the old number and the pass undercuts it. Price Pro at €9.99 with a labelled "early-access price" of €6.99 for a few weeks if you want a launch moment.
- **Pro+** (transcription, captions, recap, rehearsal analytics) as a subscription when it ships: about €3.99 a month or €24.99 a year, Pro included, with one-time Pro kept forever as its own product.
- **Business** per seat at about €29 one-time or €15 a year. **Institution** and **Event** prices from the pilots; €1,000 to €5,000 a year per campus and €20 to €50 per event are placeholders.
- **7-day pass** at €1.99 when Pro is priced, for the one-off presenter; raise it or shorten it if passes exceed 40% of revenue.
- **Grandfathering** of one-time purchases is automatic across price changes; early-user perks need the code mechanics in section 3.
- **Regional pricing:** accept the stores' equalization, then lower tiers in high-install, low-conversion countries once you see the data.

## 8. Revenue expectations under this plan

Year one shifts down (Pro priced in month 3 to 5, business from month 5), year two shifts up (a larger base, Pro+, institutions). The directions file's expectation column shows €2,000 to €4,000 MRR at month 12 as the realistic good case under the full plan; the stipend covers the gap, which is the point of taking it.

## What I am not sure about

- Whether Pro by session (a Pro phone making a web viewer Pro) draws scrutiny from App Review. It unlocks nothing inside the iOS app itself, so I expect no issue, but reviewers vary.
- The early-user perk on Android without accounts is imperfect; a reinstall loses it, and "email us" covers the few who care.
- Cosmetics may be worth more or less than I think; this is the one item where a social-video outcome could surprise in either direction.
- Business, institution and event prices are placeholders until the waitlist and the pilots speak.
