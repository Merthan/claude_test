# Connection UX: the ladder card

## The fact that simplifies everything

In your architecture the companion does not create a connection. The phone pairs once with the computer as a Bluetooth keyboard and mouse; the companion, when present, reads the vendor collection of that same pairing. So:

- Pairing by Bluetooth is the one setup step for every laptop.
- Installing the companion afterwards changes nothing about pairing; effects, screens and polls appear on the same connection.
- Even without the companion the user has a laser: gyro pointing moves the system cursor, because the phone is also a mouse.
- The companion by code (internet) and the browser viewer are the two backups for computers where Bluetooth pairing is impossible (no Bluetooth, locked-down settings) or where nothing may be installed.
- On a Mac with the companion, the direct link over the local network can later replace pairing altogether, which is how Keynote Remote works.

Every piece of the UX below follows from this. The user never chooses a transport; they climb a ladder, and the app always shows which rung they are on and what the next rung costs.

## The ladder

| Rung | Label the user sees | What they get | What it needs | Delay |
|---|---|---|---|---|
| 1 | Bluetooth clicker | next, previous, black screen via keys, laser as the mouse cursor, timer, log | pair once in the computer's Bluetooth settings | none |
| 2 | Full (companion) | spotlight, magnifier, laser styles, screens, polls, later slide info and notes | the free companion installed on that computer, nothing to re-pair | none |
| 2 on Mac, later | Direct link | everything in 2, two-way data, no pairing at all | companion on the Mac, Local Network permission once | none |
| Backup A | Companion by code | everything in 2 except instant key latency | companion installed, both devices online, one code the first time | slight |
| Backup B | Browser viewer | slides from a PDF, effects drawn in the page, polls, no animations | open anypresent.com/present on the computer, import the file locally, one code | slight |

Backups are labelled as backups and carry the line "Bluetooth is better: no delay, works offline" (A) or "The companion is better: your real slides with animations" (B). That is the "performance limited" signal you wanted, in words that do not sound broken.

## The home screen

One connection card, two buttons, one line.

**The card** shows the current rung with a three-segment bar and one sentence of "next step":

- Not connected: "Not connected" and the segments empty.
- Rung 1: "Bluetooth clicker · Max's MacBook" with one segment filled, and below it "Add spotlight and polls: install the free companion on this computer. No new pairing needed. anypresent.com/get".
- Rung 2: "Full · Max's MacBook" with two segments, and nothing to sell. On a Mac without the direct link, nothing either; do not nag for the third segment, the difference is invisible to most users.
- Direct link: "Direct · Max's MacBook" with three segments.
- Backup A: "Internet backup · Max's MacBook · slight delay" with an orange segment and "Bluetooth is better. Turn it on in both devices and pair once".
- Backup B: "Browser · slight delay · no animations" with an orange segment and "The companion is better for your real slides".

**The buttons:** "Connect by Bluetooth" (primary) and "No Bluetooth? Other ways" (secondary). The secondary opens a sheet with two cards: "Companion by code: for computers without Bluetooth. Install the free companion and enter the code it shows" and "Browser viewer: nothing to install. Open anypresent.com/present on the computer and import your PDF or PPTX locally". Each card is one line and one button.

**The line** under the card, until a companion has ever been seen: "Effects, screens and polls need the free companion. It runs quietly in the background and adds nothing to pairing."

Repeat use: the app tries the remembered rung for the remembered computer on launch and shows the card already filled. A Bluetooth user whose computer is off sees "Max's MacBook not in range" and the two buttons. No menu appears for people who already chose.

## Troubleshooting that routes to the backups

The Bluetooth pairing screen waits with the per-OS steps and a screenshot. After about 30 seconds without a connection it adds, inline, "Not showing up? Try these" with the three fixes for that OS (remove and pair again on Windows, Bluetooth off and on, forget on the phone), then "Or skip Bluetooth:" with the two backup cards. The user who cannot fix Bluetooth in a hurry is two taps from presenting over the internet, which is the outcome you asked for. The card afterwards says "Internet backup · slight delay · Bluetooth is better", so they know to fix it before next time, and the end-of-talk screen repeats that line once.

## The Mac direct link (Phase 1.5)

Discovery is automatic: the companion advertises on the local network, the app finds it, iOS asks the Local Network permission the first time, the card shows "Direct · Max's MacBook". No code, no pairing. If Test 1 in file 01 shows that macOS demands Input Monitoring for the vendor collection, the direct link becomes the Mac data channel and is worth building sooner; if not, it is still the best Mac experience and the reason a Mac user never visits Bluetooth settings. Its one visible requirement, the Local Network prompt, gets one line in the card: "Allow local network so your Mac can be found".

## Settings for start-at-login and always-ready

Both live under Settings, Advanced, so the default user never thinks "this runs all the time, I should turn it off". Each has a short description under the toggle and a confirmation sheet when switched off:

- Start with the computer: "If you turn this off, start AnyPresent on your computer manually before each talk, or your phone will not find it. While idle the app uses about X MB of memory and no measurable CPU." Put the real X from a measurement on hardware; do not print a percentage.
- Internet backup, always ready: "Keeps one idle encrypted connection per paired phone so your phone can reach this computer over the internet. Nothing is sent until a phone connects. If you turn this off, the phone can only reach this computer by Bluetooth or after you open the pairing code here."

The macOS login-item notification ("AnyPresent added as a login item") will appear on its own at first run; mention it in the first-run text so it is not a surprise.

## Stable identity, confirmed

The pairing secret is the identity on both sides, the daily rooms are derived from it, and reconnection needs no code until someone taps "Forget this computer". That is exactly what you want for the 95%: pair once, never again. The one fix is to derive the day from the server's time in `welcome` rather than the local clock (file 01).

## Presenter controls

Your plan stands: a first-run setup with three presets and a drawing of the phone in landscape with a thumb, then UI settings (labels on or off, chip assignments). Suggested preset names: "Simple" (large next and previous, actions in the far corner), "Thumb" (your layout, pointer on the pull-in area), "Classic" (pointer as its own button beside next). Timer: bottom edge, centred in landscape, where neither thumb reaches, and tapping it opens its settings. No gestures, agreed, except what a user deliberately assigns to a chip.

## Website viewer notes

- "Import locally" as the button text, with "Your file stays in this browser. Only your phone's commands travel through our server" under it.
- PPTX accepted with a warning line ("Rendered by the browser: fonts and charts may differ, animations are not shown. For an exact copy, export as PDF") and the three export guides beside it, plus "or install the companion for your real slides".
- No thumbnails before entering, agreed; a typed slide number on the phone is enough for jumps.
- Keyboard shortcuts listed in a footer for the few who want them.
- Polls render inside the viewer page (file 03), so the browser path is not a lesser experience for audiences.

## What I am not sure about

- **The 30-second timeout** on the pairing screen is a guess; it should be long enough that a slow Windows pairing finishes but short enough that a stuck one surfaces the backups.
- **Whether to show the third segment on a Mac at all.** If the direct link is invisible to most users, a two-segment bar everywhere is simpler; decide after you have both working.
- **Preset names** are placeholders.
