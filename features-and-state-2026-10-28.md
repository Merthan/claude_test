# Current technical features, technical state and user-facing features (2026-10-28)

The companion to `context/handoff-2026-10-28.md`. It describes what exists, how good it is, where it lives, and what
hasn't been decided yet.
- Numbers come from the reports named in brackets; nothing here is new measurement.
- "Shipped", "readable" and "round 8" are the three library tiers (part C1).
- Paths are relative to `C:\Users\merth\Desktop\AnyPresent\TestingMiscArea\TranscribeModelTest`.

**Contents**
- Part A: overview
- Part B: technical features in detail
- Part C: technical state (builds, verification, limitations, tests, data)
- Part D: user-facing features (phone app, winlab prototypes, languages)
- Part E: decisions not yet made
- Part F: decided against

---

## Part A. Overview

| Feature | User-facing? | Languages | Quality (short) | Shipped | Readable | Round 8 | winlab | Phone app |
|---|---|---|---|---|---|---|---|---|
| Transcription (on device) | yes | 8 | WER ≈ 10.9 % on 29 real talks | ✓ | ✓ | ✓ | ✓ | ✓ |
| Word timing, confidence, alternatives | partly (marks) | 8 | timing median 70 ms off; confidence well calibrated | ✓ | ✓ | ✓ | ✓ | ✓ |
| Gap rescue (re-decode skipped speech) | invisible | 8 | recovers ~2 / 3 of skipped sentences | ✓ | ✓ | ✓ | ✓ | ✓ |
| Pauses, sentences, speaking rate | yes | 8 | good | ✓ | ✓ | ✓ | ✓ | ✓ |
| Pitch (YIN), loudness, uptalk, trailing off | yes | 8 | pitch OK; uptalk / trailing noisy | ✓ | ✓ + octave fix | ✓ + octave fix | ✓ | ✓ |
| Recording quality (SNR, clipping, warnings) | yes | 8 | good | ✓ | ✓ | ✓ | ✓ | ✓ |
| Fillers: words the model wrote (`fl`) | yes | lexicon per language | English good; rare elsewhere | ✓ | ✓ | ✓ | ✓ | ✓ |
| Fillers: unwritten "um / uh" (`hesitations[]`) | yes | **English only (decision)** | English scan 72 % found / 94 % right | sound-only 38 % / 89 % | sound-only | **scan (en)** | ✓ | sound-only |
| Repetitions | yes | 8 | 7 % recall: unreliable | ✓ | ✓ | ✓ | ✓ (a problem kind) | ✓ |
| Per-slide numbers (if slide times are passed) | yes | 8 | good | ✓ | ✓ | ✓ | ✓ | ✓ |
| LLM correction of unsure words (server, optional) | yes | 8 | — | ✓ | ✓ | ✓ | ✓ | ✓ |
| Custom words (`hotwords`) | yes (planned) | Latin scripts | 13 hard names fixed, 0 broken | ✗ | ✓ | ✓ | ✓ (config) | ✗ |
| Speaker turns ("Speaker 1 / 2"), stats for "you" | yes | any | main speaker 4 / 4 meetings; 70 % of switches at 72 % precision | ✗ | ✗ | ✓ (voice model) | ✓ | ✗ |
| Word probability `wp` (better practise list) | yes (ordering) | 8 | top-8 71 / 69 / 74 % real errors (en / de / fr) | ✗ | ✗ | ✓ | ✓ | ✗ |
| Re-analysis without decoding (`tpsy_coach_transcript`) | no (speed) | — | seconds instead of minutes | ✗ | ✗ | ✓ | ✓ | ✗ |
| Coach findings (checklist, 12) | yes | 8 (bands en-tuned) | prototype | — | — | — | ✓ (more) | ✓ |
| Coach findings (winlab, 30) | yes | en / de / fr lists | prototype | — | — | — | ✓ | ✗ |
| Post-take screens (UX concepts A–E) | yes | 8 | prototype, owner liked it in general | — | — | — | ✓ | ✗ |
| Overlap "two voices at once" (pyannote 1.5 MB) | proposed | any | 83 % precision / 50 % recall (AMI) | ✗ | ✗ | ✗ | Review list only | ✗ |

---

## Part B. Technical features in detail

### B1. The speech model
- **Lineage:** NVIDIA Parakeet-TDT-0.6B-v3 → Tether QVAC **TranscribePsy-250M-EU-sub** (HF org `qvac`, Apache-2.0,
  teacher CC BY 4.0) → the owner's quantisation.
- **Architecture:** FastConformer encoder (24 layers, d_model 640) + TDT decoder (token-and-duration transducer: each
  step emits a token or blank plus a skip of 0–4 frames).
  - 8,192 sub-word pieces shared by all 8 languages (Latin, Cyrillic and Greek mixed; no per-language word list).
  - 80 ms frames.
- **Languages:** English, German, French, Spanish, Italian, Dutch, Polish, Portuguese (the 8 MLS languages).
- **File:** `models/custom-1.gguf`, 155 MB.
  - The recipe `C_enc4`: encoder matrices in IQ4_NL, the unused fused `attn.qkv` dropped, the TDT decoder kept at Q8_0
    (4-bit would cost +46 MB of RAM), plus one tiny training step on the owner's voice clip, naming it "custom 1".
  - Same WER as the official 305 MB file (FLEURS: −0.10 pp clean, +0.17 pp noisy, not significant).
  - Shipped encrypted as `obfuscated/models/sx.bin`.
  - The floor without retraining is ~145 MB (`README.md`, `results/report.md`).
- **Training data facts that matter:** the French and German training transcripts had fillers removed. So the model
  gives "euh" / "äh" no probability, which is why the filler scan is English only (`round8/DO-NOT-TRY.md`).

