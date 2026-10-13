# Transcription, the presentation log, and "intelligence"

## Decision: transcribe on the phone

Not on the companion. Five reasons, any one of which would be enough:

1. **The microphone is in the right place.** The phone is in the presenter's hand or on the lectern, near the mouth. The laptop is often two metres away, behind the presenter, with a fan.
2. **The slide timestamps are already there.** The phone sends every next and previous, so aligning text to slides is bookkeeping on the phone. No protocol work, no companion involvement.
3. **It works in every mode.** Bluetooth clicker without a companion, browser viewer, and rehearsal at home with nothing connected at all. Rehearsal is where students will actually use it.
4. **Both platforms now have on-device long-form recognition without bundling a model.** You will not ship 150 MB, and you will not run a speech server.
5. **The privacy story stays whole.** Audio never leaves the device; text stays on the device unless the user exports it.

The companion only ever needs a speech engine if you add a "laptop microphone" option later, and then only on macOS 26 (which has the same engine); Windows has no good free on-device engine without bundling one. Phone-first is also the cross-platform answer.

## Platform reality (verify each on a device)

| Platform | What to use | Minimum | Notes |
|---|---|---|---|
| iOS 26 and later | SpeechAnalyzer with SpeechTranscriber | iOS 26 | On-device, built for long-form and distant audio, no one-minute limit, models downloaded on demand through AssetInventory rather than bundled. About 40 locales are listed, but the supported-locale list has been unreliable across betas (Arabic was listed and did not work; some locales failed to download). Run a short validation transcription per locale before offering it, as other developers do |
| iOS 16 to 25 | SFSpeechRecognizer with on-device recognition required | iOS 13 for on-device | Lower accuracy, sessions that need restarting, fewer languages. Offer it as "basic transcript" or skip it and show "transcripts need iOS 26" on older phones. I would skip it: a bad transcript costs more trust than a missing one |
| Android 13 and later | The on-device recognizer with a segmented session | API 33 for segmented sessions; the on-device factory exists from API 31 | Segmented sessions deliver results per segment and keep listening, which is the fix for the old "words lost between restarts" problem you remember. Check on-device availability first and trigger the language pack download when missing. The general SpeechRecognizer documentation still warns against continuous use for the server-based path; that warning is about battery and bandwidth, and on-device removes the bandwidth half |
| Android 12 | On-device recognizer without segmented sessions | API 31 | Restart-based sessions with gaps. Treat like iOS 16 to 25: skip |
| Samsung phones | Same APIs, but the system recognizer may be Samsung's rather than Google's | | Behaviour and language packs differ. Test on one Samsung and one Pixel before launch; both are common among your users |

Rule: show the transcript feature only where the on-device check passes, hide it elsewhere, and never fall back to a cloud recognizer. A feature that exists on most phones from the last three years and is absent on older ones is normal; a feature that quietly sends audio to a server breaks the promise.

## The feature, in stages

**Stage 1, v1: the presentation log, timings only.** After every talk the app stores a row: date, duration, number of slides (from next and previous counts), time per slide, pointer seconds, black-screen seconds, back-steps, longest slide. Optional name, otherwise "Unnamed talk, 12 Oct 2026, 30 min, 15 slides". Local only. The post-talk screen that shows this row is also the natural home for the feedback banner, the companion upsell, and the rating prompt. This stage needs no microphone and no permission. Your "just time per slide" instinct is right, and it is enough to make the app worth opening after a talk, which it otherwise never is.

**Stage 2, Phase 1.x: the transcript.** A microphone toggle on the presenter screen ("Transcribe this talk"), off by default, remembered. Text per slide stored with the log row. Audio not stored. Export as text or Markdown through the share sheet. The phone's microphone permission prompt appears the first time, with a one-line reason; iOS shows its recording indicator during the talk, which is correct and should not be hidden.

**Stage 3, Phase 2: the overview.** A summary of your own talk, bullet points per slide, and the pace and filler statistics you want. Do it on-device where the phone can: iOS 26 Foundation Models on Apple Intelligence devices (iPhone 15 Pro and later; languages limited to the Apple Intelligence set, verify the current list), ML Kit GenAI summarization with Gemini Nano on supported Android devices (Pixel 8 and later, recent Galaxy flagships; English first, verify). Elsewhere, an opt-in cloud summary that sends text only, never audio, with the model and the data location named in one sentence. Filler words and pace in many languages are an LLM job, as you said; manual counting works for one language and fails for the next.

Order of value: stage 1 is cheap and makes the app sticky; stage 2 is the "intelligence" story for the application and the Pro+ justification; stage 3 is what makes stage 2 useful to someone who will not read a 4,000-word transcript.

## UX and caveats

- **Battery.** An hour of on-device recognition costs real battery; my guess is 10 to 20 percent on a recent phone, which is fine for a 20-minute talk and worth a warning for a 90-minute lecture ("Transcribing for long talks: keep the phone charged"). Measure it.
- **Pocket mode.** In Android screen-off mode the phone may be in a pocket; the transcript will be muffled. Show "For transcripts, keep the phone in your hand or on the lectern" the first time both are on together.
- **Rubbing noise.** A thumb on the microphone opening is the main failure; the presenter screen's thumb zone should sit away from the microphone edge, which on most phones means the bottom edge in landscape is where the mic is. Check per device orientation.
- **Language.** The app's UI language is not the talk's language. Ask once ("What language will you speak?") with the device locale as the default, and remember per talk name.
- **Storage.** Text is tiny; keep everything. Audio, if you ever add it, is a Pro+ setting with a size warning.
- **Nothing in the stipend narrative should promise cloud transcription.** "On-device, private, aligned to slides" is a stronger sentence anyway.

## How influential is it, honestly

- On installs: small. Nobody searches for "presentation remote with transcript".
- On retention and on the post-talk habit: medium. The log alone gives the app a second screen people return to; the transcript makes rehearsal a reason to open it at home.
- On who pays: medium to high. It is the clearest ongoing-value feature for Pro+, and lecturers and trainers are its natural buyers.
- On the application: high. It is the "intelligence layer" slide, it is privacy-clean, and it is credible because the pipeline is simple.

Worth doing because it is self-contained and phone-only, and because stage 1 costs almost nothing. Do not let stage 2 delay the push; it can ship in the first update.

## Live captions

Skip, as you decided. PowerPoint and Google Slides have them; the only argument for a companion-level overlay is Keynote and PDF viewers, and that is a Phase 3 accessibility feature with the macOS 26 engine, if an institution ever asks.

## What I am not sure about

- **The locale list on iOS 26** has been unreliable; validate every language you advertise.
- **Android segmented sessions on vendor recognizers** (Samsung, Xiaomi) may behave differently from Google's; the two-device test settles it.
- **Battery figures** are a guess until measured.
- **On-device summarization language coverage** on both platforms is narrower than recognition coverage; German is on Apple's list, but check the Android side before promising it to teachers.

## Sources checked

- SpeechAnalyzer overview and locale caveats: https://antongubarenko.substack.com/p/ios-26-speechanalyzer-guide and https://dev.to/arshtechpro/wwdc-2025-the-next-evolution-of-speech-to-text-using-speechanalyzer-6lo and https://developer.apple.com/forums/thread/797835
- Android SpeechRecognizer reference (on-device factory from API 31, segmented sessions, continuous-use warning): https://developer.android.com/reference/android/speech/SpeechRecognizer and https://developer.android.com/reference/android/speech/RecognitionListener.html
