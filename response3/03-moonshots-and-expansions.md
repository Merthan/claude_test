# Moonshots and expansions, ranked

## Short answer

Three things go into the polish month because they are small and change what users see first: decoding during the talk, rehearsal memory, and the screen kit. Four things are Phase 2 and build on what you already have: the deck's text feeding the coach, Q&A capture with a searchable archive, the LLM server doing more than corrections, and shareable report cards. One real moonshot became cheap because of the coach and the poll sessions together: "get the notes", where the people who scanned your QR receive a cleaned recap of your talk afterwards. Two things stay off: live cues during a real talk, and live captions. Confidence: high on the ranking, medium on the effort estimates.

## The ranked list

| Rank | Expansion | What it is | Value | Effort | When |
|---|---|---|---|---|---|
| 1 | Decode during the talk | Feed the engine's 20-second windows as they are recorded; analytics at the end | instant report; no iOS background problem; enables everything live later | days, mostly plumbing | polish |
| 2 | Rehearsal memory | Compare takes of the same talk by word alignment: shorter or longer, skipped passages, repeated hesitation spots, before and after playback | the reason to rehearse more than once; all languages; no model | 1 to 2 days prototype, a few more for the phone UI | polish or first update |
| 3 | Screen kit | Countdown and work timer with custom text, "Q&A time", "Back at 10:45", drawn by the companion and the viewer | teachers and trainers; nothing a clicker can do; also a pack to sell | days | polish |
| 4 | The deck feeds the coach | Import the PDF (share sheet) or read slide text through the viewer or the PowerPoint and Keynote integration: names and terms become custom words automatically; per-slide planned timing; notes adherence ("you skipped slide 7's point"); reading-your-slides detection | "rehearse with your actual deck", which nobody has outside PowerPoint; better transcripts of your own jargon for free | 1 to 2 weeks | Phase 2 |
| 5 | Q&A capture and the talk archive | With speaker turns: the questions you got, as a list; every talk and rehearsal searchable on the phone ("what did I say about X in lecture 3") | lecturers and trainers; sticky; private | a week | Phase 2 |
| 6 | The server does more than corrections | Per-slide summary, suggested rewrites of unclear passages, "questions your audience might ask", a translation of the recap; text only, opt-in | the "AI" line without a model on the phone; Pro+ value | days per feature | Phase 2 |
| 7 | Shareable report card | The winlab report card as an image: "5 rehearsals, pace 142, fillers down 60%" | social proof and a reason to post; costs nothing | 1 to 2 days | Phase 2 |
| 8 | "Get the notes" (the moonshot) | After the talk, the presenter taps "share the recap"; everyone who scanned the poll QR gets a cleaned, per-slide recap of the main speaker's words for 48 hours | every attendee gets a reason to scan; lecturers' students love recaps; conference speakers get a lead magnet | 2 to 3 weeks; a server rule change | Phase 3 |
| 9 | Meeting and interview modes | Record a meeting and get your share, pace and fillers; answer interview questions and get feedback; both exist in the library's capabilities | broadens the standalone coach into Yoodli's and Poised's territory, on-device | weeks of UX | standalone app, Phase 3 |
| 10 | Clarity practice for language learners | "Words the recognizer could not catch" is a soft pronunciation signal (about 70% of flagged words are real misses); framed as clarity, never as a pronunciation score | a much larger market; careful claims | weeks | standalone app, Phase 3, only with the framing rules |
| 11 | Live pace cue on the phone | A quiet haptic when the 30-second pace runs above the band during a real talk | some presenters want it; most should not be distracted | days once decoding is live | Phase 3 experiment, opt-in |
| 12 | Live captions on the projector | Phone decodes, companion overlays text | accessibility for institutions; eight languages; on-device | windows of 20 s are too slow; smaller windows cost accuracy | not now; revisit only if an institution asks |

## The three that go into polish

**Decoding during the talk.** Already argued in doc 01. One extra reason: it is the foundation for ranks 8, 11 and 12 and for anything on the watch; building it now while you know the engine is cheaper than in March.

**Rehearsal memory.** The pieces exist (notes alignment, progress page, change since last take, goal check). The product rule: takes belong to a named talk; from the second take the comparison appears without being asked; the comparison is three sentences and two reels (then and now), not a table. Keep it free for the second take and Pro+ from the third, or free throughout in the launch phase.

**The screen kit.** The companion renders full-screen views already; a countdown with custom text, a work timer that ends with a chime and returns to the slides, a "Q&A" screen with the floating question marks you mentioned, and a "Back at" screen are a day each. They are also the first thing a teacher will show a colleague.

## The moonshot, designed so it does not break your rules

"Get the notes" conflicts with two things you wrote: the speech server's rule ("an optional correction helper, no content features") and your dislike of participants on their phones during a talk. Both are solvable:

- It happens after the talk, never during. The audience's phones are not involved while you speak.
- Only the main speaker's words are included (round 8's default), so audience questions never leave the room.
- The presenter chooses, per talk, with a preview. Nothing is shared by default.
- The recap lives on the server for 48 hours under the session code, then is deleted. No accounts on either side; the attendee's browser already has the session's random id from the poll join.
- The cleanup is the server's existing LLM path on text; the per-slide structure comes from the slide times the phone already has.

Why it is the moonshot: it converts the poll join, which few people will use, into "scan to get the notes", which most lecture audiences will use, and every attendee sees your name on a page they keep. It is the growth loop the watermark never was. Why Phase 3: it needs the session plumbing, a share page, an expiry policy, and a careful privacy text, and it should wait until the coach and polls have real users.

## What still not to build

- Live cues during a real talk as a default. Opt-in experiment at most.
- Live captions, for the latency reason above.
- A 0 to 100 score. Three numbers and levels.
- Pronunciation scoring. Clarity, carefully worded, is the most you can honestly claim.
- Hotkey-triggered effects without a phone (your reason stands).
- Audience slide-following during the talk (yours and mine agree).
- Any feature that needs audio to leave the phone.

## What I am not sure about

- **Effort estimates** are mine, not measurements; the deck-feeds-the-coach item can grow if PDF text extraction on the phone fights with your deck formats.
- **"Get the notes" demand** is inferred from how lecture audiences behave, not measured; the first semester with polls will show how many scan the QR at all.
- **Clarity practice for learners** is the most valuable and the most dangerous item on the list: the claim must stay "words the recognizer could not catch", or one review from a linguist ends it.
