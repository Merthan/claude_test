# Market reassessment with the coach

## Short answer

You now have two products in one app. The remote and effects are the install engine in a small niche. The coach is a product in a larger category (public speaking practice, interview preparation, speaking in a second language) with real willingness to pay, a known retention problem, strong free competitors in English, and a gap in exactly your position: on-device, no upload, eight languages, works with any slides or none, on a phone. Adding the coach does not make the remote worse; it changes who pays and what institutions can recommend. The honest ceiling is still an indie business, now with a plausible path to €3,000 to €6,000 a month across two apps and a few university pilots rather than €1,000 to €3,000 from the remote alone. Confidence: medium.

## The competitors that matter for the coach

| | What it is | Price | Languages | Where it runs | What this means for you |
|---|---|---|---|---|---|
| PowerPoint Speaker Coach (Microsoft) | Rehearsal coach inside PowerPoint: pace, pitch, fillers, originality, repetition, inclusiveness | free with Microsoft 365 | English-speaking markets confirmed; Spanish, French and Japanese announced as "in progress" on an undated page; the Teams version is English only | PowerPoint desktop and mobile | For English PowerPoint users it is the incumbent and free. Your edge: any slides or none, seven more languages for pace and pauses, the replay of moments, speaker turns, the phone in your hand, nothing uploaded |
| Yoodli | AI speech coach, video and audio, cloud analysis; pivoted hard to enterprise sales enablement and interview roleplays | free (5 lifetime roleplays), Pro about $8 a month annually, Advanced about $20; enterprise custom | English-first | web, desktop | Proof that consumers pay for this and that the consumer business alone did not satisfy a venture-funded company. It is the official Toastmasters partner since December 2022 (free to members: transcripts, fillers, pacing, 60 minutes of storage) |
| Speeko | iOS speech coach, since 2018 | about $25 a month or $100 a year; "main features free forever" | English-first | iPhone | Proof that an indie coaching app survives eight years at a $100 price point |
| Orai | 2017 university spin-off, filler and pace feedback | free in its day | English | phone | No 2026 signal found; from memory it wound down (verify). The lesson is retention, not demand |
| Toastmasters' own practice | human evaluators, the "Ah-Counter" role that counts fillers by hand | membership | any | clubs | Your exact feature set, done by humans weekly in 14,000 clubs. The clubs are your expert testers and evangelists even though HQ partners with Yoodli |

Sources are listed at the end.

## Where the coach is different, in the order that matters to buyers

