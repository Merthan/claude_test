# Connection flow, presenter controls, watches, and the web surfaces

## 1. Who connects from where (this decides the flow)

| Situation | Share of presentations (my guess) | Bluetooth on the computer? | Can install? | Best path |
|---|---|---|---|---|
| Own laptop at university or work | 50 to 60% | yes | yes | Companion over Bluetooth; keyboard mode as the quick start |
| Lecture-hall or school desktop PC | 20 to 30% | often no (desktops), sometimes yes | no | Website viewer now; room mode later (companion pre-installed by IT, pairing by code) |
| School laptop or a borrowed laptop | 10 to 15% | yes | usually no | Keyboard mode; website viewer |
| Video call from own computer | growing | not needed | yes | Companion; effects show in the shared screen |
| One-off (speech, wedding, borrowed machine) | about 5% | varies | no | Keyboard mode; web remote |

Two consequences:

- "Nothing to install" is not universal either. Desktop PCs without Bluetooth sit in exactly the rooms students fear most. The website viewer, and later room mode, are the answer there, so the menu must show the website option rather than hide it.
- Pairing by code over the internet is a backup for laptops, but for room PCs it is the only companion path. There the phone is on mobile data and the PC is on wired LAN, so neither side depends on the room's WiFi. Your own 100 to 2,000 ms tolerance test covers the latency.

## 2. Three concepts for the flow

### Concept A: the explicit menu (your direction)

One screen, three cards, one line each, a button each:

- **Bluetooth clicker.** "Nothing to install. Works with any computer that has Bluetooth. Next, previous, black screen, laser." Button: "Pair now".
- **Companion (recommended).** "Free app for Mac and Windows, under 5 MB, starts with your computer. Adds spotlight, magnifier, notes and more. Connects by Bluetooth, or by code over the internet as a backup." Buttons: "Find my computer" and "Get the companion".
- **Website.** "For computers you cannot install on. Open anypresent.com/present on the computer, drop in a PDF, enter the code here. No animations." Button: "Enter code".

Below the cards: "Not sure which? Tap here", opening a help sheet with a paragraph per card and a two-question picker ("Your own computer?" and "Can it run Bluetooth?").

Pros: honest, teaches the model in ten seconds, maps one-to-one onto store screenshots, costs nothing to build. Cons: every first-time user makes a choice before their first success, and the word "companion" needs its line of explanation.

### Concept B: situation questions

"Where will you present from?" with "My own computer" or "A computer I can't install on", then the matching cards. Pros: matches how people think about the problem. Cons: a second screen before success, and the user often does not know whether the room PC has Bluetooth, so the website card has to be shown anyway. In practice it is Concept A with one extra tap.

### Concept C: auto-detect, then Concept A (recommended)

On open, scan for about three seconds for a remembered or nearby companion (Bluetooth advertisement, local network, remembered relay identity). Found: connect and show the presenter screen. Not found: show Concept A's menu with the Companion card marked "recommended" and one hint line, "Already installed? Start AnyPresent on your computer". Repeat users with a companion never see the menu. First-time users see an honest menu. Keyboard-mode users see it once and are remembered.

| | A | B | C |
|---|---|---|---|
| Taps to first success, first time, own laptop | 2 to 3 | 3 to 4 | 2 to 3 |
| Taps on the second use with a companion | 1 | 2 | 0 |
| Teaches the model | yes | partly | yes |
| Cost | lowest | low | low |
| Main risk | none | choice fatigue | a 3 s scan on the first run |

Recommendation: C. It keeps your explicit flow and makes the common case, second use with a companion, zero taps.

Copy and placement details:

- **First-run intro:** two screens at most, both skippable. Screen 1: "Your phone is the remote. Works with every computer, nothing to install." Screen 2: "Even better with the free companion: spotlight, magnifier, notes." The menu then repeats the same explanations under the cards, so the intro is deliberate redundancy, not the only place the model is explained.
- **Internet pairing** lives inside the Companion card as "Connect by code". The companion shows the code and a QR in its window. Never call it "internet mode" at the top level.
- **The Mac direct link:** no question. The Mac companion advertises on the local network and over Bluetooth; the phone uses the direct link when it sees it.
- **Keyboard mode fails on a given machine:** the pairing screen has "Not showing up?" with the three per-OS fixes, then "Use the companion instead" and "Use the website instead". That is the whole fallback story, and it is explicit, which is what you wanted.

