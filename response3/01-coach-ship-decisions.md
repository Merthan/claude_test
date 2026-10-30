# The coach: every open decision, answered

*Based on parts E1 to E3 and F of `features-and-state-2026-10-28.md`. I take the measured numbers in that document as given.*

## Short answer

Ship round 8 if its Android build passes the identity check within a week, show the "Coach's notes" screen with the problem reel as the main interaction, gate fillers to English and gate the whole coach by phone memory, decode during the talk so the report is ready when the talk ends, keep only the main speaker's words by default, and ship the findings your own reliability table rates as good. Everything below is the detail and the reasons.

## E1: the eleven new decisions

| # | Decision | My answer | Why |
|---|---|---|---|
| 1 | Post-take screen | **B "Coach's notes" as the main screen**, with concept C's problem reel as the primary interaction inside it; **A "Snapshot"** as the card in the takes list; **E "Full analysis"** behind a "Details" button; **D's score and radar not shown** | Praise, one thing to work on, praise is how coaching works and how people accept criticism. A 0 to 100 score built from sub-signals you yourself rate as noisy (uptalk, trailing off, repetitions at 7% recall) will be wrong often enough that users argue with it instead of practising. Three headline numbers with a trend (pace, deliberate pauses, fillers where available) are honest and still satisfying |
| 2 | Fix `words[].e` | **Fix in the library before shipping** | Decode unchanged, only end times change, and it removes the filler-at-sentence-end artefact you noticed in your own app |
| 3 | Ship round 8 | **Yes, if the Android build and the identity check pass within one week** of starting; otherwise ship the readable build (octave fix, custom words) and bring round 8 in the first update | The English filler scan (72% found instead of 38%) is the single largest quality jump in your largest market; speaker turns are what make real talks with Q&A and meetings usable. The cost (+30% analysis time, +3.75 MB) is fine. The iOS build is unknown either way (the Swift bridge has never been compiled), so the iOS coach may ship a few weeks after Android; do not hold the iOS remote for it |
| 4 | Voice model delivery | **Download, plain** | A public, attributed model; encrypting it buys nothing |
| 5 | VoxCeleb grey zone | **Accept for the consumer launch with attribution; switch to CAM++ before any institutional or business sale** | The exposure for a consumer app at this scale is low; an institution's procurement will ask; 1.5 days is cheap insurance when that moment comes |
| 6 | Non-English filler UI | **"Fillers: available for English talks"** in the place the count would be; never a zero, never "beta" or "wip" | A zero is a lie, "beta" invites distrust of everything else, and the sentence is true |
| 7 | Library output for non-English fillers | **Keep emitting; the app gates** | No library change, and you keep the data for later |
| 8 | Played-clip fix | **Build it** (about two hours) | Lecturers play videos; a clip's audio in "your" numbers is the kind of error that costs trust |
| 9 | Delete `filler_eval` | Either; it is git-ignored | Not a decision worth your time |
| 10 | Android backend split | **Later**, measure the CPU-code share first | Three 1.9 MB libraries are not the problem this quarter |
| 11 | Core ML on iOS | **Later**, after the iOS app exists and the CPU path is verified on devices | It breaks byte identity and the filler scan needs the CPU decoder |

## E2: the nineteen round-6 decisions

