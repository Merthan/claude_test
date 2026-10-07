# AnyPresent briefing 00: Overview and the big decisions

*Independent second opinion, written 7 October 2026 from the README brief. I spot-checked the appendix facts that actually swing a decision (stipend rules, Apple guideline 2.5.9, the iOS Bluetooth HID situation, PPTControl's current state, first-party phone remotes). Sources are linked in the documents that use them. Everything else is reasoning, and I say how confident I am.*

## How to read this

Eleven documents, one per topic, numbered in the order I would read them. Each ends with a "What I am not sure about" section, because you asked for that explicitly. Confidence labels:

- **High**: I would act on this without more data.
- **Medium**: a reasonable bet that is cheap to reverse, or I would want one check first.
- **Low**: a guess that data should replace. I say which data.

## The verdict in one paragraph

Build it, but as a staged bet with a fixed launch date and written kill criteria, not as an open-ended project. This is a good tool business in a small niche. A well-executed launch realistically earns €500 to €2,000 a month after a year, with upside to €5,000 and beyond only if an adjacent product (the "nothing to install" keyboard and mouse app) or an education or business channel works. That is a respectable side income and a sellable asset, not a company that funds a life on its own. The decision that matters most for your income in the next 12 months is not a product decision: it is whether you secure a stipend. €12,000 to €45,000 of guaranteed money dwarfs anything the app earns in year one, and the Berliner Startup Stipendium's Batch IV window is open now (October to November 2026) for a January 2027 start. That makes the stipend question time-critical this month. Confidence: high on the shape, medium on the numbers.

## The ten big decisions

| # | Decision | My recommendation | Confidence | Doc |
|---|---|---|---|---|
| 1 | Build it or not | Yes. Roughly 400 to 500 hours to a public v1 by mid-January 2027, then a 90-day measurement with kill or continue criteria written down in advance. | High | 01 |
| 2 | Stipend first or sell first | Do both in the order that the rules allow: apply now (Berlin Batch IV first, EXIST as the fallback), launch the free version now, and switch on paid features when funding starts, or on a hard date if funding fails. Confirm with your Gründungsservice this month whether a free public launch counts as "business activity". | Medium (rules need one confirmation) | 07 |
| 3 | Monetization model | Free core, one-time Pro unlock (no watermark, extra effects, later notes and watch), a cheap 7-day pass for one-off presenters, business licenses sold through the desktop companion and website. No subscription at launch. No ads, ever. | High on structure, medium on prices | 04 |
| 4 | The watermark strategy | Keep it, but treat it as a modest, free, compounding channel, not the growth engine. App store search (ASO) plus localization is the engine. Watermark: small, the URL, only while an effect is active. | High | 03 |
| 5 | Connection-mode UX | Never present five modes. Auto-detect, default to keyboard mode when no companion is found, soft-upsell the companion. The user answers at most one question: "Can you install something on that computer?" | High | 05 |
| 6 | Feature scope | Launch narrow: clicker, gyro laser, spotlight, magnifier, timer, black screen, on iOS and Android, with the macOS and Windows companion. Watches, notes, and the web viewer come in 1.1 and 1.2. Your real constraint is the test and support surface across six platforms, not bloat in the store listing. | High | 06 |
| 7 | Website fallback (viewer plus web remote) | Rank it higher than you do. It hedges the iOS platform risk, serves school PCs and Chromebooks, and is your SEO landing page. Ship a basic version within two months of launch. | Medium | 06, 03 |
| 8 | Android strategy | Update the old app in place (same package name) instead of a new listing, and grandfather the old Pro app's buyers automatically. | Medium | 04, 06 |
| 9 | Name | Keep AnyPresent. Fine, not brilliant. The store subtitle carries the keywords; the watermark should read anypresent.com. | High | 08 |
| 10 | Second product | After 90 days of data, seriously evaluate a "nothing to install keyboard and mouse" app on iOS sharing your HID core. That market is roughly 25 times larger than presenter apps and the iOS incumbent is weak. | Medium | 06, 01 |

## Where I disagree with your assumptions

1. **"Most students use it for free" is not a planning basis.** The most successful apps in this category reach single-digit millions of lifetime installs over a decade. Plan for 100,000 to 500,000 lifetime installs in two years and be pleased if you beat it.
2. **The watermark reaches fewer eyes than you think.** It shows only when the companion is installed and an effect is active. Most student use will be plain slide control with nothing installed, where no audience sees anything. The loop is real but narrow. Doc 03 has the arithmetic.
3. **"Bloat is fine" is true for downloads but not for you.** You are one person shipping on iOS, Android, macOS, Windows, web, Wear OS and watchOS. Each feature multiplies the test matrix and the support inbox. Code scales with LLM assistance; testing and support do not.
4. **Watches at launch: no.** Wear OS in 1.1 (you are an Android developer and Galaxy Watch owners were orphaned by Samsung's Android 15 restriction and WowMouse's removal), Apple Watch in 1.2 once users ask.
5. **The iOS "nothing to install" mode is your most fragile asset.** Apple's CoreBluetooth nominally refuses the standard HID service for peripherals; the shipping apps use a workaround that Apple has not blessed. It works today and may work for years, or vanish with one iOS release or one reviewer. Do not let the product's identity on iOS depend on it. Companion and relay must be first-class, and you should submit a minimal iOS build to App Review early (with manual release) to learn whether Apple accepts it before you invest everything else.
6. **Your legal and tax state is a loose end.** Revenue since 2021 without any registration will surface in any stipend application and needs fixing either way. Doc 09 explains, without drama.

## What I am least sure about, and what would settle it

| Unknown | Why it matters | What settles it | By when |
|---|---|---|---|
| Organic install volume you can reach | Dominates the revenue estimate (a factor of 3 either way) | First 60 days of store data after ASO and localization | March 2027 |
| Whether a free launch counts as "business activity" for EXIST or Berlin | Decides launch sequencing | One conversation with your university's Gründungsservice; if needed one email to Projektträger Jülich | October 2026 |
| Which EXIST rate applies (€1,000 student vs €2,500 graduate) | €18,000 difference over the year | Same conversation | October 2026 |
| Durability of the iOS HID workaround | The iOS "no setup" promise | Early App Review submission; test every iOS beta; fallback-first design | November 2026, then yearly |
| Paid conversion with effects (1% or 3%?) | Three-fold revenue swing | 90 days of paywall data | April 2027 |
| Whether businesses buy at all | Upside only | Offer a license, count inquiries | Mid-2027 |
| The watermark's real viral effect | Marketing time allocation | Direct traffic to anypresent.com; one-tap "how did you hear about us" | Mid-2027 |

## Decision log (fill in as you decide)

| Decision | My recommendation | Your decision | Date |
|---|---|---|---|
| Build | Yes, staged | | |
| Stipend path | Berlin Batch IV now, EXIST fallback, free launch now | | |
| Monetization | Free + Pro unlock + pass + business license | | |
| Watermark | Keep, small, URL, effects only | | |
| Connection UX | Auto-ladder, one question | | |
| v1 scope | Narrow (doc 06 list) | | |
| Web viewer timing | Within 2 months of launch | | |
| Android listing | Update in place | | |
| Name | Keep | | |
| Second product | Evaluate at day 90 | | |

## The documents

- `01-worth-it-market-and-money.md`: is it worth it, how big it can get, my revenue scenarios and how I got them, kill and continue criteria.
- `02-competition-moat-and-copycats.md`: competitor map, whether people will vibe-code alternatives, where the moat really is, platform risks.
- `03-growth-and-marketing.md`: the watermark thesis examined, channels ranked, ASO, education, content, a launch plan, what to do with €200.
- `04-monetization-and-pricing.md`: the model, the prices, business licensing without hurting students, store mechanics, what to avoid.
- `05-ux-onboarding-and-companion.md`: connection ladder, first five minutes, companion pairing, presenter screen, failure recovery.
- `06-features-and-roadmap.md`: v1, 1.1, 1.2, later, never; platform sequencing; the second product.
- `07-startup-vs-tool-and-stipends.md`: EXIST versus Berlin versus bootstrapping, timing, eligibility unknowns, the application narrative, questions to ask.
- `08-name-and-brand.md`: the name, store naming, watermark design, trademark.
- `09-risks-legal-and-unasked.md`: tax and registration, platform risks, support load, metrics, costs, calendar, things you did not ask.
- `10-open-questions-and-next-30-days.md`: the unknowns table, an ordered 30-day plan, all sources.
