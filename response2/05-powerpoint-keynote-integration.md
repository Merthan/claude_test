# Deeper PowerPoint and Keynote integration

## Verdict

Yes, in Phase 2, text only, capability-gated. It is the clearest reason a professional presenter picks AnyPresent over a €15 clicker beyond the effects, and it is the thing the desktop-app competitor sells. The confusion you fear is real and is solved by showing nothing where nothing is available, not by avoiding the feature.

## What it gives, and who cares

| Capability | Who cares | Transport cost |
|---|---|---|
| Slide number and total ("12 of 40") on the phone and watch | everyone who has ever lost their place | a few bytes |
| Title of the upcoming slide ("Next: Q4 results") | lecturers, trainers, anyone with 60 slides | tens of bytes |
| Notes text for the current slide, as a glance, not a teleprompter | the "I forgot the number" moment you described | up to a few hundred bytes, prefetched for the next slide |
| Jump to slide by number | lecturers answering a question from slide 7 | one command |
| Slideshow started and ended events | everyone: the timer and the presentation log start and stop themselves, and the end-of-show summary appears without a tap | one event each |
| Which application is presenting | the companion's own status, and your support inbox | one string |

Not worth it: thumbnails (you are right, never over Bluetooth, and little value on a phone you are not looking at), animation counters ("Animation 3 of 4" is cute and confusing), anything that changes the slides.

## The confusion problem and how to defuse it

Your worry: "Why does it not work in Google Slides?", "It worked last time in PowerPoint, why not now in the browser?". Four rules make this a non-issue, and they are how every app with app-specific features behaves:

1. **Nothing is shown unless the companion reports the capability.** The phone has no empty "Slide ? of ?" panel. When PowerPoint or Keynote is detected, the slide line appears; otherwise the presenter screen looks exactly as it does today.
2. **The companion names what it sees.** Its status, mirrored on the phone's connection card, reads "PowerPoint detected: slide info on", "Keynote detected: slide info on", or "Other app: basic control". People understand "other app" immediately.
3. **One line in the compatibility page and the FAQ:** "Slide numbers, titles and notes work with PowerPoint and Keynote on the desktop. Google Slides, PowerPoint in the browser and PDF viewers do not expose this, so you get the full remote and effects without slide info."
4. **The basic controls never change.** Next, previous, screens, effects and polls behave identically in every app. Slide info is an addition that appears and disappears, never a mode.

PPTControl and Keynote Remote live on exactly this boundary and nobody reviews them badly for it.

## Cost and permissions

- **Windows:** PowerPoint's automation interface from the tray process (same user, no admin): the current show position, the slide's notes text, go-to-slide, and the slideshow begin and end events. Edge cases to budget: presenter view with two windows, protected view documents, two presentations open, PowerPoint not yet running when the companion starts. About a week for a solid first version, with the edge cases, plus testing across Office 2019, 2021 and Microsoft 365.
- **macOS:** Keynote and PowerPoint are both scriptable; Keynote exposes the current slide of a playing document and its presenter notes, and PowerPoint for Mac exposes the slide show view. Each app triggers one Automation prompt ("AnyPresent wants to control Keynote") the first time; that is a normal prompt and far less alarming than Input Monitoring. PowerPoint for Mac's scripting has historically been patchier than Keynote's; budget an extra few days for it.
- **Google Slides, PowerPoint for the web, PDF viewers:** nothing reliable without a browser extension. Say so and move on. The website viewer already knows its own page number and can send `slide.state` as designed, so the viewer path gets slide numbers for free.

## Transport

- Over the relay and the direct link: trivial, the messages exist (APP messages, CHUNK for anything larger).
- Over Bluetooth: HID output reports, which is Test 2 in file 01. Keep payloads small (slide number, a short title, notes capped at about a kilobyte, prefetched one slide ahead) so they fit the report size without a streaming layer. If output reports fail on a host, slide info simply does not appear on that host, which the capability rule already handles.

## When

Phase 2, after the push, as the headline of the Pro+ launch together with the transcript. Build Windows PowerPoint first (the largest user group), Keynote second, PowerPoint for Mac third.

## What I am not sure about

- **PowerPoint for Mac scripting reliability** across versions; it may need a fallback to "detected, but slide info unavailable" on some builds.
- **Whether the notes glance is used enough** to justify the prefetch logic; ship slide numbers and the upcoming title first, add notes if the log shows people looking at the phone between slides.
