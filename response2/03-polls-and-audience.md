# Polls and the audience layer

## Verdict

Include polls in v1, limited and account-free, and position them as "the fastest way to ask the room a question during any presentation", not as a Mentimeter replacement. The position is real: every incumbent needs a presenter account and preparation inside its own tool or add-in, and their free tiers are stingy. Your version needs no account on either side, starts from the phone in five seconds, and draws over whatever is on screen. That is a selling point, a deterrent, and a good application slide. The risk is not Mentimeter; it is scope creep. Keep to the list below and stop.

## Market position

| | Presenter account | Preparation | Works over any content | Free tier (as reported in 2026) |
|---|---|---|---|---|
| Mentimeter | required | slides built in Menti or an add-in | no | 50 participants a month across the whole account, plus one unlimited session a month |
| Slido | required | questions prepared in Slido or an add-in | via PowerPoint, Google Slides, Teams, Webex add-ins | 100 participants an event, three polls and one quiz |
| Poll Everywhere | required | prepared | embeds in PowerPoint, Keynote, Google Slides | 40 participants |
| Kahoot | required | prepared quiz sets | no | limited free for teachers |
| Google Slides audience Q&A (from memory; verify) | Google account | none | Google Slides only | free, questions only |
| PowerPoint with Microsoft Forms (from memory; verify) | Microsoft 365 | prepared form | PowerPoint only | included in 365 |
| German university tools (Particify, frag.jetzt, Pingo) | varies | prepared | no | free |
| **AnyPresent** | none | none for ad-hoc polls | yes, including PDFs, browsers, drawing boards | unlimited polls; audience size metered later |

Where you win: spontaneous questions ("quick, who agrees?"), lecturers who will not create an account for a once-a-week check, schools where student data is a problem (your voters are anonymous browser sessions), and anyone presenting from a PDF or a browser where the add-ins do not exist. Where you do not win and should not try: designed interactive decks, word clouds with moderation, team quizzes with leaderboards and music, analytics dashboards. Mentimeter is not going to notice you, and that is fine.

A note on Mentimeter's 50 a month: a lecturer with 200 students cannot use free Mentimeter at all. In the launch phase, an unlimited audience is a concrete reason for exactly those lecturers to try you, and they are the people who later pay for Pro+ or whose institution pays for room mode.

## What exists and what to add for v1

Exists (per the context): yes/no, single choice, multi-select, rating, reactions; a join screen with QR, code and live counter; hidden results with a "who voted" ring; live bars; closed state; final reveal; three chart styles; four themes; voting page in English and German; the companion joins from a link or over Bluetooth.

Add for v1, in this order:

1. **Pulse check.** A poll that stays open: "too fast / fine / too slow" or a 1 to 5 "do you follow?" with a live average, shown as a small corner widget instead of a full screen, so the lecture continues while it runs. It is the lecturer's killer feature, it needs no question text, and it is the same Durable Object with a different render. Pace checks are the most common reason teachers reach for these tools at all.
2. **Correct-answer flag** on single and multi choice: the presenter marks the right option on the phone; the reveal highlights it. No points yet. This is the cheapest version of "quiz" and most of what teachers want.
3. **Numeric estimate.** Voters type a number; the screen shows a histogram and the median. Fun in classrooms ("how many litres?"), and it is numeric input only, so there is nothing to moderate.
4. **Prepared questions on the phone.** A list where the presenter types up to a handful of questions before the talk and launches each with one tap. Local storage, no website editor, no sync. It turns "ad-hoc only" into "lightly prepared" for nearly no code.
5. **Results on the voters' phones after the reveal.** Standard, cheap, and voters expect it. This is not slide following; it is the result of the thing they just did.
6. **"Show the join screen again" and "End audience session"** as actions on the phone. People arrive late; spontaneous polls happen an hour in.
7. **Voting page in about ten languages** via the same localization pass as the app. The page is public and the audience is anyone.
8. **The six accessibility basics on the voting page** (file 07). It is the one surface strangers with disabilities will use.

## What to defer and why

- **Free text and word clouds** (Phase 2): the most popular Mentimeter feature, and the one that needs a profanity filter, a host-side "hide" button, a report link on the voting page, and the app-store user-generated-content rules once answers appear inside the phone app. Add it with those three pieces, not before.
- **Quiz sets with points, leaderboard and nicknames** (Phase 2): Kahoot's loop. When you add it, generate nicknames (colour plus animal) instead of letting people type them; that is how Kahoot avoids moderation, and it keeps the voting page free of text input.
- **Audience questions with upvotes** (Phase 2 or later): free text again.
- **Exports** (Pro+): CSV of results after the talk.
- **Images in questions, teams, timers per question:** not in year one.

## Design rules

- One join per talk, as designed. The QR must be re-showable at any time.
- The companion renders the big screen; the website viewer renders the same polls in its own page (it takes the companion role already), so the browser path is not a lesser experience for audiences. The web page may use emoji; the companion uses icons; that is fine.
- Anti-abuse is in place (rate limits, TTL, browser-id vote-once). Add "clear and reopen" for the presenter and a hard cap on voters per session that the free tier later meters.
- No presenter account, no voter account, no personal data. Say this on the voting page footer in one line; teachers read footers.
- Big-screen typography for the back of a room on a 1024 by 768 projector: question in the largest type the screen allows, bars thick, no colour-only coding (the icons already do this).

## Metering and tiers

Launch phase: unlimited polls and unlimited audience, with the Pro+ badge visible on "audience over 50" and "exports" from day one, labelled "free during the launch phase". When Pro+ is priced: free keeps unlimited polls up to 50 voters per session (more generous than any incumbent's free tier and enough for every school class and seminar), Pro+ removes the cap and adds exports, prepared sets, quiz mode and themes. Lecture halls with 200 students are professionals or institutions, which is the point of the cap. The cost side is irrelevant: a vote is a twentieth of a request, and a session of 200 voters and five polls is about 50 requests.

## The stop list

Do not build in year one: word clouds without the three moderation pieces, leaderboards with typed names, per-question timers, image answers, team modes, a web editor for question sets, result analytics across talks, integrations with slide tools, or any "audience sees the slides" feature. Each is a month, and none moves installs.

## What I am not sure about

- **How many presenters will use polls at all.** My guess is 10 to 20 percent of active presenters try one and 5 percent use them regularly, mostly teachers and lecturers. That is enough to justify the feature as built; it is not enough to justify the stop list being broken.
- **The 50-voter free cap** is a guess at the line between "class" and "lecture hall". Adjust it with the first semester's data from your own server counts.
- **Google Slides Q&A and PowerPoint Forms details** are from memory; verify before quoting them anywhere.

## Sources checked

- Mentimeter free plan details (September 2026 write-up): https://www.productcompass.pm/p/mentimeter-free-plan
- Slido, Mentimeter and Poll Everywhere free tiers as compared by third parties in 2026: https://www.koji.so/blog/best-slido-alternatives-2026 and https://ahaslides.com/cy/blog/free-online-polling/ and https://meetergo.com/en/magazine/mentimeter-alternatives
