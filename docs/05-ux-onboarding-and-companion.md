# AnyPresent briefing 05: UX, onboarding, and how the phone and the companion work together

## Short answer

The user never chooses between five connection modes. The app chooses, shows one status line, and asks at most one question: "Can you install something on that computer?" The first five minutes must deliver a working slide change in under 60 seconds with nothing installed, then softly offer the companion for effects. The companion is the "pro half" of the product: small, trustworthy, auto-updating, the keeper of effects, relay pairing, licensing and later notes. Everything below is about removing the moments where people give up. Confidence: high on the principles, medium on the specific screens.

## The connection ladder is an implementation detail, not a menu

Internally you have five paths. The user should see three words and a traffic light.

| Internal mode | What the user sees | When it is used |
|---|---|---|
| Direct iPhone to Mac link | "Connected to Max's MacBook" | Companion installed, both Apple, nearby. Fastest and most reliable; use it whenever it exists |
| Bluetooth GATT to the companion | "Connected to Max's MacBook" | Companion installed, any OS, nearby |
| Internet relay | "Connected to Max's MacBook via internet" | Companion installed and Bluetooth is unavailable or fails, or the user is far away |
| Bluetooth keyboard (HID) | "Keyboard mode: nothing installed" | No companion found; works with any computer, including school PCs and Chromebooks |
| Web viewer | "Presenting in the browser" | Started from the website, for computers where nothing can be installed and the file can be opened in a browser |

Rules:
- The app scans for a companion (Bluetooth advertisement, local network, and a remembered relay identity) for a few seconds on launch. If found, it connects. No question asked.
- If nothing is found, it offers keyboard mode as the primary button, and the companion as the secondary "want spotlight and more?" link. One screen, two choices, no explanation of GATT or HID anywhere.
- If a companion connection drops during a talk and the companion is online, the app switches to the relay silently and the status line changes colour for a second. No dialog, ever, during a presentation.
- A manual override lives behind a tap on the status line: "Use internet instead", "Pair as keyboard instead", "Forget this computer". Nobody needs it on day one; power users and your support replies do.
- Remember computers. The second launch should be: open app, already connected, present.

Keyboard mode is one-way: the phone cannot know whether the key arrived. Companion and relay are two-way. Design the UI for that honestly: in keyboard mode show "sent", in companion mode show "received". A "Test connection" button before a talk makes this explicit, and is the thing nervous presenters want most.

## The first five minutes, as a script

Goal: first slide change within 60 seconds of opening the app, with nothing installed. Target: 60% or more of new users reach it within five minutes. Measure the time to first key sent.

1. **Screen one (5 seconds).** One sentence: "Control any presentation from your phone." One primary button: "Connect to a computer". One small link: "Just look around first" that opens the presenter screen in a demo state with no connection, so the impatient see what they would get before they do anything.
2. **Scanning (3 to 5 seconds).** "Looking for AnyPresent on nearby computers". If a companion is found, tap it and you are done. If not: "No companion found on nearby computers" with the primary button "Pair as a Bluetooth keyboard (nothing to install)" and the secondary "Install the free companion for spotlight and more", which shows anypresent.com/get and a QR code. A tertiary "I have a pairing code" covers companion users whose Bluetooth is off.
3. **Keyboard pairing (30 seconds).** The user picks the computer's icon (Windows, Mac, Chromebook, Linux). The app shows the exact three steps for that OS with a screenshot, and waits. The phone knows when the host connects, so the screen flips to "Connected. Press next to test" on its own. No "done" button.
4. **First success.** The presenter screen with a one-time overlay: "Tap here for next slide. Hold here for the laser." Then nothing else until the user has changed a few slides.
5. **The soft upsell, after success, not before.** A dismissible card on the presenter screen: "Want the spotlight and magnifier? Install the free companion on your computer", with the link. Shown once, then available in settings. No paywall before the first successful session, ever.

Permissions: ask for Bluetooth at the moment of pairing with a one-line reason. Nothing else at onboarding. No notification permission, no rating prompt, no account, no email.

## Onboarding for people who give up quickly

The drop-off points in this category, in order: Bluetooth pairing fails or the computer does not show the phone; the user does not know where the computer's Bluetooth settings are; the phone is still paired to a previous computer; the user expects the phone to control slides but a different window has focus on the computer. Each needs a one-screen answer in the app:

- A diagnostics screen the user can reach from the status line: Bluetooth on or off, paired to something else, host OS tips ("On Windows, remove AnyPresent in Bluetooth settings and pair again"), and a one-tap switch to internet mode when a companion exists.
- A "Before you present" checklist shown once: Do Not Disturb on the phone (a WhatsApp banner mid-talk is the number one professional embarrassment), screen brightness, battery, and "click into your slide show on the computer once".
- Never block. Every screen has a way to skip, and the demo state exists for people who want to see first and set up later.

