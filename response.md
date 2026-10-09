# Response to your notes (9 October 2026)

*You asked for decisions, not menus, and for honesty about what I am unsure of. This file is the summary and the direct answers to each of your notes. Five topic files carry the detail. Nothing in `docs/` was changed. Where this response contradicts a doc, this response wins. No new web checks were made for this response; anything marked "verify" is from memory.*

## What changed in my recommendations

| Topic | The docs said | Now |
|---|---|---|
| Connection flow | Auto-detect, one question, silent mid-talk fallback | Auto-detect, then an explicit three-card menu (Bluetooth clicker, Companion, Website) with one-line explanations and a help sheet. No mid-talk switching. Internet is "by code", a backup inside the Companion card, never a top-level mode |
| Watches | 1.1 and 1.2 | In v1. Architecture: watch is a remote for the phone (baseline, covers keyboard mode), watch talks to the relay directly as a bonus. No watch-to-PC Bluetooth keyboard |
| Web viewer and web remote | 1.1 | In v1, built right after the protocol. The web remote also gives you guests for group mode |
| iOS keyboard mode | Treated as a risk | Treated as given |
| Roadmap | Staged over six months | Everything before the launch push, in a build order that finds integration problems first |
| Monetization at launch | Pro from day one if rules allow | Free launch phase with the on-screen credit from day one, Pro badged but free, price switched on in month 3 to 5 together with new features. Cosmetic pointers. Pro travels by session so the web viewer can be Pro without accounts |
| Company logo in the spotlight | Proposed | Dropped. The connection toast on the big screen becomes the primary free-tier credit |
| Ambition | A tool with a stipend narrative | A three-phase funded year: universal remote, presenter intelligence (notes, thumbnails, rehearsal analytics, on-device transcription and live captions), institutions and audiences (room mode for universities, event mode, audience slide-following). Written as aims with my expectations next to them |
| Accounts | None | None in v1, but the purchase record is designed for an optional email link later, and Pro travels by session now |

## Direct answers to your notes

### 05 UX

- **Connection flow.** You were right that "one question" hid too much. The new recommendation is Concept C in `response-connection-flow-and-controls.md`: a three-second scan for a known or nearby companion, then your explicit menu. Repeat users with a companion never see the menu. First-timers see three honest cards. The help text under the cards and a two-screen intro say the same thing twice on purpose: it works with nothing installed, and it is much better with the companion.
- **Internet as the backup.** Yes, and phrased as "by code" inside the Companion card. One nuance: for lecture-hall and school desktop PCs without Bluetooth, by-code is the only companion path, and there the phone is on mobile data and the PC is on wired LAN, so the slow-WiFi worry mostly does not apply.
- **"Are you connecting to a MacBook?"** No question. The Mac companion is discovered automatically and the direct link is used when it is seen.
- **Mid-talk switching.** Dropped, agreed. Red dot, a Reconnect button, the presenter decides.
- **Re-pairing.** Optimized for the 95%: remember the last computer, companion starts with the computer by default, and if it is not found, the menu with a one-line "Start AnyPresent on your computer" hint. Nothing cleverer.
- **Controls.** Your expandable actions menu plus two or three configurable shortcuts is the right shape. My recommendation: tap = next and hold = pointer on the same thumb zone, with a setting to separate them; the actions button in the hard-to-reach corner where exit is now; pointer type chosen on the phone and sent with every hold; labels on by default with a one-time "hide labels" hint after the first talk. A second concept with a gesture layer is in the file, not recommended for v1.
- **Watches.** Accepted for v1, and I now agree with your reasons. The design: all setup and purchases on the phone, the watch shows next, previous, black screen, timer and a connection dot, nothing more at launch. Baseline architecture is "watch controls the phone, phone forwards", because that is the only way a watch can drive keyboard mode. Direct watch-to-relay when the companion is in use is a bonus if the protocol makes it cheap. Wear OS as a Bluetooth keyboard to the PC: not in v1.
- **Website viewer and website remote.** Both scoped in the file. Viewer: PDF first, file never leaves the browser, thumbnails grid, effects in page, code and QR, group mode. Remote: parity on controls including gyro pointing through the browser, no Bluetooth, no purchases, credit shown. The remote belongs in v1 because it is the zero-install-anywhere path, the funnel into the app, and the way a group member without the app joins a group session.

### 06 Features

- **iOS keyboard mode.** Given, from here on.
- **Everything before the push.** Accepted. The condition is build order: protocol and session model first, because the web, the watches, the companion, group mode and room mode all inherit it. See `response-build-order-and-launch.md`.
- **Deterrence by breadth.** Partly true and worth it. The file lists the cheap deterrents that make "I could vibe-code this" visibly false.