## 3. Reconnection for the 95%

1. The phone remembers the last computer per mode and tries it on launch, silently, as part of the scan.
2. The companion starts with the computer by default. Its first run says, in one line: "Starts with your computer so your phone finds it next time. Change in settings." Most people will never quit it. Those who do get the hint on the phone.
3. Keyboard mode: the host remembers the pairing, the phone just advertises again. If Windows dropped the pairing, the per-OS fix screen says "remove it in Bluetooth settings and pair again". Nothing cleverer.
4. By-code pairing: the companion and the phone each keep a stable identity. After the first pairing, the relay reconnects them without a new code whenever both are online. The code is only for the first time or after "Forget this computer".
5. Mid-talk: no automatic mode switching. The status dot turns red and a "Reconnect" button appears. The first tap retries the same mode; a second tap offers the menu. The presenter decides.

Any more logic serves the 5% and costs the 95% in confusion and you in time.

## 4. After the first presentation

A card on the end-of-show summary after the first completed keyboard-mode session: "That worked. Want spotlight and magnifier next time? The free companion is under 5 MB, starts with your computer and uses almost nothing. anypresent.com/get". Shown twice at most, then it lives in the menu. The end-of-show summary (time, slides, "how was the connection?") is also the natural home for the rating prompt and for the "how did you hear about us?" question.

## 5. Presenter controls

What a presenter does, by frequency: next (constant), pointer hold (frequent for some, never for others), previous (occasional), black screen (occasional), timer glance (constant but passive), everything else (rare, mostly before the talk or once).

Design rule: the first two must work blind; everything else may need a glance.

### Concept A (recommended): one main zone, one actions button, three shortcut chips

- **Main zone, where the thumb rests.** Tap = next. Hold = pointer, with the gyro zeroed at the moment the hold starts, as you have it. A press shorter than about 250 ms sends next on release; a longer press starts the pointer without sending next; releasing a hold never sends next. The cost is that next arrives on release rather than on press, roughly 100 ms later than a press-triggered next, which is not perceptible in a talk. A setting "Separate pointer button" splits the zone for people who hate it or who want the pull-in area for the pointer.
- **Previous.** The smaller zone at the bottom, as you have it.
- **Actions button.** The hard-to-reach corner (bottom right in landscape, where exit is now). It opens a sheet: Black screen, White screen, Start show, End show, Pointer type (Laser, Spotlight, Magnifier, Fun…), Timer (start, reset, marks), Jump to slide (later), Settings, Exit. Exit does not deserve its own corner; the system gesture does it and the sheet has it.
- **Three shortcut chips** along the top edge or the far edge, each an item from the same sheet. Defaults: Black screen, Pointer type toggle (Laser to Spotlight), Timer start and stop. Configurable in settings from the sheet's items. Chips show an icon and a label. After the first completed talk, a one-time hint offers "Hide labels". Labels stay on by default because first-timers need them.
- **Timer** at the top, large; tapping it opens its settings. **Status line** with the three-word connection state and the dot.
- **Pointer type is chosen on the phone and sent with every hold.** The companion renders what it is told and holds no per-presenter preferences. This matters for room mode later, where the PC is shared and must not hold anyone's settings.
- **Android screen-off mode:** volume up = next, volume down = previous, long press volume up = black screen toggle. No pointer with the screen off.

### Concept B: separate pointer button plus a gesture layer

Pointer under the thumb's pull-in position, next at the thumb rest, previous at the bottom, swipe down anywhere = black screen, two-finger tap = actions sheet. Pros: fully blind operation for power users. Cons: discoverability for first-timers, accidental black screens, and hard to explain in one screenshot. Not v1. Possibly a "blind mode" toggle later if users ask.

