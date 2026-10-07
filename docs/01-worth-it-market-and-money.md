# AnyPresent briefing 01: Is it worth it, how big can it get, and what will it earn

## Short answer

Yes, worth building, under three conditions: you launch by mid-January 2027, you measure for 90 days against criteria you write down now, and you pursue the stipend in parallel because it changes year-one economics more than any product choice. Without a stipend, year one is poorly paid work whose return arrives in years two and three or through a sale. With a stipend, year one is a paid year building an asset you own. Confidence: high.

## The most reliable data point you have: the old app

The old app is the only evidence about this exact product in this exact niche run by you, so I weight it heavily.

| Metric | Value | What I read from it |
|---|---|---|
| Lifetime installs | ~46,000 over ~5.3 years | ~720 a month on average; probably 1,000 to 1,500 a month in the first two years, then decay, now 38 a month while hidden |
| Pro buyers | ~1,200 at $4.99 | 2.6% of installs paid, through the higher-friction route of a separate paid app. That is a healthy conversion for a utility |
| Gross Pro revenue | ~$6,000 lifetime, ~€4,000 to €4,500 net | Matches your €50 to €100 a month |
| Marketing | Almost none | So this is the floor for what the niche gives a listing that merely exists |
| Platforms | Android only, English only, connection failures on some devices, no iPhone | Each of these is a multiplier you now get to fix |

The relaunch fixes four multipliers at once: iPhone (60% of US mobile traffic, and US universities are iPhone and Mac heavy), localization (store search is per storefront), reliability (the auto-fallback ladder), and effects (a reason to pay beyond "it is a clicker"). A product that was earning €80 a month with all four multipliers missing is a reasonable base for a product earning ten times that with them fixed. That is the core of my optimism, and it is also where the uncertainty lives: I do not know how much each multiplier is worth, and the appendix data cannot tell us.

## How big the market is (my derivation)

Nobody publishes market sizes for phone presenter apps, so I triangulate from the appendix.

- **Presenter apps specifically.** PPTControl does ~3,700 Android installs a month with a 3.1-star rating and a mandatory desktop app. Its iOS side is probably similar or larger (it has Apple Watch support, the US skews iOS), so call it 7,000 to 10,000 installs a month for the category leader. Remote for Slides has 100,000 users total after years. Three dead apps had 2.2 million, 710,000 and 290,000 lifetime installs. My read: the whole category, all apps on both platforms, sees perhaps 20,000 to 50,000 installs a month worldwide. A top-three app can expect 5,000 to 15,000 a month. Confidence: low to medium.
- **General "phone as keyboard or mouse" apps are a different league.** Appground's Bluetooth Keyboard & Mouse does 100,000 installs a month on Android alone, 9.7 million lifetime. Remote Mouse does 73,000 a month. Unified Remote has 14 million lifetime installs and its company reported SEK 953,000 (roughly €85,000) of revenue for 2025. Two conclusions: (a) the adjacent general-purpose market is about 25 times larger than the presenter niche, and (b) even 14 million installs of a general remote produced only about €7,000 a month for a mature company. That is the ceiling shape for this whole family of utilities: large install numbers, low revenue per install.
- **Hardware demand tells you intent exists.** About 30,000 clickers a month from the top ten listings on Amazon US, mostly $10 to $20, and ~7,700 weekly Amazon searches for "presentation clicker". People search for hardware because they do not know a phone can do it. That is both the limit (discoverability) and the opportunity (content that intercepts "do I need a clicker" searches). Logitech Spotlight sells ~500 units a month on Amazon US at $120: the premium "effects" segment is tiny in units, but it proves people pay for the spotlight experience, and you can serve the much larger group that will pay €10 but not $120.
- **Students.** Tens of millions of tertiary students in the US and EU, each presenting a few times a year. The reported shift toward in-class presentations and oral exams because of AI-written homework (Fortune, April 2026) is a genuine tailwind, but small relative to the discoverability problem.

## What limits growth, ranked

1. **Purchase frequency and willingness to pay.** People present a few times a year, and the spacebar, a friend, Keynote Remote, Remote for Slides and an €8 clicker are all "good enough". This caps conversion at a few percent and the price at around €10. Nothing you build changes this much; effects and notes raise it a little.
2. **Discoverability.** "Best presentation remote" roundups do not mention apps. You have to win store search and write the content that intercepts hardware intent. This is the limit you can actually move, and it is cheap to move.
3. **Platform dependency.** The iOS keyboard mode rests on an unblessed workaround (doc 02). Apple's rule 2.5.9 blocks volume buttons on iOS. Android OEM Bluetooth stacks break HID on some phones (your old app's complaint).
4. **Solo bandwidth.** Six platforms, connection support (the heaviest kind of support there is), marketing, and store administration, all on one person. This is the limit most likely to make you stop, and it is why doc 06 argues for a narrow launch.
5. **Competitive response.** PPTControl's September 2026 redesign explicitly advertises connection stability. Appground could ship an iOS app or a better presenter mode any time. First-party moves (Apple, Microsoft, Google) are unlikely but would be decisive.

## Revenue scenarios (12 months after public launch)

Assumptions are stated so you can replace them with data. "Installs" means both phone platforms combined, "conversion" means any payment within the first months after install, "ARPPU" is net revenue per paying user after store fees at the 15% small-business rate. Launch pricing per doc 04: Pro at €5.99 launch price rising to €9.99, 7-day pass €1.99.