### 07 Startup and stipend

- **The misunderstanding.** My concern was about the window before the funding starts, not during it. During the funding, founding a UG or GmbH and earning revenue that stays in the company is normal and expected. Your "everything free during the launch phase" fits both programmes under any likely reading. Two things to do: unpublish the old Pro app when the free launch goes live so nothing sells in the pre-start window, and verify whether you may pay yourself a salary from the company while on the stipend (I believe not; the stipend replaces it). `response-stipend-clarifications.md` has the BAföG and insurance arithmetic and the trimmed question list.
- **Aiming higher.** Agreed. `response-directions-and-ambition.md` has a direction map with ratings, deep dives on the ones that matter, a three-phase funded-year plan with "aim" and "my expectation" side by side, and an application skeleton. The two biggest new ideas, room mode for universities (the companion pre-installed on lecture-hall PCs by IT) and event mode (stage laptop, session-chair timer, speaker alerts), are also the two I most want you to build for spread, so the ambition is not decoration.

### 08 Name

- **Company logo in the spotlight.** Dropped, you are right.
- **Big "AnyPresent connected" on the screen.** Good idea, and better than the effect watermark as the main free-tier credit because it appears in every companion session while the screen is already projected. Design rules and the Pro interplay are in `response-monetization-accounts-and-free.md`.

### 09 Risks

- Agreed. Microsoft Store plus the Apple account cover distribution. Nothing further.

### 10 Open questions

1. Yes, I meant launching before the funding starts. "All features free during the launch phase, credit on screen" is the right move, and I now recommend it even if revenue were allowed, for the data and the word of mouth. Do not use the word "beta" in the App Store; Apple's guideline 2.2 rejects apps presented as betas or demos. "Launch phase" and "early access" are fine.
2. and 3. Noted; ask.
4. Assumed.
7. Yes: a Business page with a waitlist (email, organization type, team size) and three survey questions. It doubles as evidence for the application.

### Your general notes

- **Accounts.** Stay account-less in v1, but make Pro travel by session: a Pro phone that connects to the companion or to the web viewer makes that session Pro (no credit, no toast); a business license key entered in the companion or the viewer does the same for a machine. The web remote used alone stays free with credit. Design the purchase record so an optional email link can be added later. That answers "the website could never be Pro" without building accounts. The "premium settings unlocked" worry disappears because the PC license only removes the credit; effects are free with credit anyway, so there is nothing on the phone to unlock from a PC.
- **Radically free at launch.** Yes, with four rules: credit from day one, purchase infrastructure built now but hidden, Pro features badged "Pro, free during launch phase" from day one so the later price is no surprise, early users keep Pro. Never introduce a price by taking a feature away; introduce it together with new features.
- **Fun pointers.** Yes: three to five free to seed spread, singles at €0.99 to €1.99, a pack in Pro, seasonal items, and one deliberately absurd luxury pointer at €49.99 or €99.99 as a marketing stunt. Keep the Fun category visually separate so business users never meet a cat pointer by accident.
- **The locking line.** What the audience sees stays free (that is what spreads); what only the payer values is paid; reliability is never paid. The full table is in the monetization file.

## The decisions I would lock this week

1. Connection flow: Concept C (auto-detect, then three cards).
2. Controls: Concept A (tap/hold main zone, actions sheet in the far corner, three shortcut chips, labels toggle).
3. Watches: phone-bridge baseline, relay-direct as a bonus, no watch keyboard mode.
4. Scope: all surfaces before the push; protocol and session model first.
5. Monetization: free launch phase with the on-screen credit; Pro badged from day one and priced in month 3 to 5 with thumbnails, jump and notes; Pro by session; business license key; no accounts; cosmetic pointers.
6. Ambition: the three-phase funded-year plan, with room mode and event mode as the institutional story and on-device transcription with live captions as the Pro+ story.
7. Stipend: Berlin Batch IV now if your incubator accepts solo founders, EXIST as the fallback; exmatriculate only after written confirmation; unpublish the old Pro app at the free launch.

## Files

- `response-connection-flow-and-controls.md`: three flow concepts and the pick, reconnection rules, the presenter screen, watches, web viewer and web remote scope.
- `response-directions-and-ambition.md`: the direction map, deep dives, the funded-year plan with aims and expectations, the application skeleton, follow-up funding.
- `response-monetization-accounts-and-free.md`: accounts, Pro by session, the locking table, the free launch rules, cosmetics, business, the toast, pricing anchors.
- `response-stipend-clarifications.md`: before versus during, BAföG and insurance, Berlin versus EXIST, the trimmed questions.
- `response-build-order-and-launch.md`: build order, launch sequencing, deterrence, the irreversible decisions, timeline.
