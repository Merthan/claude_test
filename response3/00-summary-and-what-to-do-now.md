# Response 3 (30 October 2026): summary and what to do now

*Read in full: `prompt_30_10` and `features-and-state-2026-10-28.md` (682 lines). Checked online: the Berlin stipend batches and team rules, the Prototype Fund, NLnet's grants, Cloudflare's Workers Launchpad, GründungsBONUS Plus, Yoodli's pricing and pivot, Speeko, Toastmasters' Yoodli partnership, PowerPoint's Speaker Coach languages, the "AirPods as clicker" angle, and iOS per-app memory limits. Four sites could not be opened directly from this session (prototypefund.de, nlnet.nl, science-startups.berlin, cloudflare.com), so dates from those come from search summaries and are marked "confirm on the site". No existing file was edited; everything new is in `response3/`.*

## The verdict

You are done building version 1. You are not done with the product. The next ninety days are ship, fund and measure, not build. Three additions fit inside "polish" because they are small and they change what users see first: decoding during the talk so the report is ready when the talk ends, rehearsal memory (take-to-take comparison), and the countdown and Q&A screen kit. Everything else in this response is Phase 2 and should wait for real users and for the stipend decision. Confidence: high.

What the coach changed, and it changed more than I expected:

- **The centre of gravity for money and for institutions moved from the remote to the coach.** An on-device speech coach in eight languages that uploads nothing is the thing a German university can recommend to every student, and it is a product category with real willingness to pay (Speeko charges about $100 a year and is alive after eight years; Yoodli charges $8 to $20 a month and went enterprise). The remote stays the install engine; the coach is the reason to pay and the institutional story.
- **The stipend case is now strong.** A quantization recipe that matches the 305 MB reference at 155 MB, a decoder patch that reads filler probabilities without changing outputs, speaker turns in ggml with a custom op at 1.45% equal error rate, 10.9% word error rate on real talks on a phone at 19 times real time: those are measurable engineering results, which is what juries respond to. Doc 04.
- **"Too complex to copy" is now true against solo and LLM-assisted copiers.** Not against Microsoft or Apple, and it never will be; but they are English-first and tied to their slide tools. Doc 02.
- **A standalone coach app is the right second product,** ahead of the keyboard and mouse app, because the coach's audience is everyone who speaks, and a "presentation remote" listing will never rank for "public speaking practice". Doc 05.

## The ten decisions I would make this week

1. **Ship round 8** (English filler scan, speaker turns, word probability) if the Android build passes the identity check within a week; otherwise ship the readable build and bring round 8 in the first update. Doc 01.
2. **Post-take screen:** concept B "Coach's notes" as the main screen, concept C's problem reel as the interaction, concept E behind "Full analysis", no 0 to 100 score. Doc 01.
3. **Fillers for English only,** worded "Fillers: available for English talks", never a zero, never "beta". Doc 01.
4. **Decode during the talk, analyse at the end.** The engine already works in 20-second windows; feeding them as they arrive makes the report instant and removes the iOS background-processing problem. Doc 01 and 03.
5. **Gate the coach by memory and duration, deliver the model as a download, default to "only my voice is kept", show a one-time recording-consent notice.** Doc 01.
6. **Rehearsal memory** in v1 if it really is one to two days; otherwise the first update. Doc 03.
7. **Countdown, work-timer and Q&A screens** in v1 as a basic free set; packs later. Doc 06.
8. **Release free (no in-app purchases) in December, push in late January, price Pro and Pro+ in April with the stipend or in February without one.** Doc 04 and 07.
9. **This week, email three Berlin incubators** (team-size rule, Batch IV and V dates, whether a free release before the start matters), **re-approach the EXIST contact** with a one-page technical summary and a mentor from a speech or usability group, and **decide on the open-source question** (Prototype Fund, NLnet) by next week. Doc 04.
10. **Standalone coach app:** start in February, ship in March or April, cross-promoted. Doc 05.

## Direct answers to your prompt

