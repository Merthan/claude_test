# AnyPresent briefing 03: Growth and marketing, including an honest look at the watermark

## Short answer

The watermark is a good, free, compounding channel and a poor growth engine. Keep it, make it small and actionable, measure it, and do not plan around it. The engine is store search in ten languages on two platforms, with effects in the screenshots, backed by content on anypresent.com that intercepts people searching for hardware clickers. Everything else (communities, short video, education outreach, deal sites) is a spike or a slow burn to layer on top. Spend the €200 on things that remove friction (Windows code signing or a screenshot template), not on ads. Confidence: high on the ranking, medium on the specific tactics.

## The watermark thesis, examined

Your thesis: students use it free with a watermark, audiences see the name, the name spreads, money comes from watermark removal and business users.

What is right about it: the audience is exactly the right people (classmates who will present next week), the mechanism has worked before ("Sent from my iPhone", Hotmail's footer, Loom and Zoom free tiers), and the cost is zero.

What is wrong with it as the engine:

1. **It only shows when an effect is active.** Effects need the companion. Most student use will be plain slide control with nothing installed. The audience then sees a student holding a phone, nothing more.
2. **Exposure per presentation is seconds.** Spotlight is used to point at one chart, then switched off.
3. **The arithmetic is small.** Suppose a strong year one: 10,000 monthly active presenters, 30% with the companion, 60% of those using an effect in a given talk. That is 1,800 watermark-visible talks a month at perhaps 20 viewers each, so 36,000 impressions. If 1% of viewers visit the site and 20% of those install, that is about 70 installs a month. Multiply every rate by three and it is still a few hundred, against thousands from store search. The rates are invented; the structure is the point.
4. **It does not reach professionals, who are the ones who pay.** Professionals see it, judge it as "trial software", and buy or not. Fine for conversion, irrelevant for spread.

What the watermark is good for: a steady trickle of highly qualified installs, brand familiarity in exactly the rooms where the next presenter sits, and the conversion lever for people who present in front of audiences that matter to them. Keep it; design it as a credit, not a nag.

Design rules (doc 08 has the wording): small, bottom corner, reads "anypresent.com", appears only while spotlight or magnifier is on, fades in and out with the effect, never pulses, never covers content, never appears on the phone. If it looks like a feature credit, students keep using it. If it looks like a trial nag, they stop using effects and you lose both the spread and the reason to pay.

Measure it: direct and organic visits to anypresent.com (distinct from store traffic), and a one-tap optional "How did you hear about us?" after the first successful session with "Saw it in someone's presentation" as an option. Decide by mid-2027 whether it deserves any further design effort.

## Channels, ranked by expected installs per hour of your time

| Rank | Channel | Expected effect | Effort | Confidence |
|---|---|---|---|---|
| 1 | App store search (ASO) on both stores | The majority of installs for the life of the product. Your old app got 46,000 installs from this alone with no help. | 2 to 3 days initially, then ongoing | High |
| 2 | Store listing and UI localization in 8 to 12 languages | Multiplies ASO; search is per storefront; LLM makes it nearly free | 2 to 3 days | High |
| 3 | The old Android listing's history | Updating in place keeps 46,000 installs' worth of history, existing users get an update notification, and the "Bluetooth Presenter" keyword history stays (doc 04) | 0 extra | Medium |
| 4 | Content on anypresent.com plus the web viewer page | Slow (6 to 12 months to rank), durable, intercepts hardware intent and "how to control slides from phone" queries | 1 day per article, 8 articles | Medium |
| 5 | Communities (Reddit, Hacker News, German teacher and student forums) | Launch-week spikes of hundreds to a few thousand installs, plus early ratings and bug reports | 2 days around launch | Medium |
| 6 | Short vertical video (TikTok, Reels, Shorts) | High variance: most clips do nothing, one in twenty may bring thousands. The gyro laser and spotlight are visually demonstrable | 10 to 15 clips over 8 weeks | Low to medium |
| 7 | Education outreach (university IT help pages, Hochschuldidaktik, teacher networks) | Slow, durable, high trust; a listing on a university help page is worth years of trickle | 2 days of emails, then follow-ups | Medium |
| 8 | Deal and code sites (MyDealz via a friend, Reddit code giveaways) | Spikes with mixed-quality users; Google caps promo codes at 500 a quarter, Apple allows far more | Hours | Low to medium |
| 9 | Product Hunt | A one-day spike, backlinks, credibility; mostly tech audience | 1 day | Low to medium |
| 10 | Roundup and review outreach ("best presentation remote" articles ignore apps) | Low hit rate per email, large payoff per hit | Hours per week for a month | Low |
| 11 | Paid ads with €200 | Roughly 100 to 300 installs once. Not worth it except as a keyword test | Skip | High |

## ASO, concretely

- **Apple title** (30 characters): keep the brand plus one keyword, for example "AnyPresent: Slide Remote". **Subtitle** (30 characters): "Clicker, laser & spotlight". **Keyword field** (100 characters): presenter, clicker, powerpoint, keynote, google slides, remote, pointer, bluetooth, presentation, control. Do not repeat words already in the title or subtitle; Apple indexes them once.
- **Google Play title** (30 characters) and short description (80 characters) carry the most weight; the full description should naturally contain the same terms several times.
- **Screenshots**: the first two must show the phone next to a laptop with the spotlight effect visible, because that is the thing nobody else shows. Third: "Nothing to install". Fourth: the gyro laser. Fifth: timer and black screen. A 15-second preview video of the gyro pointer and spotlight on both stores.
- **Ratings prompt**: after a session with at least five slide changes and three minutes, never during pairing, never after a failure. Reply to every negative review with a fix or a workaround; it is visible to the next thousand readers.
- **Localized listings** for at least: English, German, Spanish, French, Portuguese (Brazil), Italian, Turkish, Japanese, Korean, Simplified Chinese, Indonesian. Add languages that show up in your install data.
- **Compatibility content inside the listing**: "Works with PowerPoint, Keynote, Google Slides, PDF, Canva, Prezi" is both true (keyboard mode works with anything) and heavily searched.

## The education channel, concretely

- **Germany**: GDPR is the gate. Your no-account, no-tracking design is the pitch. Write a one-page German "Datenschutz und Technik" sheet: no account, no personal data, the relay carries only control messages and a random pairing code, nothing stored, where the servers are. Send it with a two-paragraph email to the e-learning or Hochschuldidaktik centre of twenty universities and ask to be listed next to Remote for Slides and Keynote Remote on their help pages. Teachers' networks (Lehrer-Online, the Twitterlehrerzimmer successors on Bluesky and Mastodon, eduki) take short posts with a video.
- **Schools**: the teacher's PC cannot be touched, so the web viewer (doc 06) is what makes AnyPresent usable in school. Until it exists, the keyboard mode on a school laptop is the story. Chromebooks accept Bluetooth keyboards, so US K-12 Chromebook rooms are covered by the keyboard mode and later by the viewer in Chrome.
- **Class and club codes**: a teacher or club gets a batch of Pro unlock codes for a term. On iOS these are Apple offer codes (one-time unlocks, generous quotas). On Android, Google's 500 codes a quarter cap means you should instead license the teacher's laptop through the companion (doc 04), which unlocks every phone that connects to it.
- **The tailwind to mention in outreach**: in-class presentations and oral exams are rising as a response to AI-written homework. More presentations, more presenters, more reason for a university to point students at a free, privacy-clean remote.

## Content and the website's role

anypresent.com should be three things: the download page for the companion, the web viewer (a tool page that ranks on its own), and eight to ten articles written for the queries people actually type. Suggested first articles: "Do you need a presentation clicker? Use your phone", "Logitech Spotlight alternative for €0", "How to control PowerPoint from your phone (Windows and Mac)", "How to control Google Slides from your phone", "Present a PDF from any browser with a phone remote", "Bluetooth presenter not connecting: the fix", "Presenting from a school or lecture-hall PC you cannot install on", and a compatibility page listing tested combinations. Put an Impressum and privacy page up from day one (doc 09).

## Short video plan

Ten to fifteen clips over eight weeks after launch, each under 20 seconds, phone in hand, laptop in frame, no talking required: the spotlight following the phone, the magnifier on a dense chart, "this is a €130 Spotlight, this is a free app", a fun pointer, the "nothing to install" pairing in 15 seconds. Post the same clip to TikTok, Reels and Shorts. Expect most to flop; the point is to find the one hook that works and then repeat it. Budget the time, not money.

## Launch plan

| When | What |
|---|---|
| October | Decide the stipend path (doc 07). ASO keyword research with store autocomplete. Website skeleton with Impressum and privacy page. |
| November | Submit a minimal iOS build for review with manual release to test acceptance of keyboard mode. TestFlight and Play closed testing with friends and a Reddit call for testers. Screenshots, preview video, localization. Microsoft Store and notarized Mac companion builds. |
| December | Soft launch (free tier only if the stipend path requires it): both stores live, no promotion. Fix what the first few hundred users break. Low-traffic month, good for catching bugs. |
| Mid-January | Launch push: Reddit (r/powerpoint, r/macapps, r/androidapps, r/iphone, r/teachers, r/professors, r/GradSchool, r/de and r/Studium for German), Hacker News "Show HN" (the HID trick and a Rust tray companion are HN material), Product Hunt, LinkedIn for the business angle, MyDealz via a friend with free Pro codes, German teacher communities. |
| February to March | Web viewer launch as its own mini-launch. Video experiment. University email round one. |
| April | 90-day review against doc 01's criteria. |

## What to do with €200

In order: a Windows code-signing solution if the Microsoft Store route does not cover direct downloads (doc 09), a decent screenshot template, a used Apple Watch when you reach that milestone. Not ads.

## Realistic install expectations

Month one after the launch push: 2,000 to 6,000 installs combined, mostly from spikes. Months two and three: whatever ASO sustains, which is the number that matters and which decides the 90-day review. See doc 01 for the scenarios.

## What I am not sure about

- **The watermark rates** in the arithmetic above are invented. Only the measurement plan is firm.
- **Short video** could be far better than I estimate; this category is unusually demonstrable in five seconds. It is the one channel where I would happily be wrong.
- **University help pages** move at university speed. Plan a six-month lag between the first email and the first listing.
- **Whether updating the old Android listing in place beats a fresh listing.** I think the history and the installed base win (medium confidence); a fresh listing wins only if the old rating drags and you cannot recover it with recency.