### B2. Engine and decoding
- **Engine:** `tether-ai-research/qvac-transcribePsy` @ `364ec36` (parakeet.cpp on ggml), vendored in
  `tpsy_core/third_party/qvac-transcribePsy` with our patches:
  - **Patch 1:** exports (piece probabilities, durations, alternatives).
  - **Patch 2:**
    - optional entropy confidence (`ent_conf`, off; no gain);
    - optional decoder phrase bonus for custom words (`hotword_start` / `hotword_bonus`, off, not recommended).
  - **Patch 3 (round 8):** the filler scan.
    - Read-only: on every blank step it also reads the joint network's probability of word-start filler pieces (um, uh,
      hm, äh, ehm, euh, eh, er, ah, em), including frames a blank skips.
    - It never changes which token wins.
    - CPU decode only.
- **Our code has no CPU-specific code**; all SIMD is inside ggml's kernels (rule: keep it that way).
- **Long-form windows:** `window_frames 256` (20.48 s) with `context_frames 64`.
  - The engine's API default (one 300 s pass) needs 13–15 GB of RAM on 20–25 min talks: never use it.
  - Recordings up to 4 h (`max_input_s`).
- **Gap rescue (library, on by default):**
  - Stretches of ≥ 2 s without a word start that hold ≥ 1 s of speech-level audio (15 dB above the noise floor) are
    decoded again with 2 s of context.
  - It recovers about 2 / 3 of the occasional skipped sentences (about one per hour of audio).
  - Rescued words are marked.
- **Known engine traps:**
  - Decoder cold start: sometimes no first token for seconds to minutes. At the chosen windows: 0 / 29 talks official,
    1 / 29 with C_enc4.
  - Short skips: ~1 per hour, mostly fixed by the gap rescue.
  - The stream API needs `chunk_ms ≥ 320`.
  - Thread scaling is poor beyond ~4 threads.
- **Dev tool:** the engine CLI (`parakeet.exe`) dumps encoder frames with env `PARAKEET_DUMP_ENCODER=<file>`.

### B3. Library API (`round8/tpsy_core/include/tpsy.h` is the reference)

**Lifecycle:**
- `tpsy_open(model, options_json, &err)`, `tpsy_close`, `tpsy_cancel`, `tpsy_free`, `tpsy_version`, `tpsy_last_error`.
- Open options include `voice_model` (round 8: the voiceprint GGUF; without it there are no speaker turns) and
  `backends_dir`.

**Calls (each also as `_file` for a WAV path):**
1. `tpsy_transcribe`: plain text.
2. `tpsy_coach`: everything (decode + rescue + analytics + JSON; with the voice model, speaker turns too).
3. `tpsy_run`: the same, with every setting in the config.
4. `tpsy_coach_transcript` (round 8): re-runs speaker turns + analytics + JSON on an existing result and the same audio,
   without decoding.
   - Seconds instead of minutes.
   - Use it after an LLM correction, for new settings or slide times, or for speaker turns alone (`{"analytics": false}`).
   - Not bit-exact with a fresh run: times are rounded to 10 ms in the JSON; 8 rescued words differed slightly in level /
     pitch.

**Helpers:**
- `tpsy_llm_requests(result, options)`: the marked lines for the server LLM.
- `tpsy_apply_fixes(result, response)`: applies the server's fixes.
- `tpsy_sign(ts, path, body)`: X-Auth signature.

**Config keys and defaults** (`transcriber.h`; `parse_config` in `api.cpp`):