| Decision | My answer |
|---|---|
| overlap-finding ("two voices at once") | **Not in v1.** It needs a second model and a port; overlaps are not in the result schema. Revisit with meeting mode |
| speaker-change from pyannote | Drop; round 8 superseded it |
| filler-defaults | Keep defaults; English uses the scan |
| far-field-warning | **Yes**, and cap any "good" at "ok" when SNR is low, as winlab does |
| octave-fix | Yes |
| pitch-port (SwiftF0) | No |
| hotwords | **Ship the string-level method with a tiny UI** ("names and terms in this talk"), and in Phase 2 fill it automatically from the deck (doc 03) |
| entropy-conf | No, closed |
| events | No |
| short-takes | **Yes, port the "too short" rule** (rate, pitch and volume from 30 s; pauses from 60 s; nothing about uptalk or repetitions under 90 s) |
| lang-bands | Yes, as prototype, with the soft "other" bands for the five uncalibrated languages |
| presets / speaking contexts | **Not as settings. As one question at the start of a take:** "What are you practising? Presentation, Lecture, Meeting, Interview." It sets the bands and which findings appear, and it frames expectations. One tap is not a setting |
| keypause | Informational only |
| practise-wording | "Words the recognizer could not catch", never "mispronounced" |
| optional-modules (notes, key terms) | **Phase 2, fed by the deck's text** (doc 03) |
| positioning | Reword to what is true: "Rehearse your talk, then jump straight to the moments that need work: pace, pauses, unclear passages, and (in English) fillers. In eight languages, on your phone, with nothing uploaded." |
| daily-practice | Later, in the standalone app |
| port-order | As the document says, plus round 8 and the chosen screen; rehearsal memory ahead of overlap |
| default-word-list | No |

## E3: the direction questions

| Direction | My answer |
|---|---|
| Rehearsal memory (compare takes by word alignment) | **Build it.** No model, all languages, one to two days for the prototype, and it is the feature that makes rehearsing three times meaningful: "40 seconds shorter, you skipped the pricing slide, you hesitated at the same place in four of four takes". Takes group by the talk's name; the comparison appears automatically from the second take. v1 if it fits, else the first update |
| Live mode (live transcript, live cues) | **Not now**, with one distinction: decoding during the talk is not live mode and you should do it (below). Live cues on the phone during a real talk are a distraction you cannot take back; a live pace meter is a Phase 3 experiment at most |
| Overall score 0 to 100 | **No.** Three numbers with trends and a per-area level (Good, OK, Work on it). Your own verdict document already warned about this; trust it |
| Settings for end users | Lab only, plus the one-question context picker |
| Norms for percentiles | **No percentiles in v1.** The norms come from research-only talks. Rebuild them from commercially usable audio (VoxPopuli) in Phase 2 or never show percentiles; absolute bands are enough |
| Custom words upgrade (beam search) | Not now |
| Pronunciation with a known text | No |
| Standalone apps | Yes, the coach app second; doc 05 |

## Decode during the talk, analyse at the end

