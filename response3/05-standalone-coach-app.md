# The standalone coach app

## Short answer

Yes, as the second product, ahead of the keyboard and mouse app, started in February and shipped in March or April after the launch push. The reason is store search: the people who need a speech coach search for "public speaking practice", "presentation practice", "filler words" and "interview practice", and a listing called "presentation remote" will never rank for any of them. The library is done, the screens are designed, and the standalone app is mostly a container, a listing and a pricing decision. Confidence: high on "yes", medium on the timing.

## Why a second app rather than the coach inside AnyPresent only

- **Category.** App stores rank within categories and keywords. The coach's audience is anyone who speaks in front of people: students before every presentation, job seekers, non-native speakers, sales and consulting staff, Toastmasters members, lecturers. Few of them will find a coach inside a clicker app.
- **Pricing freedom.** A coach app can run a yearly plan and an event pass without touching the remote's one-time Pro.
- **Institutions.** "Recommend this rehearsal coach to your students" is the sentence a university can act on; "install this clicker app which also has a coach" is not.
- **The stipend story.** One company, a product family built on one on-device speech core: the remote, the coach, later the keyboard and mouse app. Juries like a family more than a feature.

Keep the full coach inside AnyPresent as well. The remote's users get it as the Pro+ reason, and the real-talk recording (what you actually said per slide, with the Q&A) only exists there.

## What the standalone app contains

The same library and the same screens: the takes list under named talks, the context question (presentation, lecture, meeting, interview), the Coach's notes screen with the reel, rehearsal memory, words to practise, custom words, the deck import once it exists (share a PDF into the app), exports and the report card, the server corrections and improvements as opt-in. No remote, no companion, no polls. A "practise 90 seconds" daily prompt can come later; do not ship it first.

## Naming

The coach serves interviews and meetings too, so "AnyPresent Coach" is slightly off, but it carries the brand, the publisher, and the cross-promotion, and juries see a family. Two directions:

- **Family name:** "AnyPresent Coach: Speech Practice". Cheapest, consistent, slightly awkward for interview users.
- **Sibling name under the same publisher:** a short word for rehearsal or clarity, with "from the makers of AnyPresent" in the description. Better for the category, one more trademark check, one more brand to explain.

I would take the family name now; renaming later is painful for store equity, but the brand consolidation is worth more in year one than the slight awkwardness. Decide once, check the trademark registers once.

## Apple's duplicate-app rule

Rule 4.3 targets near-identical apps. A clicker with a coach and a coach without a clicker, with different icons, names, screenshots and descriptions, are different products that share a library, which is normal. Do not make the coach app a stripped AnyPresent; make it the coach, fully.

## Pricing (placeholders; doc 06 has the catalogue)

- Free: pace, pauses, pitch and volume, clarity moments, the reel of the three biggest moments, English fillers, the last three takes.
- Coach Pro: €24.99 a year, €79 lifetime, Event pass €2.99 for seven days. Includes unlimited takes and history, rehearsal memory, speaker turns and "keep all speakers", words to practise and custom words, deck import, exports, server improvements.
- Keep the same tier names and prices as Pro+ in AnyPresent so a person who sees both is not confused.

## The cross-app purchase problem

Purchases do not transfer between two apps on either store, and a subscription group cannot span apps. So a Pro+ buyer in AnyPresent would have to buy again in the coach app, and the other way round. Two options:

1. Accept it for the first months. The overlap of people who want both is small, and support can hand out offer codes to the few who complain.
2. Build the optional email link from `response-monetization-accounts-and-free.md` before the coach app ships: a purchase in either app can be linked to an email, and the other app honours it. This is the first concrete reason to build that link; a few days on the Worker.

I would do option 1 at the coach app's launch and option 2 within the following quarter, because the same link also solves platform switching and business seats.

## Channels for the coach app

- **Toastmasters clubs.** HQ partners with Yoodli, but clubs choose their own tools and the "Ah-Counter" role is your feature done by hand every week. Two or three Berlin clubs as beta testers, then r/Toastmasters and district newsletters with a free-forever core and a privacy sentence.
- **Universities.** Hochschuldidaktik centres, writing and speaking centres, career services and language centres. The pitch: every student can rehearse privately on their own phone, in eight languages, with nothing uploaded; a GDPR one-pager; a campus licence (Pro for all students) in year two. This is a more natural institutional sale than room mode for the remote, and the two can be pitched together later.
- **Reddit and communities:** r/PublicSpeaking, r/GradSchool (thesis defences), r/languagelearning (carefully: clarity, not pronunciation), r/consulting and r/cscareerquestions (interview answers).
- **Content:** "how to stop saying um" in eight languages is a search term with volume in every one of them; the articles write themselves from your own findings list.

## Metrics that mean something for a coach

Not daily active users. Takes per talk (are people rehearsing more than once), return before the next event (did they come back within 90 days), purchases per event, and the per-finding thumbs. A coach that is opened four times a year by someone who presents four times a year is working.

## What I am not sure about

- **Timing.** February is right if the January push does not generate a support load that eats the month; if it does, March.
- **The family name** is a judgement; a sibling name might rank marginally better for interview and language users, at the cost of a second brand.
- **University licences** are plausible and unproven; the first two conversations decide whether this is a year-one or a year-two revenue line.