| Group | Keys (default) |
|---|---|
| Decode | `threads` 4, `window_frames` 256, `context_frames` 64, `top_k` 3 (alternatives per piece), `steps` true, `pieces` false, `max_input_s` 14400, `preset` |
| Rescue | `rescue` true, `rescue_gap_s` 2.0, `rescue_speech_s` 1.0, `rescue_db_above_floor` 15, `rescue_pad_s` 2.0 |
| Analytics | `analytics` true, `pitch` true, `low_conf` 0.60, `pause_min_s` 0.30, `long_pause_s` 3.0, `sentence_gap_s` 1.5, `sentence_max_words` 60, `slides` (array of seconds) |
| LLM marks | `llm_conf` 0.85 (~7 % of words marked, roughly half wrong), `llm_alt_min` 0.05, `llm_alts` 2 |
| Fillers | `fillers` true; gap search `hes_gap_min_s` 0.30, `hes_min_s` 0.20, `hes_max_s` 1.50, `hes_db_below_speech` 20, `hes_tail_s` 0.10, `hes_flat_st` 4.0; written ambiguous fillers `filler_amb_min_s` 0.35, `filler_amb_gap_s` 0.25; scan (round 8) `filler_scan` true, `filler_scan_min_p` 0.003, `hes_scan` true, `hes_scan_p` 0.005, `hes_scan_confirm_p` 0.003 |
| Custom words | `hotwords` [], `hotword_sim` 0.78, `hotword_conf` 0.70, `hotword_start` 0, `hotword_bonus` 0 |
| Confidence | `ent_conf` false |
| Speakers (round 8) | `speakers` true, `spk_hop_s` 1.0, `spk_refine` 0.45, `spk_min_gap_s` 0.10, `spk_min_speaker_s` 15, `spk_thr` / `spk_thr2` / `spk_rerecog` / `spk_merge_sim` −1 (= the voice model's own values; ResNet34: 0.675 / 0.54 / 0.60 / 0.35) |

### B4. Result data (what every coach result contains)

Documented field by field in `round8/tpsy_core/bridges/android/SpeechResult.kt` (and `SpeechResult.swift`).

**`words[]`:**
- `w` (text), `s` / `e` (start / end), `c` (confidence = minimum piece probability), `alt` (alternatives with
  probabilities), `db` (loudness), `f0` (median pitch), `syl`, `pc` (punctuation probability);
- `fl` (filler word: 1 lexicon, 2 ambiguous word with evidence), the rescued flag, LLM-fix marks;
- round 8 adds `spk` (speaker label) and `wp` (probability of the whole word, on unsure words).
- **Caveat:** `e` runs on to a late "." / "," piece (handoff, section 5.4). Pauses and sentence ends already use the
  speech end.

**Low-level traces:**
- `pieces[]` (sub-word tokens: id, text, time, probability, duration, alternatives; only with `pieces: true`).
- `steps[]`: decoder certainty every visited frame.

**`sentences[]`:**
- start / end (speech end), words, text, an LLM line with `{word|alt}` marks;
- `wpm` (including the pause after), `art_wpm` (while speaking), loudness;
- end-level drop + trailing off, pitch range, end rise + uptalk, unsure-word count, how it ended;
- round 8 adds `spk`.

**Other lists:**
- `pauses[]` = [start, duration, before-sentence flag].
- `hesitations[]` = [start, end, p_speech, pitch range, scan_p]: unwritten filler candidates.
- `filler_scan[]` = [t, p, piece] (round 8).
- `repetitions[]`, `slides[]` (per-slide rate, pauses, fillers, loudness, pitch range), `rescued[]`.

**`stats`:**
- words, speaking time, wpm, articulation wpm, syllables / s;
- pauses (count, per minute, mean, max, total, long);
- mean confidence, low-confidence words, rescued words;
- loudness median / range, pitch median / range, uptalk / trailing counts;
- hesitations, filler words, fillers per minute, repetitions, `language` (guess).
- Numbers only (plus `language`): the Kotlin reader parses every value as a number.
- Round 8: `stats.speaker`, `stats.share`. With 2+ speakers, `stats` / `pauses` / `hesitations` / `repetitions` /
  slides describe the main speaker; `stats_all` keeps the whole recording.

**Speakers (round 8):** `turns[]`, `speakers{count, main, model (attribution string), windows, switches, list}` (per-speaker
stats and share).

**`quality`:** clipping %, speech level, noise floor, SNR, warnings (clipping, too_quiet, noisy, no_speech).

**`text`, `text_marked`, `timing`, `capabilities`** (`speakers`, `filler_scan`, …), `config`, `version`.

### B5. Analytics inside the library (`src/analytics.cpp`)

**Pauses**
- Gaps between words of ≥ 0.30 s. A gap starts at the last letter piece + 0.16 s (fix f544f36: the model writes "."
  only when the next speech starts, so the word end used to swallow the pause).
- Long pause: ≥ 3 s.

**Sentences**
- Split at end punctuation, a pause of ≥ 1.5 s, or after 60 words at the longest pause.
- Ends use the speech end (fix ed9c24e).
- Round 8: no sentence runs across a voice change.

**Speaking rate:** wpm overall and per sentence, articulation wpm, syllables / s.

**Pitch**
- YIN pitch track per word / sentence; range in semitones (p10–p90), end rise (uptalk), drift.
- Readable / round 8 add an octave / outlier correction (±50-frame median, octave moves, drop > 7 st jumps).
  Example: German talk de_r2tvb4 range 14.1 → 7.0 st.
- SwiftF0 was evaluated: only slightly more robust, not ported.

**Loudness:** per word and sentence, spread, end-level drop (trailing off).

**Quality:** noise floor, speech level, SNR, clipping, warnings.

**Language guess:** stop-word counts per language over the words (`A.language`, `language_score`).

**Fillers, three steps (`find_fillers`, long comment in the code):**
1. **Written filler words** from a per-language lexicon ("um", "äh", "euh", …). Spellings that are ordinary words in
   the recording's language (e.g. "a", "e", German "um") count only with evidence: long, flat, a gap before or after
   (`filler_amb_*`).
2. **Sound-only gap search** in every gap between words (word end = last letter piece + TDT duration):
   - a voiced sound within 20 dB of the median speech level;
   - ≥ 0.2 s long, ≤ 1.5 s of such sound per gap, flat pitch (≤ 4 st);
   - the first 0.1 s of a gap skipped, 3 s before the first word searched, never after the last word.
3. **English only (round 8, `A.language == "en"`):** the scan rule.
   - A stretch outside the words where the scan probability peaks at ≥ 0.005 is a filler.
   - A weaker voiced sound in a gap (≥ 0.1 s, down to 26 dB under speech) counts if the scan reaches 0.003 within
     0.12 s.
   - Sound-only finds without scan support are dropped.
   - The frame right before a word that starts with the same letters is ignored.

Other languages keep step 2. The product decision is to show fillers for English only (part E).

**Repetitions:** a word repeated right away. Only 7 % recall, because the model writes repeats once: unreliable.

**Slides:** given slide-change times, per-slide rate, pauses, fillers, loudness, pitch range.

### B6. Speaker turns (round 8; `src/voiceprint.*`, `src/speakers.*`)

**Voice model:** WeSpeaker ResNet34-LM (trained on VoxCeleb2, CC BY 4.0: attribution needed; the VoxCeleb data is a
licence grey zone, the owner's call).
- Converted to GGUF at 4-bit (Q4_0): `round8/models/voiceprint-resnet34-q4_0.gguf`, 3.75 MB, git-ignored.
- Made by `round8/tools/convert_voiceprint.py`.

**Front end and network**
- Kaldi fbank with mean normalisation, written in C++ (max difference 0.0002 vs. kaldi-native-fbank).
- ResNet34 in ggml with our own channel-innermost im2col custom op (ggml's own im2col took 80 % of the time).
- Cosine to onnxruntime f32: 1.0 at f32, ≥ 0.999 at 8-bit, 0.93 mean / 0.90 min at 4-bit.
- Equal error rate on AMI pairs: 1.45 %.

**Turn logic**
- 2 s voiceprints on a 1 s grid (adaptive: every 2nd window, plus refinement around gaps where the coarse windows
  differ).
- A voice-change test at word gaps of ≥ 0.1 s, with hysteresis.
- Re-recognition of earlier speakers; speakers with < 15 s of speech merge into the most similar bigger one unless
  clearly different.
- Numbering in order of appearance. Main speaker = most speaking time.

**Swappable:** the GGUF carries the network type, the front end and the tuned turn settings (`voiceprint.tuned.*`). A
CAM++ file would need only its graph (not built, ~1.5 agent days).

**Numbers (`round8/models-round8.md`)**

*AMI scenario meetings (4):*
- main speaker right 4 / 4;
- 70 % of switches between ≥ 10 s turns found, at 72 % precision (85 % lenient);
- labels 4 / 4 / 4 / 5 for 4 people.

*29 solo talks (6.1 h):*
- 1 shows a second speaker (a whispered passage);
- plain errors 0.3 per hour.

*Stats for "you" in meetings:*
- wpm error 14.5 → 5.3, fillers / min error 0.68 → 0.32;
- unclear-word list 926 → 308 entries, 68 % by the main speaker instead of 26 %.

*Per-speaker wpm:* within 4.3. *Talk share:* 4.5 points off on average, up to 13, always too high.

*Cost:*
- +3.75 MB file, +3–4 MB peak RAM;
- +28–31 % coach time (6.5-min talk 26.6 → 34.2 s; 30-min meeting 154 → 202 s, PC, 4 threads).
- Not measured on a phone.

**ggml finding:** the repacked 4-bit matmul loses accuracy with a 3D right-hand matrix (cosine 0.81–0.84); our code
reshapes to 2D. Worth reporting upstream.

### B7. Custom words (round 6; readable + round 8)
- **Config:** `hotwords: ["Name", "Term", …]`. An empty list means no change at all.
- **Default method, string-level correction** (`apply_hotword_fuzzy` in `transcriber.cpp`):
  - 1–3 decoded words are replaced by a listed phrase when the letters are similar (≥ 0.78) **and** the model was unsure
    (mean confidence ≤ 0.70).
  - The list spelling is used; timings kept; confidence set to 1.0.
- **Results:**
  - Hard names on 6 talks: 13 fixed, 0 broken, 0 other words changed.
  - 29 talks with oracle lists: 67 of 75 replacements right.
  - Decoy lists: 5 replacements, 3 wrong. The confidence gate is essential: without it 138 replacements, 143 broken.
- **Decoder bonus (opt-in, not recommended):** fixed ~7 of 40 names, with side effects ("sept" → "7", "a" → "à").
- **Limits:**
  - Latin scripts only.
  - Replaced words aren't marked in the JSON (a possible `fx` / `ow` flag).
  - The combination of both methods is untested.
  - Beam search with the list built in would be the real upgrade (~1 week, only when a list is set).
- **Default word list:** recommendation "no big list" (a generic 319-term list made 1 wrong replacement and 0 fixes on
  10 English talks).

### B8. Server (optional) and LLM correction (`server-contract.md`)
- **`POST /v1/optimize`:** the app sends the `[s]` sentence lines with `{word|alt}` marks for words below `llm_conf`
  (0.85; ~7 % of words). The server's LLM returns `fixed_segments`; the library applies them (`tpsy_apply_fixes`).
  Handles 401 / 413 / 429 / 502.
- **Model download:** signed `GET /v1/model?lib=1.0.0`, resumable, checked against size + SHA-256.
- **Auth:** `X-Auth` HMAC signature (`tpsy_sign`; the key is in `tpsy_core/src/sign.cpp`, private).
- **Server rule:** the server stays an optional transcription-correction helper. No server rating or content features.

### B9. Protection, release pipeline, platforms
- **Flow:** `tpsy_core/` (readable master, edit here) → `obfuscated/scripts/obfuscate_source.py` → `obfuscated/core/`
  (generated, never edit by hand) → builds.
  - The generated code renames everything (`sx_*` functions, `com.speechkit.SpeechEngine`), adds model decryption and
    hardening.
  - The model is encrypted at rest (`transform_model.py` → `sx.bin`).
  - Private, never published: `obfuscated/namemap.py`, `NAME-MAP.md`, `baked_config.json`, `models/sx-debug.gguf`, the
    HMAC key.
- **Version pairing:** `namemap.VERSION_STRING` = `sx 1.0.0` (the number is the server's `?lib=`).
  - Round 8 is `tpsy_core 1.1.0`; the server must map 1.1.0 to the same speech model.
  - The voice model is a new, separate asset.
- **Android:**
  - arm64-v8a only; three complete libraries of ~1.9 MB each:
    - `libsx.so`: armv8.2-a+dotprod+i8mm+fp16 (Armv8.6 / v9 cores);
    - `libsx_dotprod.so`: armv8.2-a+dotprod+fp16 (most phones since 2018/19);
    - `libsx_compat.so`: armv8-a (any arm64 phone).
  - The Kotlin loader picks one; `build_android.py` checks exports and 16 KB page alignment.
  - Idea (not done): ggml can split its CPU kernels into small per-CPU backend libraries loaded at runtime (`backends_dir`
    exists in `tpsy_open`), giving one main library + three small CPU libraries instead of three full copies.
  - Our build switches that split off for Android / iOS (`CMakeLists.txt`). How much of the 1.9 MB is CPU code is
    unmeasured. About ½–1 agent day + a phone test.
- **iOS:**
  - The Swift bridge (`Tpsy.swift`, `SpeechResult.swift`) has never been compiled (no Mac).
  - One build with a minimum chip level is enough.
  - The engine has a Core ML option (Neural Engine, CPU fallback), off in our build. Using it would mean:
    - unencrypted converted model files next to the app;
    - transcripts no longer byte-identical (judge by WER);
    - the English filler scan and confidences need the CPU decoder (unchecked whether that survives).
  - Recommendation: keep CPU as the reference; add Core ML only once an iOS app exists.
- **Windows / PC:** `sx.dll` (shipped) via `sx.py`; `tpsy.dll` (readable / round 8) via `bridges/python/tpsy.py`. These
  are used by winlab and pc_suite.

### B10. Resources and speed
- **RAM:** ~1.37 GB + 4.85 MB per audio minute (3 h ≈ 2.2 GB); the voice model adds +3–4 MB peak.
- **Speed:**
  - PC (Ryzen 5 5600X): ~12× real time for one job, ~16× for two in parallel.
  - Pixel 9: ~19× on the 3 s sample. A 30-minute talk waits about 1.5–2 minutes for its report on a Pixel 9 (estimate in
    `speech-verdict.md`).
- **Library size:** ~1.9 MB per Android variant; the model is 155 MB; the voice model 3.75 MB.
- **Decode on phone vs. PC:** identical on the Quick suite.

### B11. Measured quality (main numbers)

| What | Result | Source |
|---|---|---|
| WER, 29 real TED(x) talks en / de / fr | ≈ 10.9 % (3 h file 9.8 %) | `context/handoff.md` §9 |
| WER, FLEURS 8 languages | 9.11 % official; 155 MB file −0.10 pp | `results/report.md` |
| Word timing vs. SpeechMatics | median 70 ms, p90 200 ms | `context/handoff.md` |
| Confidence calibration | ≥ 0.95: ~4.6 % wrong; < 0.6: > 50 % wrong | same |
| Fillers, English, filler scan (round 8) | PodcastFillers test 72 % found / 94 % precision (84 % strict); AMI headset 73 % found, false alarms 1.6 / min in filler-free speech | `round8/models-round8.md` §3 |
| Fillers, English, sound-only (shipped) | podcasts 38 % / 89 %; AMI close-mic 65 % / 57 %; far-field 13–17 % recall | round 6 / 8 |
| Fillers, German / French, sound-only | German acted 59 % / 77 %; French interviews 31 % / 52 %; best language-independent idea still failed on French | `round8/research/DEAD-END-fillers-outside-english.md` |
| Words to practise (flagged words really misrecognised) | by confidence en 60 / de 41 / fr 69 %; top-8 by `wp` 71 / 69 / 74 % | round 6 / 8 |
| Overlap (pyannote seg-3.0 int8) | 83 % precision / 50 % recall on AMI; 0–1 false alarm / h solo | `research/overlap.md` |
| Events (laughter, breath, music) | laughter ~50 % precision; breath ≤ 8 % recall: nothing ships | `research/events.md` |
| Short takes | rate / pitch / volume stable from 30 s; pauses need 60 s; hedges 90 s; uptalk / repetitions < 90 s unusable | `research/short-takes.md` |

---

## Part C. Technical state

### C1. Which build has what

| | Shipped (`obfuscated/`, sx 1.0.0, built 2026-10-20) | Readable (`tpsy_core/`) | Round 8 (`round8/tpsy_core/`, 1.1.0) |
|---|---|---|---|
| Decode, rescue, analytics of 2026-10-20 | ✓ | ✓ | ✓ |
| Pause fix, sentence / recording end fix | ✓ | ✓ | ✓ |
| Octave / outlier pitch fix | ✗ | ✓ | ✓ |
| Custom words (string-level + opt-in decoder bonus), `ent_conf` (patch 2) | ✗ | ✓ | ✓ |
| Filler scan (patch 3), English scan rule | ✗ | ✗ | ✓ |
| Speaker turns, `voice_model`, stats for the main speaker | ✗ | ✗ | ✓ |
| `wp`, `tpsy_coach_transcript` | ✗ | ✗ | ✓ |
| Obfuscated + Android `.so` built | ✓ | ✗ (not regenerated since round 6) | ✗ (dry run of the obfuscation passed) |
| Used by | phone STT Lab, owner's app, pc_suite, winlab "shipped" | `lab.py check` | **winlab default** (`r8_worker.py`) |

### C2. Verification status
- **Round 8 vs. shipped:** decode byte-identical on the 6 reference files with every feature on and the voice model
  loaded (`round8/tools/check_identity.py --more --voice`, PASS 2026-10-27).
- After the filler-experiment removal (2026-10-27), the rebuilt `round8/build-win` gave output identical to before on
  454 of 454 files.
- **Readable vs. shipped:** identical on 3 files (`lab.py check`); the formal 45-file verification was not re-run after
  round 6 / 8.
- **Obfuscation:** the dry run on the round 8 tree passed (every anchored edit matched, no `tpsy` / `parakeet` / `qvac`
  names left). Not run for real.
- **Not done:**
  - Android builds of round 6 / 8;
  - the voiceprint check per CPU variant on a phone (criterion cosine ≥ 0.9 vs. PC f32);
  - phone speed of the speaker step;
  - the 45-file gate;
  - Swift compile.

### C3. Known limitations and bugs

**Engine and result data**
- **`words[].e` includes a late punctuation piece** (open fix). Effects:
  - a filler or pause after a sentence-final word sits inside that word's span;
  - the Timeline word box looks too long;
  - possibly the owner's "no ähm at sentence start / end" observation in their app.
- **`tpsy_coach_transcript` isn't bit-exact** with a fresh run (10 ms rounding; small level / pitch differences on
  rescued words).
- **Pitch already differs** between the shipped and readable builds on 65 words of the reference files (before round 8).
- **Engine:** decoder cold start (rare), ~1 skipped sentence per hour (mostly rescued), poor thread scaling beyond 4.

**Fillers**
- **Fillers outside English:** the model can't see them. The sound-only finder is weak there (59 % / 77 % German acted,
  31 % / 52 % French). The decision: show fillers for English only. The library still emits sound-only `hesitations[]`
  for other languages; the UI must gate them.
- **Filler counts are a minimum,** especially far from the microphone (far-field recall 13–17 %). winlab caps a "good"
  at "ok" when SNR < 18 dB or mean confidence < 0.88.

**Speakers**
- **Played clips:** the change into a video clip is found, but not the change back. A few seconds of clip then stay in
  "your" numbers. The fix is known (~2 agent hours), deferred by the owner.
- **Talk share is biased upward** in free discussions (missed short turns).
- **No real phone recording of a talk with audience Q&A** exists; AMI far-field meetings stand in.

**Other**
- **Repetitions are unreliable** (7 % recall).
- **Bands and thresholds** (pace, pauses, uptalk, per-language bands, presets, short-take limits, UX thresholds) are
  prototype values. Calibrated only on 29 TED(x) talks (en / de / fr): rehearsed speech, research-only licence.
  es / it / nl / pl / pt have no real-talk calibration.

### C4. Tests and tools that exist
- **Unit tests:** `winlab/tests/test_ux.py` (10), `winlab/tests/test_coach.py` (22), `winlab/selftest.py` (slide text).
- **Identity:** `round8/tools/check_identity.py`, `py -3.12 winlab/lab.py check [--full]`, `tpsy_core/tests/verify.py` +
  `obfuscated/scripts/verify_obf.py` (the 45-file gate, WSL), `obfuscated/scripts/harness.py` (readable vs. obfuscated
  JSON).
- **Batch tests:** `pc_suite/pc_suite.py`. Tests: smoke, podcast-quick / -test / -val / -sweep, talks-wer, fleurs,
  long-1h / -3h, threads, recordings; analyses of WER, fillers, calibration, timing, RAM.
- **Round 8 tools (`round8/tools/`):**
  - `eval_speakers_cpp.py`, `eval_turns_r8.py`, `speaker_benefits.py`, `speaker_extras.py`, `switch_aids.py`;
  - `filler_eval.py`, `filler_data.py`, `practise_eval.py`, `timing.py`;
  - `convert_voiceprint.py`, `check_voiceprint.py`, `embed_windows_cpp.py`, `adaptive_sim.py`.
- **Round 6 tools:** `research/tools/*.py` (every round 6 number is reproducible). **Round 7:** `model-testing/`.
- **Phone:** STT Lab Tests tab (Quick / Standard / Long / Provoke suites), `testapp/tools/make_testpack.py` (29 talks +
  FLEURS + 1 h / 3 h with PC baselines).

### C5. Data and licences
- **Commercially usable:**
  - AMI meetings (CC BY 4.0);
  - FLEURS (CC BY 4.0);
  - the owner's own recordings;
  - VoxPopuli (CC0 per its card; suggested for norms, not yet used).
- **Research-only (measure / tune thresholds only):**
  - PodcastFillers (it tuned two filler-scan thresholds);
  - TED-LIUM / mTEDx talks (the 29 test talks, CC BY-NC-ND: the norms in `winlab/norms.json` come from them);
  - CFPP2000 (French);
  - Nyra German disfluency set (licence unknown);
  - DisfluencySpeech.
- **Voice model:** WeSpeaker ResNet34-LM is CC BY 4.0, but trained on VoxCeleb2 (grey zone: owner's decision).
- **Locations:**
  - `testdata/` (`README.md`), `testdata/PodcastFillersData/` (28 GB);
  - `testdata/filler_eval/` (~0.5 GB, the dead-end test sets; only the README is tracked);
  - AMI shards rebuilt by `research/tools/ami_build.py`.

---

## Part D. User-facing features

### D1. Phone: STT Lab (`testapp/`, shipped library), what a tester sees today
- **Setup:** model download / import / verify, server URL, signing test vectors, device facts.
- **Run:** sample, recorder (16 kHz), any file or the test pack; every library setting; analysis cutoffs as sliders
  with Defaults; Provoke tools (crash, RAM pressure, cancel); live progress / RAM / thermal.
- **Results:** every run with speed, variant, peak memory, crash reason.
- **Viewer:**
  - **Text:** confidence colours, pause chips ≥ 1.5 s, "⋯ähm?" chips at unwritten fillers, filler words in orange,
    repetitions, rescued / LLM-fixed words, loud / quiet, pitch colours, per-sentence lines.
  - **Timeline:** rows of 5–40 s with certainty lane, pitch, word boxes, loudness, pauses, hesitations, slides.
  - **Coach:** the checklist.
  - **Stats:** numbers + 5 charts.
  - **LLM:** preview / send / simulate / apply / undo.
  - **JSON.**
  - Player with seek, ±5 s, 1×–2×.
- **Coach tab (prototype, `CoachRules.kt` + `Coach.kt`):**
  - Good / OK / Work on it, each with number, target, tip and "why";
  - findings: speaking rate (overall, fastest and slowest part, absolute band), pauses, long silences, fillers per
    minute, lively voice (pitch range), steady volume, trailing off, uptalk, repeated words, recording quality, per-slide
    / per-minute hotspots;
  - "Moments to review" with ▶ (1.5 s before) and ▶ now.
- **Not on the phone yet:**
  - anything from rounds 5–8 (relative rules, short-take limits, goals, words to practise, speaker turns, English filler
    scan, custom words, the UX concepts);
  - the port list is `research/phone-port.md`.

### D2. winlab prototypes (desktop, `py -3.12 winlab/lab.py serve`): what the owner judges

#### UX concepts tab: the newest work and the likely app screen
- **One analysis per take,** for the analyzed speaker only (with 2+ voices, the main speaker). Five layouts:
  - **A Snapshot:** score + level, one sentence, three numbers (pace, fillers, deliberate pauses), best and weakest part,
    the 3 moments to fix.
  - **B Coach's notes:** praise / improve / praise. A strength (with your best part), ONE thing to work on (why, how, its
    moments), a goal for the next take, the weakest passage as a practice script, a second strength, and "Who spoke
    when" (with 2+ speakers).
  - **C Replay:** playback first.
    - Problem reel at the top (all kinds, filters, lead time).
    - The talk on one timeline: pace ribbon against the sweet spot, problem ticks, deliberate pauses, other voices,
      passages, dashed speaker-change lines.
    - Best / worst part reels; a "⇄ Speaker changes" mode.
  - **D Scorecard:** overall score, six sub-scores (bars + radar), badges, change since the last take of the same run
    name, highlight / lowlight, a reel for the lowest score.
  - **E Full analysis:** everything per area, all moments, best / worst three with text, speakers, words to practise.
  - **☰ Datapoints:** every datapoint with this take's value, how it's measured, its reliability, which concepts show it,
    and verdict buttons.
- **Problem-moment replayer (in every concept):**
  - jumps through moments in time order with a short lead;
  - shows the detection above a live transcript (current word highlighted, the problem in red, an unwritten filler as a
    red "filler" mark);
  - advances by itself;
  - between moments, a 60 ms fade + a cue (soft beep default, chime, tick, short pause, nothing; saved as `ux_cue`).
- **Problem kinds and thresholds (`winlab/ux.py` `T`):**
  - filler (written or only heard);
  - pause inside a sentence ≥ 1.2 s (double weight from 3 s);
  - long silence ≥ 5 s;
  - 40 s without a pause of ≥ 0.7 s;
  - uptalk; trailing off;
  - rushing (the 30 s-smoothed pace above the ok band for ≥ 20 s);
  - flat sentence (≥ 12 words, < 2 st);
  - repetition;
  - unclear word (confidence < 0.6 or `wp` < 0.35; off by default).
  - Deliberate "power pauses": 0.7–3 s between sentences.
  - Passages: 25–45 s, cut at sentence ends.
- **Speaker changes** (not problems, never scored): each plays from 5 s before the previous speaker's last word to 5 s
  after the new speaker's first word. A silence over 3 s between them is skipped (1 s kept each side). Optionally also
  the voice changes the model folded back into the same speaker.
- **Scores:** six sub-scores (weight): Pace 1.2, Fluency 1.5, Pausing 1.0, Vocal variety 1.0, Confident endings 0.8,
  Clarity 0.5 (Clarity counts only for English).
- **Badges:** Filler-free stretch, Power pauser, Steady pace, Confident endings, Lively voice, Clean opening, Strong close.
- **Filler reliability shown in Datapoints:** "scan" for English round 8 runs; "sound-only, unmeasured in other
  languages" otherwise.
- **Neither the UX concepts nor `coach.py` hides fillers for non-English takes yet.** The English-only decision isn't
  applied in winlab or on the phone.

#### Coach tab (older): six views of the same findings
1. Checklist (= phone).
2. Focus (summary, strengths, 1–2 things, liveliest moment).
3. Story (whole talk on one line).
4. Per slide (vs. planned duration).
5. Scores + progress across takes with the same run name.
6. Report card (one printable page, PNG export, percentiles vs. 29 TED talks, goal and goal check, "compare speaking
   contexts").

#### Coach findings in `winlab/coach.py` (30, prototype; "new" ones aren't on the phone)

*Core:*
- `rate`: speaking rate.
- `stretches`: fastest / slowest parts, relative to your own median.
- `pauses`, `longpauses`.
- `fillers`: "at least N", capped on noisy audio, a "where" hint.
- `monotone`: lively voice, pitch range.
- `volume`, `trailing`, `uptalk`, `repetitions`, `quality`.
- `hotspots`: minutes / slides to practise, relative.

*Clarity and wording:*
- `clarity`: stretches the recogniser was unsure about.
- `crutch`: crutch and hedge words, en / de / fr lists, soft hedges.
- `practise`: words the recogniser couldn't catch, grouped by word.
- `sentlen`: short clear sentences.
- `openers`: pet phrases / sentence starts.

*Structure and timing:*
- `timing`: on time vs. planned minutes.
- `highlight`: liveliest moment.
- `arc`: start and finish vs. your middle.
- `opening`: opening pause.
- `stamina`: voice stamina over thirds of a 4+ min talk.
- `pausekind`: pauses between thoughts vs. inside sentences.

*Delivery:*
- `keypause`: informational.
- `emphasis`: words you stress, informational.
- `pitchdrift`.
- `engage`: questions and you / we.

*Optional modules:*
- `notes`: notes adherence.
- `musttalk`: key terms.
- `reading`: reading your slides; needs slide times + text.

*Settings:*
- Presets / speaking contexts: default / ted / pitch / lecture / meeting (change only the bands).
- Per-language bands (`LANG_RULES`) and short-take minimums (`SHORT_MIN_S`).

#### Other winlab pages
- **Run:** any dataset or mic; "Library" switch round 8 / shipped.
- **Results.**
- **Review:** 10 min on one page with keep / reject per detected item.
- **Verdicts:** wow / useful / meh / too complex / wrong per finding, view and datapoint.
- **Decisions:** the 19 round-6 questions.
- **Compare:** two runs side by side.
- **Progress:** rehearsals by run name.
- **Tests:** pc_suite. **Setup.**

### D3. Language support for user-facing features

| Feature | en | de | fr | es / it / nl / pl / pt |
|---|---|---|---|---|
| Transcription | ✓ | ✓ | ✓ | ✓ |
| Pace, pauses, pitch, volume, quality, speaker turns | ✓ | ✓ | ✓ | ✓ (bands uncalibrated: soft "other" bands) |
| Unwritten fillers ("um" counted) | ✓ (scan) | **not offered** (decision 2026-10-27) | **not offered** | **not offered** |
| Filler words the model writes (`fl`) | ✓ | rare | rare | rare |
| Crutch / hedge lists, audience address, stop words | ✓ | ✓ | ✓ | ✗ |
| Clarity limits | ✓ | per-language limits | per-language limits | soft |
| Words to practise | 71 % (top-8 by `wp`) | 69 % | 74 % | unmeasured |
| Custom words | ✓ | ✓ | ✓ | ✓ (Latin script) |
| German / French strings | — | not native-reviewed | not native-reviewed | — |

### D4. What the real app would show once round 8 ships (planned, not built)
- Speaker labels and talk share (rounded), with the voice model's attribution on the licences screen.
- All coach numbers for "you" (the main speaker). Filter the unclear-word and practise lists by
  `words[].spk == speakers.main`.
- An English filler count about twice as complete (72 % instead of 38 % found) with fewer false ones. No filler count in
  other languages.
- A practise list ordered by `wp`.
- Faster re-analysis after an LLM correction (`tpsy_coach_transcript`).
- The post-take screen the owner picks from the UX concepts.

---

## Part E. Decisions not yet made

### E1. New since round 8 (owner's call)

| # | Decision | Options | My recommendation | Notes |
|---|---|---|---|---|
| 1 | Which post-take screen the app gets | UX concepts A–E, a mix, parts of the Coach views | B "Coach's notes" or A "Snapshot" as the main screen, C "Replay" reels inside it; E behind "details" | the owner said "in general seems pretty good"; no verdicts stored yet |
| 2 | Fix `words[].e` (late punctuation) | fix in the library / leave / fix only in the app | fix in the library before shipping round 8 | decode unchanged; only word end times change; check the app's filler placement afterwards |
| 3 | Ship round 8 now | ship / wait | ship after 1 and 2 | `round8/REPLACE.md` checklist, steps 1–8 |
| 4 | Voice model delivery | bundle / download; encrypt like `sx.bin` / plain | download like the speech model; plain is acceptable (public, attributed model) | 3.75 MB |
| 5 | VoxCeleb grey zone of the voice model | accept / switch to CAM++ (Alibaba's own data) | owner's legal judgement | CAM++ graph ~1.5 agent days; loses more at 4-bit |
| 6 | Non-English filler UI | hide the section / "Fillers: available for English" / "wip" | "available for English" or hide; never a 0, never "wip" or "beta" | the owner floated "unsupported or wip" |
| 7 | Library output for non-English fillers | keep emitting sound-only `hesitations[]` / switch off for non-English | keep (the app gates them); avoids a library change | — |
| 8 | Played-clip fix | build (~2 agent hours) / leave | build with the round 8 ship if clips matter | deferred by the owner 2026-10-27 |
| 9 | Delete `testdata/filler_eval/` (~0.5 GB) | keep / delete | either; it's git-ignored | outside round 8 |
| 10 | Android ggml backend split (one main library + small CPU libraries) | do / leave three full copies | measure the CPU-code share first | ½–1 agent day + phone test |
| 11 | Core ML on iOS | later / never | later, once the iOS app exists | breaks byte identity; the filler scan needs the CPU decoder |

### E2. The 19 round-6 decisions (`research/decisions.json`; winlab Decisions page; none answered)

| Id | Question | Recommended | Note since then |
|---|---|---|---|
| overlap-finding | ship "two voices at once N times" (pyannote 1.5 MB)? | yes, 0.7 / 0.3 s, "at least N"; hand-port to C++ later (~300–400 lines) | still not ported; overlaps aren't in `SpeechResult` |
| speaker-change | keep the speaker-change items of the pyannote model? | drop | superseded by round 8 speaker turns |
| filler-defaults | default filler settings | keep defaults; tuned set opt-in | partly superseded: English uses the scan; other languages show no fillers |
| far-field-warning | "fillers under-counted: noisy / far" | yes | in winlab |
| octave-fix | keep the pitch octave correction | yes | in readable + round 8 |
| pitch-port | replace YIN with SwiftF0 | not now | — |
| hotwords | ship custom words, which method | string-level only, optional list | needs a phone UI |
| entropy-conf | change word confidence | no | closed |
| events | events feature (laughter, breath, music) | no | owner later dropped breath etc. too |
| short-takes | 30–90 s takes with "too short" rule | yes | port to phone |
| lang-bands | per-language bands from TED talks | yes, as prototype | — |
| presets | speaking-context buttons | keep | conflicts with `speech-verdict.md` "no settings for end users": decide |
| keypause | show as verdict? | informational only | — |
| practise-wording | "words the recognizer could not catch" | yes, never "mispronounced" | — |
| optional-modules | notes / key terms in the app | optional extras | — |
| positioning | which promise leads | "Rehearse your talk, then see exactly where you lose your audience: pace, pauses, fillers and unclear passages, in your language, on your phone, with nothing uploaded." | **fillers are English only now**: reword |
| daily-practice | 60–90 s daily practice in the plan | yes | — |
| port-order | phone port order | relative fastest / slowest; start & finish + goal + report card; short-take rules; words to practise; overlap; notes / terms | add round 8 items and the chosen UX screen |
| default-word-list | ship a ~1,000-word default list | no big list | — |

### E3. Direction questions (from `speech-verdict.md` v2 and later)

| Direction | State | Open question |
|---|---|---|
| **Rehearsal memory** (compare takes by word alignment: "40 s shorter, skipped pricing, hesitated here in 4 of 4 takes", before / after playback) | not built. Pieces exist: notes alignment, Progress page, change since last take, goal check | build next? (my recommendation: yes; no model, all languages, ~1–2 agent days for a winlab prototype) |
| **Live mode** (live transcript, live cues, instant report via a ~2 MB VAD + short segments) | not built; voice commands dropped | wanted at all? (about a week for a prototype) |
| **Overall score 0–100** | shown in UX concepts A / D and Coach view 5 / 6 | `speech-verdict.md` warns against a score built from weak parts: keep, or show three numbers with trends? |
| **Settings for end users** (presets, contexts) | in winlab | keep them in the lab only? |
| **Norms for percentiles** | from 29 TED talks (research-only) | rebuild from commercially usable audio (VoxPopuli) before showing percentiles in the app |
| **Custom words upgrade** | string-level method done | beam search with the list (~1 week); test FOSDEM / Earnings-21 audio for built-in terms |
| **Pronunciation with a known text** | later / maybe | needs a scoring function; testable on speechocean762 |
| **Standalone apps** | possible (coach app, transcription app, one model set) | which first, and add-ons as optional downloads |

---

## Part F. Decided against (don't re-propose)

- **Fillers outside English:** all nine ideas (`round8/DO-NOT-TRY.md`; measurements in
  `round8/research/DEAD-END-fillers-outside-english.md`; code in commit `6df8191`).
- Voice commands / wake words / auto-advance; "hear it without fillers" playback.
- Breath, throat clearing, coughs, laughter / music / applause events.
- Drawn-out words and "probable repetition" detectors; emotion / traits; camera; on-device LLM.
- Sortformer; ZIPA; Silero VAD as a fix; CED-tiny laughter (shelved).
- Forced scoring for practise words; longest monologue, turn counts, quick handovers, switch aids; part 5 of round 8.
- Speaker change from the pyannote model alone; entropy confidence; the tuned podcast filler settings as default.
- More WER work or a bigger model; a big default word list.