| | Low | Base | High |
|---|---|---|---|
| Installs per month at month 6 to 12 | 2,000 | 6,000 | 15,000 |
| Paid conversion | 1.2% | 2.2% | 3.0% |
| ARPPU (net) | €5.50 | €6.50 | €7.50 |
| Consumer revenue per month | ~€130 | ~€860 | ~€3,400 |
| Business licenses per month | €0 | ~€150 | ~€800 |
| **Monthly revenue at month 12** | **~€130** | **~€1,000** | **~€4,200** |
| Cumulative first-year revenue (ramping) | ~€500 | ~€5,000 | ~€18,000 |
| Year-two run rate (prices at full level, installs flat to slightly up) | ~€150/month | ~€1,500/month | ~€5,000/month |

My subjective probabilities: Low 30%, Base 45%, High 20%, and a 5% "breakout" case above €8,000 a month that requires the second product or an education or business channel to work. The median outcome is the Base column. The expected value is pulled up by the tail to roughly €1,800 a month at month 12, but you should plan on the median.

How the numbers come about:
- Installs: the old listing did ~1,000 a month with none of the multipliers. Two platforms, ten languages, a working connection story, effects in the screenshots and the old Android listing's history should give several times that. PPTControl's 3,700 a month on Android alone with a 3.1-star rating is the sanity check for the Base case. The High case assumes you rank first or second for the main search terms in the big storefronts.
- Conversion: the old app achieved 2.6% through a separate paid app. In-app purchases are lower friction, effects give a visible reason to pay, but the free tier is more generous than before. I shade down to 2.2% for Base.
- ARPPU: mostly €5.99 to €9.99 one-time purchases at 85% net, diluted by €1.99 passes.
- Business: pure guess, included so you remember it exists.

## The hourly-rate reality check

| | Hours | Revenue | Implied rate |
|---|---|---|---|
| Build to public v1 (October to mid-January) | ~450 to 500 | €0 | €0 |
| Rest of year one (1.x releases, marketing, support) | ~450 | ~€5,000 (Base) | about €5 an hour on the whole year |
| Year two (maintenance plus marketing) | ~400 | ~€18,000 (Base) | about €45 an hour |
| Asset value at end of year two (Base) | | €1,500 MRR apps with growth sell for roughly 2.5 to 4 times annual revenue | €45,000 to €70,000 |

Compare: a working-student job at 20 hours a week pays €1,200 to €1,600 a month; a junior developer in Berlin earns €45,000 to €55,000 gross. If your only goal were maximum income in the next 12 months and no stipend were available, a job wins. With a stipend of €1,000 to €2,500 a month, the app plus stipend wins on income and keeps every option open. Without a stipend, the app is a bet on years two and three, on the second product, and on the sale value. You said income is the main goal: that is exactly why doc 07 matters more than doc 06.

## What would make it worth it, and what would not

Worth it, any one of these:
- A stipend approval (guaranteed €12,000 to €45,000 for the year, and an excuse to do it properly).
- Base-case or better install numbers after 90 days (3,000 or more a month organically).
- Conversion at or above 2% once effects are in the screenshots.
- The keyboard and mouse second product showing a larger funnel than the presenter app.
- Any education or business channel that produces a repeatable order.

Not worth continuing full-time, any one of these after 90 days of a real launch:
- Fewer than 1,500 organic installs a month across both platforms after ASO and localization are done.
- Pairing success below 80% on the paths you control (companion and relay), because the reviews will never recover.
- Rating stuck below 4.0 for reasons you cannot fix (platform-level Bluetooth failures).
- Apple rejects the HID mode and the companion path alone does not convert.
- A better-paying use of the year appears and the app is at Low case.

## Kill and continue criteria at day 90 after public launch (write these in your decision log now)

| Metric | Continue full-time | Reduce to part-time, start second product | Maintenance mode |
|---|---|---|---|
| Organic installs per month (both platforms) | 3,000 or more | 1,500 to 3,000 | under 1,500 |
| Paired-and-used rate (first slide change within a session) | 85% or more | 70 to 85% | under 70% |
| Paid conversion | 2% or more | 1 to 2% | under 1% |
| Store rating (both) | 4.3 or more | 4.0 to 4.3 | under 4.0 |

If a stipend is approved, "maintenance mode" becomes "finish the funded year anyway, but shift the roadmap toward the second product and the business channel".

## Realistic size, stated plainly

Two years out, a well-run AnyPresent is 100,000 to 500,000 lifetime installs, €1,000 to €3,000 a month, 4.4 stars, listed on a dozen university help pages, with a desktop companion that IT departments tolerate. That is the honest "good" case. The "great" case is a family of two or three "nothing to install" apps sharing one core and earning €5,000 to €10,000 a month combined, which is where Appground and Unified Remote live. A venture-scale outcome is not on the table and you should not spend time pretending otherwise to anyone, including stipend juries (doc 07 explains how to pitch honestly and still get funded).

## What I am not sure about

- **Install volume** is the dominant uncertainty, and it is only knowable by launching. Expect the first two months to be noisy and the third to be informative.
- **Conversion with a generous free tier.** The old app's 2.6% came from a tight free tier (I assume). If effects-with-watermark satisfy most people, conversion could land near 1%. The pass and the no-watermark unlock are the levers; measure, do not guess.
- **My category sizing** (20,000 to 50,000 installs a month worldwide) is a triangulation from four data points. It could be off by a factor of two in either direction.
- **The business column** is a placeholder. There is no evidence either way; it costs little to offer and find out.
- **Sale multiples** for small utility apps vary widely with growth and platform risk. Treat €45,000 to €70,000 as a plausible range, not a plan.