The engine already processes long audio in 20.48-second windows with 5-second context. Feed those windows as the recording produces them, on the phone, during the talk or the rehearsal, at your measured 19 times real time on a Pixel 9 (a few percent of one core's time on a recent phone, more on a mid-range one). Run the gap rescue, the speaker turns and the analytics once at the end over the audio you kept in memory anyway; the document says that pass takes seconds. Result: the report is on screen seconds after the talk ends instead of two minutes later, and on iOS you never need background processing, because the app is in the foreground for the presenter screen the whole time. Two things to verify: that the streaming path produces the same words as the batch path within tolerance (your byte-identity culture will have to accept a small, documented difference), and the battery cost over an hour on a mid-range phone. Confidence: medium-high that it works; high that it is the right design if it does.

## Memory, devices, download

- **Memory.** About 1.37 GB plus 4.85 MB per minute. iPhones with 4 GB (iPhone 11, 12, 13, SE 3) sit at roughly a 2.1 GB per-app limit; 3 GB and 2 GB iPhones (XR, X, 8, which still run iOS 16) cannot run this at all. Gate the coach by physical memory and cap the recording length by the available memory at start; use Apple's increased-memory-limit entitlement where it applies; on Android require 6 GB unless a 4 GB test passes. The remote keeps its iOS 16 minimum; the coach shows "needs a phone with at least X GB" on the others.
- **Download.** The 155 MB model and the 3.75 MB voice model on first use, on Wi-Fi by default, resumable and checked (you have this). Keep the store binary small. Hosting on Cloudflare R2 behind your Worker costs nothing in egress; Play's on-demand asset packs are an alternative on Android.
- **Time.** With decoding during the talk, the wait disappears; without it, a 30-minute talk is two minutes on a Pixel 9 and five on a mid-range phone, which needs a progress screen and a "keep the app open" line.

## Privacy, consent, licences

- **Only your voice is kept, by default.** Round 8's main-speaker logic makes this a one-line default: other speakers' words are dropped from the stored transcript unless the user turns on "keep all speakers" (meetings, Q&A). This is the single best privacy decision available to you, and it is also the legal one: in Germany, recording non-public speech of others without consent is a criminal matter (verify the exact scope with your Steuerberater's lawyer friend or a one-hour consultation), and a seminar or meeting is not public. Add a one-time notice: "Recording other people may require their consent. By default only your own words are kept."
- **Nothing uploaded, except what you choose.** The server correction sends unsure words as text, never audio; make it opt-in with the provider named in one sentence. Your positioning line must not say "nothing uploaded" without that qualifier.
- **Licences screen.** NVIDIA's teacher model (CC BY 4.0, attribution), TranscribePsy (Apache 2.0), the engine, ggml (MIT), WeSpeaker ResNet34-LM (CC BY 4.0, with the attribution string the GGUF carries), the fbank front end, and anything else you vendored. CC BY is not optional.
- **Export compliance.** The model decryption and the HMAC signing mean the app "uses encryption"; answer the store questions truthfully. If the crypto comes from the OS libraries, it is the usual self-classification; if a vendored cipher is compiled in, check whether the annual self-classification report applies (verify; a one-time half hour).
- **Eight languages, said precisely.** "Transcription, pace, pauses, pitch and volume in eight languages. Fillers in English." Localize the app's UI and store listings in exactly those eight languages (English, German, French, Spanish, Italian, Dutch, Polish, Portuguese); it aligns the marketing claim with the product and it is the cheapest multiplier you have.

## Which findings ship in v1 (by your own reliability table)

Ship: speaking rate (overall, fastest and slowest parts), pauses and long silences, fillers (English only, "at least N", capped on noisy audio), lively voice (pitch range with the octave fix), steady volume and trailing off shown as moments rather than counts, recording quality, per-slide and per-minute hotspots, words to practise ordered by word probability, clarity stretches, timing against planned minutes, opening pause, rushing stretches, flat sentences, and with round 8 the speaker share.

Hide behind "Full analysis" or keep off: repetitions (7% recall), uptalk as a count (noisy; keep it as "moments to listen to"), crutch and hedge lists (informational, English, German and French only), openers, stamina, pitch drift, audience address, emphasis, key pauses.

Put a thumbs-up and a thumbs-down on every finding card ("Was this useful?"), counted anonymously. That is your Verdicts page in the hands of real users, and it decides what moves out of "Full analysis" later.

## The post-take flow, concretely

1. The take ends. The report appears within seconds (decoding happened during the take).
2. Screen B: one strength with its best moment, one thing to work on with its three moments and a goal for the next take, a second strength, three numbers with trend. "Play the moments" starts the reel with the lead-in, the live transcript and the cue sound.
3. "Details" opens E. "Compare with last take" opens rehearsal memory once a second take exists.
4. The takes list shows A's snapshot per take under the talk's name.

## What I am not sure about

- **The one-week rule for round 8.** If the Android build is harder than expected, shipping the readable build is not a loss; the first update can carry round 8.
- **Decode-during-the-talk** depends on the engine's streaming path and on how the windowed decode handles a window boundary mid-word; the document says the stream API exists with a 320 ms minimum chunk, so I expect it to work.
- **The memory base of 1.37 GB** looks high for a 155 MB model; if it is a scratch allocation sized for the maximum window, it may be reducible, which would widen the device range. Worth one afternoon of measurement, not a project.
- **The German consent rule's exact scope** for lectures and seminars; the "only your voice" default is right under any reading.
