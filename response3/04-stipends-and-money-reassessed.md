# Stipends and money, reassessed with the custom pipeline

## Short answer

The speech pipeline makes you fundable where "a clicker app" was marginal. Four actions this week decide the next six months: settle the team-size rule at the Berlin incubators (if Science & Startups really requires two to four founders, a co-founder is not a cost under this programme, they bring their own €2,500 a month), re-approach the EXIST contact with a one-page technical summary and a mentor from a speech or usability group, decide whether you are willing to open-source the speech library (that unlocks the Prototype Fund and NLnet, and nothing else does), and keep the December release free of in-app purchases until the stipend question is answered. Confidence: high on the actions, medium on the dates, which I could not confirm on the sites themselves.

## What the research found (dates marked "confirm" could not be read on the site from this session)

| Programme | What it gives | What I found | Status for you |
|---|---|---|---|
| Berliner Startup Stipendium | up to €2,500 a month per founder, usually 12 months, through an incubator | The Senate's April 2026 overview lists application windows in January to February 2027 with a 1 April 2027 start (Batch V), which matches your TU statement. A third-party listing shows a Science & Startups Batch IV with a 4 November 2026 noon deadline and a 4 January 2027 start, and lists its conditions as teams of two to four founders, main residence in Berlin, full-time commitment with no employment and no full-time study; the official overview does not show that batch, so treat it as unconfirmed. The January thematic programmes (Adlershof smart city, Vision Health) do not fit | Apply for the April start. The team-size rule is the open question |
| EXIST Gründungsstipendium | €2,500 a month (graduate rate), 12 months, plus up to €10,000 costs and €5,000 coaching | Rules unchanged. Your contact's "too research-based" has two readings: the programme favours technology-based innovation and a clicker app did not qualify, or they confused it with EXIST-Forschungstransfer, which does require research results | Re-approach with the technical summary below; it changes the first reading |
| Prototype Fund | about €47,500 per project for six months (2024 figure; the newer programme may differ, confirm), for individuals and small teams resident in Germany, results under an open-source licence | "Every fall you can apply"; the last review cycle ran December 2025 to February 2026; the 2026 window was not visible to me | Confirm the window today at prototypefund.de; only with the open-source decision |
| NLnet (NGI) | €5,000 to €50,000 per project (one source says more), open-source results, individuals welcome | The regular Commons Fund closed in June 2026 while NLnet moves to a new programme; its proposal page reportedly announced new calls opening 3 September with a 3 November 2026 deadline | A proposal is a few pages; feasible by 3 November only if you decide this week and only with the open-source decision |
| Cloudflare Workers Launchpad | introductions to venture investors and promotion for startups built on Workers; financing, not credits | "Applications for Cohort #7 are now open" on the programme page (undated); quarterly selection | Twenty minutes; apply once a company exists, or now |
| GründungsBONUS Plus (Berlin) | up to €50,000, up to 50% of setup costs | Needs a Berlin company and the other half of the money; applications listed until September 2027 | Park until the UG exists and revenue or a stipend covers the other half |
| Emergent Ventures (Mercatus) | small fast grants for ambitious young people | not researched beyond memory | A one-page long shot; low confidence |

## The team-size question is the one to settle this week

If Science & Startups (TU, HU, FU, Charité) requires two to four founders, you have three moves:

1. **Ask other carriers.** HWR's Startup Incubator Berlin, the HTW and BHT services and the UdK centre run their own calls under the same programme and may accept solo founders. Ask each in one email: solo accepted, next batch dates, whether a free public release before the start matters.
2. **Reframe the co-founder.** Under this programme each founder receives their own stipend, so a co-founder adds a funded, full-time person to the project for twelve months at no cost to you. A business, education or marketing co-founder with 10 to 20% equity who spends a year on university pilots, Toastmasters clubs and the launch push is a good trade even before the stipend; with it, it is obviously good. Both EXIST and Berlin prefer teams. Where to look: TU's Centre for Entrepreneurship matching, Startup Night Berlin, a Wirtschaftsinformatik classmate who wants to found, and a Berlin Toastmasters club, where you will find communicators who understand the coach instantly.
3. **Mind the full-time rule.** "No full-time study" means exmatriculating or switching to part-time before the start, which you planned anyway.

Timeline: the January to February window gives you ten weeks to find a co-founder if one is required. Start now; do not wait for the incubators' reply to start looking.

## EXIST, re-approached

Send a one-page technical summary, with numbers, and ask for a second opinion. The bullets:

- A 155 MB on-device speech model with the same word error rate as the 305 MB reference (your own 4-bit recipe, measured on FLEURS and on 29 real talks: 10.9%).
- A decoder patch that reads filler probabilities on every frame without changing the recognised text (English fillers 72% found at 94% precision).
- Speaker turns in ggml with a custom im2col operator, 1.45% equal error rate, main speaker right in 4 of 4 meetings.
- Eight languages, on a phone, at 19 times real time, with nothing uploaded; word timing within 70 ms of a commercial service; calibrated confidences.
- A measurement culture: identity tests, a 45-file verification gate, an evaluation suite over hundreds of files.