Why A: it keeps the thumb still for the two frequent actions, it shrinks the screen to three zones and three chips, it degrades gracefully with labels for first-timers, and a single store screenshot can explain it.

## 6. Watches

Three architectures:

- **W1, watch as a remote for the phone (baseline, both platforms).** The watch sends next, previous, black screen and pointer-type toggle to the phone; the phone forwards them over whatever mode is active, including keyboard mode. This is the only way a watch can drive a no-companion setup. The phone app must be running: on iOS, WatchConnectivity wakes the phone app in the background and the Bluetooth peripheral keeps running under its background mode; on Android, a foreground service. All setup, pairing and purchases happen on the phone. The watch shows "Set up on your phone" until then, which answers your worry about configuring anything on a watch screen.
- **W2, watch talks to the relay directly (bonus).** When the companion is in use, the watch app connects to the relay itself over the phone's connection or over WiFi and LTE, so the phone can stay in a bag. Both watch platforms can open a WebSocket. If the protocol is designed once, this is a second client, not a new system.
- **W3, watch as a Bluetooth keyboard to the PC (Wear OS only).** Possible in principle, fragile in practice: watch Bluetooth stacks, pairing a watch to a PC on a watch screen, a second connection next to the phone's. Apple Watch cannot do it. Not v1; revisit only if Wear OS users ask loudly.

Recommendation: W1 at launch on both platforms, W2 if the protocol makes it a day's work, W3 not unless demand is loud.

Watch UI at launch: next (large, most of the screen), previous (swipe or a small zone), black screen, timer with vibration marks, connection dot. Nothing else. Notes on the watch arrive with notes on the phone.

Installation: iOS bundles the watch app with the phone app. Wear OS ships as its own build under the same Play listing's Wear form factor, installable from the watch's store or prompted from the phone app. You need a real Apple Watch (Series 5 or later, used) to test; the simulator will not tell you about WatchConnectivity and Bluetooth reliability.

## 7. Website viewer: scope

- **Input:** PDF as the recommended format, with a ten-second "Export as PDF" guide for PowerPoint, Keynote and Google Slides (three screenshots). PPTX rendering in the browser is a fidelity trap (fonts, SmartArt, charts, embedded media). If you accept PPTX at all, render it with a clear warning; I would ship PDF-only first and count how many people ask for PPTX.
- **Privacy line:** the file never leaves the browser; only control messages travel through the relay. Say so on the page. It is your GDPR sentence for schools.
- **Features:** full screen; pairing code and QR on the first screen; a thumbnails grid for jump-to-slide (easy in the viewer, hard elsewhere, and it makes the viewer better than a plain PDF reader); black and white screen; laser, spotlight and magnifier drawn in the page; timer on the phone; keyboard shortcuts for local use so the page is a decent PDF presenter on its own, which is what will rank in search; group mode with several controllers.
- **Credit** shown unless a Pro phone is in the session or a license key is entered (see the monetization file).

## 8. Website remote: how far to go

- **Parity on controls:** next, previous, black, white, touch laser, gyro laser through the device-orientation permission, spotlight and magnifier hold, pointer type, timer, thumbnails when the viewer is the target.
- **Not included:** Bluetooth, volume buttons, screen-off, settings sync, purchases. Credit always, unless the session is already Pro through a Pro phone or a license.
- **Its three jobs:** the zero-install-anywhere path (web remote plus web viewer), the funnel ("Get the app for Bluetooth, screen-off and your watch"), and guests in group mode: a group member without the app joins by code from a browser. The third job is why it belongs in v1.
- Build it as a controller endpoint of the same protocol as the watch and the phone app.

## What I am not sure about

- The 250 ms tap-and-hold threshold. Test with your own grip; 200 to 300 ms is the usual range.
- The share estimates for presenting contexts are guesses; the first "where did you present from?" survey replaces them.
- Whether W2 is worth it at launch depends on how clean the protocol is; if it is more than two days, defer it to the first update.
- PPTX in the browser: demand may be higher than I think among school users who cannot export; count the requests.