## The companion's role and its own first run

The companion is optional for slide control and mandatory for effects, relay, licensing, notes and jump-to-slide. Position it as the free upgrade, not as a requirement.

First run on the computer: download, open, two things on screen: "Open AnyPresent on your phone. This computer will appear as 'Max's MacBook'" and a pairing code with a QR code for internet pairing. A "Try the spotlight" button shows the effect immediately, which is the wow moment and the reason to keep it installed. Then it lives in the tray or menu bar with a status dot, effect toggles, "Test effects", "Pairing code", and "Check for updates". Start at login by default, because people forget to start it before a talk and blame the app.

Pairing by proximity should be the default and should need no code. The QR or code path is the fallback for internet mode and for the first pairing when Bluetooth is off. Pairing once should be enough: the phone remembers the computer, the companion remembers the phone, and the relay identity is stable so reconnection over the internet is automatic.

Licensing lives on both ends (doc 04): the phone says "Pro", the companion says "licensed"; either removes the watermark.

Permissions on the computer: ask only when needed. macOS needs an accessibility permission only if the companion simulates key presses (not in keyboard mode, where the phone is the keyboard). Screen-overlay effects need none. Explain each permission in one line at the moment it is needed.

Distribution: notarized Mac download plus Homebrew; Windows via the Microsoft Store (free signing, no SmartScreen warning, IT departments can deploy it) plus a direct download and winget (doc 09).

## The presenter screen

Your layout is right: thumb-first, next slide where the thumb rests, laser and spotlight hold under the thumb, previous slide at the bottom because it is rare, a dimmed minimal screen, landscape with room for notes later. Keep it. Additions:

- One status line at the top with the three-word connection state and the colour dot. Tapping it opens the override and diagnostics.
- Timer with vibration alerts, big enough to read at arm's length, with a rehearsal mode.
- Haptics on every press, because a physical clicker gives a click and the phone must feel at least as certain.
- Black screen as its own button, because it is the second most used function in real talks.
- Effects as a mode you hold, not a mode you toggle, matching how Logitech does it. Holding is also what makes the "mouse button held" vendor channel natural.
- Android: volume buttons and screen-off mode as you have them. iOS: no volume buttons at launch (doc 02).

## Mid-talk resilience

Everything that goes wrong during a presentation must be handled without a dialog. The relay fallback is silent. A lost keyboard pairing shows a red dot and a one-tap "Reconnect". The app keeps the screen on and ignores rotation. Incoming calls are the user's problem, but the checklist told them.

## The website viewer and the web remote

Treat these as a separate product surface with its own entry point, not as mode five of the phone app.

- **Viewer**: the user opens anypresent.com/present on any computer, drops in a PDF (recommended) or a PPTX exported to PDF, gets a full-screen presentation with a pairing code. Effects are drawn in the page, which is easier than any OS overlay. Animations are not supported, and the page says so once.
- **Web remote**: the phone opens anypresent.com/remote, enters the code, gets next, previous, black screen, a touch laser, and a timer. The phone's browser can even do gyro pointing with the device-orientation permission. This is the "nothing to install anywhere" flow, and the funnel into the app ("Get the app for Bluetooth, screen-off and volume buttons").
- The phone app also controls the viewer, so app users get the viewer for free as their school-PC answer.

Keep the viewer out of the phone's onboarding and in the "trouble connecting" path and on the website. It is also your platform-risk hedge: it depends on no Apple or Google behaviour at all.

## Watches (later)

A watch is a remote for the phone, not for the computer. The phone stays the bridge in all modes; the watch sends next, previous and black screen, shows the timer, and vibrates on timer marks. Design the phone protocol now so that a second controller (watch, web remote) can attach without changes.

## Things to avoid in the UX

- A mode picker with five options and technical names.
- Any explanation of Bluetooth profiles anywhere.
- A paywall, rating prompt or permission request before the first successful slide change.
- Dialogs during a presentation.
- A companion that needs admin rights or opens a big window on every start.
- Making the volume-button feature a visible promise on iOS before Apple has accepted it.

## What I am not sure about

- **Which default to lead with when no companion is found.** I chose keyboard mode because it delivers success in 60 seconds and matches your "No Setup" identity. The counter-argument is that it is the fragile path on iOS and gives no effects; if App Review or iOS updates make it unreliable, lead with the companion instead.
- **Auto-scanning for a few seconds on every launch** could feel slow to repeat users. Remembered computers should connect in under a second; if they do not, skip the scan.
- **The "Just look around first" demo state** might reduce the share of users who pair at all. Measure it; drop it if it hurts.