That is a technology-based venture by any jury's standard. Add a mentor professor from a speech, usability or machine-learning group; TU Berlin's Quality and Usability Lab works on exactly speech quality and prosody (verify who is there now and whether they take mentorships). Then the only remaining EXIST obstacle is sequencing: application December or January, decision around March or April, start May to July, later than Berlin. Apply in parallel if allowed, accept whichever comes first, and keep revenue off until the start.

## The open-source decision

What the open-source funders would require you to publish: the C++ library (engine patches, analytics, speaker turns, custom words, the API), the quantized model and its recipe, the evaluation tools. What stays yours: the app, the screens and UX, the server, the obfuscation pipeline, the brand, the remote, polls, integrations, and every dataset you cannot redistribute anyway.

For opening it:
- €47,500 (Prototype Fund) or €5,000 to €50,000 (NLnet), or both, is more than the coach is likely to earn in its first year under any scenario in doc 02.
- Credibility where it pays: German public institutions prefer open source ("digital sovereignty"), and "open source, on-device, funded by the Prototype Fund" is a sentence a university can put on a help page. It is also a Hacker News story and a GitHub reputation.
- Contributors: more languages, fixes, upstream patches to the engine.
- Future EU and NGI money requires it anyway.
- The engine's lead is six to twelve months regardless; your durable advantages are the product around it, the distribution, the eight-language app, and the fact that you also hold the clicker.

Against opening it:
- A competitor app could appear within weeks on top of your library, in your languages.
- Your obfuscation and encryption work becomes sunk cost.
- A half-open release (a crippled public version, the good parts private) is worse than either choice: it annoys the funders and the community and protects nothing.

My lean: apply, if a window is open now and you can live with the engine being public. 60 to 40, not 90 to 10. If you decide no, skip both funders entirely and do not revisit; if yes, do it whole-heartedly under Apache 2.0, with the model weights and the evaluation tools, and keep the product moat where it actually is. These grants do not care about app revenue, so they are compatible with pricing the app in February if the Berlin path fails.

## Sequencing: free now, priced later

| Situation | What to do |
|---|---|
| Berlin accepts solo founders at some carrier | Apply in the January to February window; release free in December; price Pro and Pro+ at the April start |
| Berlin requires a team and you find a co-founder by mid-January | Same, with two stipends |
| No stipend path by mid-January | Price Pro and Pro+ in February; keep applying for the open-source grants if you chose that path; apply to GründungsBONUS Plus after founding the UG once revenue covers the other half |
| EXIST reconsiders | Parallel application; accept the earlier of the two |

The cost of waiting from December to April is one to three thousand euros of early purchases. The stipend is thirty thousand, sixty with a co-founder.

## This week's emails and checks

1. Science & Startups (bss@science-startups.berlin): is there a Batch IV with a January start still open; solo founders; Batch V dates; does a free public release before the start matter.
2. HWR Startup Incubator Berlin and one more carrier: the same three questions.
3. Your EXIST contact: the technical one-pager, the mentor question, whether parallel applications are acceptable.
4. prototypefund.de: is the fall window open; amount and licence conditions.
5. nlnet.nl/propose: deadline and scope; submit a short proposal by 3 November if you chose open source.
6. Your Steuerberater: register the sole proprietorship now if not done; the coach does not change this.

## What I am not sure about

- **Every date in the table** that I could not read on the site: the Batch IV existence and deadline, the Prototype Fund window and amount, NLnet's 3 November deadline.
- **The team rule** at Science & Startups comes from a third-party listing of an earlier batch.
- **TU's Quality and Usability Lab** as a mentor source is from memory; confirm the group and its current head.
- **The open-source lean** is a judgement about where your moat is; if you believe the engine is the business, decide the other way and I would not argue hard.

## Sources checked

- Berlin Senate overview of the Berliner Startup Stipendium (20 April 2026): https://www.berlin.de/sen/wirtschaft/gruenden-und-foerdern/gruendungs-und-startup-foerderung/finanzielle-foerderung/zuschuesse/20260420_uebersicht_aufruf_2_berlinde_final.pdf
- Science & Startups Batch IV as listed by a third party (deadline, team rule): https://superscout.co/program/science-startups-berliner-startup-stipendium
- Prototype Fund application page and background: https://prototypefund.de/en/apply and https://www.munich-startup.de/en/news/prototype-fund-foerderung-fuer-public-interest-tech
- NLnet proposal page and 2026 call notice: https://www.nlnet.nl/propose and https://nlnet.nl/news/2026/20260601-call.html
- Cloudflare Workers Launchpad programme page: https://www.cloudflare.com/lp/workers-launchpad
- GründungsBONUS Plus: https://www.ibb-business-team.de/en/gruendungsbonus and https://www.foerderdatenbank.de/FDB/Content/DE/Foerderprogramm/Land/Berlin/gruendungsbonusplus-unterstuetzung-aufbau-startup.html