- **"In theory mostly ready."** Agreed. The remaining risk is reliability across devices, not features: the three companion hardware tests from response 2, the coach's memory gate, and the iOS build of the speech library, which has never been compiled. Doc 07 has the order.
- **Polls redesign and on-screen timers.** Polls: the minimal set from `response2/03` (pulse check, correct-answer flag, numeric estimate, prepared questions) and nothing else. Timers: yes, as screens drawn by the companion and the viewer, with a plain countdown free and the kit in Pro. Doc 06.
- **Leaving the coach "at its current state".** Right call, with two exceptions that are not research: rehearsal memory (no model, all languages) and the slide-text synergy (names and terms from your deck become custom words; notes adherence; per-slide planned timing). Doc 03.
- **Standalone coach on the side.** Yes, second product, after the launch push. Doc 05.
- **What to hide on the phone.** Ship the findings your own reliability table calls good, hide the rest behind "Full analysis" or off, and put a thumbs-up or thumbs-down on each finding so the users tell you which to keep. Doc 01.
- **Different stipends because the pipeline is custom.** Yes: EXIST becomes defensible, Berlin's jury will see technology, and two open-source funders (Prototype Fund, NLnet) now fit if you are willing to open the library. Doc 04 has the trade-off; my lean is to apply if the window is open and you can live with the engine being public.
- **Market reassessment.** Two markets in one app; the coach raises willingness to pay and the institutional story; retention of coaching apps is episodic, so price for episodes. Doc 02.
- **"Why not just film yourself."** Because nobody films themselves five times, because the phone hears you from your hand, because the replay jumps to the moments and a video does not, and because nothing leaves the phone. Audio loses body language, which is the one thing a video adds; that is fine for the 80% of feedback that is pace, pauses, fillers and clarity. Doc 02.
- **"Too complex to copy."** True against solo copiers for six to twelve months; irrelevant against platforms; Mentimeter will not care. Doc 02.
- **Dumb Bluetooth gadgets as clickers.** Keep it and market it ("your earbuds are a clicker"). One competitor does AirPods on Mac only; you do it on Windows, Mac and the web. Mind the iOS audio-session rules: with the screen off the app needs an active audio session to receive media buttons, and your recording feature is the legitimate reason for it. Doc 02.
- **Screens as paid packs.** Yes, three packs at most plus singles, with the basics free. Doc 06.
- **More functionality, moonshots.** Ranked in doc 03. The one real moonshot that is now cheap is "get the notes": after a talk, the people who scanned your poll QR receive a cleaned recap of what you said per slide. Phase 3, with a privacy design.
- **No interviews, keep an in-app poll.** Fine. Toastmasters clubs and r/Toastmasters are the expert users you do not have in your life, and they will test the coach harder than any interview would. Doc 07.
- **"Only polish and I'm done?"** Done building, yes. Then ship, fund, measure.
- **Stipends with the April start and the EXIST comment.** Doc 04: the team-size rule at Science & Startups is the thing to settle this week, and a co-founder is not a cost under this programme, they bring their own €2,500 a month.

## Files

- `01-coach-ship-decisions.md`: every open decision in parts E1 to E3 answered, the screen, the gating, memory, download, licences, consent, languages, which findings ship.
- `02-market-reassessment.md`: the two markets, competitors with sources, differentiation, the video counterpoint, retention, revised numbers, copyability, the gadget angle.
- `03-moonshots-and-expansions.md`: ranked expansions with cost and value, the three that go into polish, the recap moonshot, what still not to build.
- `04-stipends-and-money-reassessed.md`: Berlin batches and the team rule, EXIST re-approached, the open-source funders and the trade-off, the smaller options, the sequencing of free versus priced.
- `05-standalone-coach-app.md`: why, when, naming, pricing, the cross-app purchase problem, the university angle.
- `06-monetization-update-and-screen-packs.md`: the catalogue with the coach, what is free in the coach, screen packs, passes, compliance notes.
- `07-six-week-launch-plan.md`: week by week to a December free release and a January push, with the beta channels and the stipend emails.