1. **Nothing leaves the phone.** Every competitor above analyses in the cloud (Speaker Coach runs on Microsoft's services; Yoodli uploads video). For students, for anyone rehearsing a confidential pitch, and for every German institution that would like to recommend a tool, this is the deciding property. It is also why your cost per user is zero, so the free tier can be generous.
2. **Eight languages for pace, pauses, pitch, volume and clarity.** Speaker Coach and Yoodli are English-first. Fillers stay English-only on your side too, and you say so; the other signals are the ones a German, French or Polish student actually gets nowhere else on a phone.
3. **Works with any slides or none.** Keynote, Google Slides, a PDF, a wedding speech, an interview answer. Speaker Coach needs PowerPoint; Yoodli needs you at a computer.
4. **The replay of moments.** "Autoplay the worst parts" with a lead-in and a live transcript is the feature people will show each other. Video tools make you scrub.
5. **Real talks, not just rehearsals.** When the remote is in use, the same recording gives you what you actually said per slide, the Q&A with speaker turns, and the comparison with the rehearsal. Nobody else can do this because nobody else is also the clicker.
6. **Rehearsal memory.** Take-to-take comparison by word alignment ("you skipped pricing again") turns one-off feedback into practice. Phase 2 at the latest.

## "Why not just make a video of yourself?"

The counterpoint is right about one thing: a video shows body language, and audio does not. For everything else it is wrong in practice:

- People do not film themselves five times before a talk; they rehearse in a kitchen, on a walk, in a library. A phone in the hand records those; a tripod does not.
- A video gives you an hour of yourself to scrub through. The coach gives you the twelve moments that matter, with the transcript, in two minutes.
- A video of your face in a cloud service is the thing students and professionals least want to exist. On-device audio is the opposite.
- The signals people actually fix (pace, pauses, fillers, trailing off, unclear passages, time per slide) are audio signals. Posture and gaze are real but are coached well by one human comment and poorly by software.

So: not "instead of video" but "the thing you will actually do five times".

## Retention, honestly

Coaching apps have episodic use: people rehearse before a thesis defence, a job interview, a conference, then stop. Yoodli's enterprise pivot and Orai's fade both say this. For you it means:

- Price for episodes: a one-time purchase, a seven-day pass for the big event, and a yearly plan only for people who present for a living. Doc 06.
- Build the reasons to come back that cost nothing: the takes list with its history, rehearsal memory, the real-talk recording through the remote, and in the standalone app a "practise 90 seconds" habit loop later.
- Do not measure the coach by daily use; measure it by "came back before the next event" and by purchases per event.

## Revised numbers

Everything in `docs/01` and the expectation column of `response-directions-and-ambition.md` still holds for the remote. The coach changes three things:

| | Without the coach | With the coach in the app | Plus the standalone coach app (doc 05) |
|---|---|---|---|
| Installs | ASO-driven, unchanged | slightly up (new keywords: "rehearse", "practice presentation") | a second funnel in a larger category; my guess is 30 to 100% of the remote's install volume within a year |
| Paid conversion and price | Pro once, about 2% | Pro+ now has a reason; conversion to any payment 2.5 to 4% at a higher average | subscription-friendly for professionals; passes for events |
| Institutions | room mode, slow sales | "a privacy-clean rehearsal coach for every student" is a recommendation a Hochschuldidaktik centre can make this semester, and a site licence they can justify | the same, with the coach as the product they actually license |
| Month-12 run rate, my expectation | €2,000 to €4,000 a month (previous estimate) | €2,500 to €5,000 a month | €3,000 to €6,000 a month across both apps, plus 0 to 3 university pilots at €0 to €3,000 each |

These are still indie numbers. The stipend remains the dominant year-one income, which is why doc 04 matters more than this one.

## Copyability, reassessed

- **A solo developer with an LLM:** cannot reproduce the coach in a weekend or a month. The quantization and its evaluation infrastructure, the decoder patches, the calibrated analytics, the speaker model with a custom op, the obfuscation, and the test corpus are months of specialised work. Expect six to twelve months of lead, which is enough.
- **Mentimeter, Slido, Kahoot:** different product; they will not. The polls in your app are an add-on, not a threat to them, and that is fine.
- **Microsoft:** already has an English coach inside PowerPoint and may add languages. It will never be on-device on a phone with any slides.
- **Apple:** could add a rehearsal coach to Keynote on top of the iOS 26 speech APIs within a year or two. If it does, it will be Keynote-only and Apple-languages-only; your remaining niche is everything else. This is the one platform risk worth a line in the stipend application's risk section.
- **Yoodli and the like:** could add on-device processing; their business is enterprise video roleplays now, so they will not optimise for a 155 MB phone model.

Your wish to "seem too complex to copy" is therefore met for the people it can be met for. The complexity has a cost on your side too: support surface, test matrix, build pipeline. Keep the identity tests and the obfuscation gate automated so the complexity stays yours and not your weekends'.

## The gadget angle (earbuds, headphones, watches as clickers)

Keep it and market it. The facts: Microsoft supports Surface Earbuds gestures in PowerPoint; one iPhone app (Air Presentation) sells AirPods support as an in-app purchase and needs its own Mac companion; a Slidev add-on maps earbud taps to slides in the browser. Nobody does it across Windows, Mac and the web with an internet backup, and nobody markets it to students. The hook is "your AirPods are a clicker" and "any Bluetooth media button, including your watch's music controls".

Two cautions: on iOS, receiving media-button presses with the screen off requires an active audio session, and the stores dislike silent audio played only to stay alive; your recording feature is the legitimate reason for the session when it is on, and when it is off, keep the session to the duration of a talk and explain it in the review notes. On the web, media keys need the page to be "playing" something, which is why the Slidev add-on asks for a click first; the viewer can do the same.

## What I am not sure about

- **The coach's install contribution** is a guess; the standalone app's funnel in a bigger category is the part I would bet on, not keyword spillover inside the remote's listing.
- **Speaker Coach's current languages**; the Microsoft page is undated. If Spanish, French and Japanese shipped, your language edge is smaller in those three and unchanged in German, Italian, Dutch, Polish and Portuguese.
- **Orai's status** is from memory.
- **University pilots** are plausible, not evidenced; the first two conversations will tell you whether "recommend to students" is a six-week or a six-month decision at a German university.

## Sources checked

- PowerPoint Speaker Coach (languages, feedback categories): https://support.microsoft.com/en-us/topic/cd7fc941-5c3b-498c-a225-83ef3f64f07b and the Teams version: https://snhu-accessibility.screenstepslive.com/a/1677102-microsoft-teams-speaker-coach
- Yoodli pricing and enterprise focus (third-party reviews, 2026): https://www.outdoo.ai/blog/yoodli-review-and-pricing and https://www.finalroundai.com/blog/what-is-yoodli
- Toastmasters and Yoodli partnership: https://www.toastmasters.org/about/partnerships-collaborations/yoodli and https://www.geekwire.com/2022/toastmasters-adopts-ai-powered-speech-analytics-technology-from-seattle-startup-yoodli/
- Speeko pricing: https://speeko.co/subscriptions and https://apppricinglab.com/iap/apple/1071468459
- Orai background: https://venturebeat.com/ai/orai-app-uses-ai-to-help-you-become-a-better-public-speaker
- AirPods and earbuds as clickers: https://support.microsoft.com/en-us/office/use-the-surface-earbuds-in-your-presentation-6319a6f3-ad69-44e6-a8ff-e79676423e4a and https://mwm.ai/apps/air-presentatation-ppt-remote/1294122699 and https://awesome.ecosyste.ms/projects/github.com%2Fice-hazymoon%2Fslidev-addon-slidepods
- iOS per-app memory on 4 GB phones: https://developer.apple.com/forums/thread/688973 and https://developer.apple.com/forums/thread/834805
