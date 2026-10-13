# Data without tracking, feedback that matters, other features judged, and room-mode control for later

## The data question

"Count the requests" never meant analytics with identifiers. You already have four sources that cost nothing in privacy terms:

1. **The two store consoles.** Installs, uninstalls, crashes, countries, devices, OS versions, conversion to purchase, and on Google the retention curves. This is the funnel's top and bottom, free, with no code.
2. **Your own server.** The relay and the poll Worker already count sessions, pairings, voters and messages without any personal data. A daily aggregate of those counts is the "count the requests" for polls, by-code pairings and the web viewer. Add a counter for "viewer imported a PPTX" and "pairing by code started" if they are not there; they are counts, not people.
3. **TestFlight and Play testing feedback.** Both give testers a free-text box with screenshots. This is where "I could not find X" arrives before launch.
4. **Reviews.** Read every one; reply to every negative one.

Add two things, both voluntary and explicit:

5. **A feedback form** (a Google Form or a ten-line page on the Worker) linked from the post-talk screen and from settings, with three questions and a free-text box: what did you present with, what was missing, what nearly made you give up. Free text is the most valuable thing you will read in year one; read it weekly. Behind the "five talks, 50% off" banner it also seeds Pro purchases (file 06). A mailing list is optional; a one-line "may we email you when the companion gets slide info?" checkbox on the form is enough, with the privacy sentence next to it.
6. **The one-tap "how did you hear about us?"** on the post-talk screen, once, skippable. It is the only way to learn whether the credit on screen works.

What not to build: identifiers, sessions, cohorts, third-party analytics SDKs. If you ever want in-app counters ("effect used", "pairing failed on Windows"), send them without any identifier and declare "usage data, not linked to you" in the store labels; that is honest and teachers accept it. Not having them is also fine in year one, because the server counts and the form cover the decisions you actually face.

## Other features, judged

| Feature | Verdict | Why | When |
|---|---|---|---|
| Countdown and break screen on the big screen ("Back at 10:45", "5:00") | yes | trivial with the existing big-screen renderer, loved by teachers and trainers, nothing a clicker can do; add it as a screen mode | v1 |
| Group mode (several phones, one deck) | yes | your relay already survives concurrent pairings and hosts accept several Bluetooth keyboards; what remains is UX (a "whose turn" lock is optional). Student groups are your spread engine | v1 if cheap, else 1.1 |
| Timer and slide number overlay on the laptop's own screen (not the projector) | yes | a confidence monitor for people who have none; the companion already draws overlays | 1.1 |
| Timer starts on the first "next", log starts with it | yes | no setup, and with the Phase 2 integration it becomes automatic from the slideshow event | v1 |
| Pre-talk checklist (Do Not Disturb, brightness, battery) | yes, once | the WhatsApp banner mid-talk is the number one professional embarrassment | v1 |
| Ink and annotation from the phone | maybe | works over any content, but gyro drawing is shaky and touch drawing needs eyes on the phone; PowerPoint has a pen | Phase 2, only if asked |
| Hotkey-triggered effects without a phone | no | your reasoning: it makes a standalone-effects clone easy to compare against; add it only after a competitor tries | not planned |
| Live captions overlay | no | PowerPoint and Google Slides have them; Keynote and PDF are a Phase 3 accessibility case at most | not planned |
| Event mode | no | specialty software; zero focus unless someone asks | not planned |
| Audience slide following | never | discontinued by Apple and Microsoft for low usage, as you said | never |
| Slide thumbnails on the phone | never over Bluetooth | file 05 | never |
| Free-text answers and word clouds | later, with a filter, a host-side hide and a report link | file 03 | Phase 2 |
| Room mode for institutions | later | design the control expiry now so the Phase 3 build does not fight the Phase 1 protocol | Phase 3 |
| Accessibility | six basics now, VPAT later | below | v1 for the web pages |
| Watch | W1 only | agreed | v1 |
| Keyboard and mouse sibling's internet mode | Pro+ later, capped | file 06 | if asked |

## Room-mode control for later (so it is designed, not forgotten)

Your trolling case: a phone paired weeks ago in a lecture hall turns the screen black during someone else's lecture. Rules that prevent it, all cheap when the managed mode is built:

- Room pairings are session-scoped: a phone connects with the code shown on the room's screen or sticker, and the pairing expires after a fixed window (four hours) or when the next session starts, whichever comes first. Nothing persists on the phone for a room.
- Codes rotate per session, and the room shows the current one only when asked (a hotkey on the room PC or an idle screen), never permanently in a corner.
- One active presenter at a time holds the control token; a second phone must enter the current code, which the current presenter can see is happening ("another phone is asking for control").
- Screens (black, white, blur) opened by a phone close automatically when that phone disconnects or the session ends.
- The companion in managed mode has a "kick all" action and a log of connections (counts and times, no identities).

## Accessibility: the six basics now

For the voting page, the viewer and the web remote: real buttons with labels, visible focus, contrast at the AA level, tap targets of at least 44 pixels, no information carried by colour alone (your icon-based polls already do this), and a page that works with a screen reader's basic navigation. Doing this at the start is a day; retrofitting is a month. A VPAT document is written when an institution asks and nobody asks before Phase 3.

## What I am not sure about

- **Group mode's cost** depends on how the phone UI handles several controllers' state (whose black screen, whose pointer). If it is more than a few days, 1.1.
- **The countdown screen's typography** on old projectors, like the poll screen; same evening with a projector.
- **Whether a mailing list is worth its privacy paperwork** in year one; the form's checkbox is the minimum and may be all you need.
