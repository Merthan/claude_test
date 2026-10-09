# Build order, launch sequencing, deterrence, and the irreversible decisions

## Accepting the scope

Everything before the launch push: iOS, Android, Wear OS, watchOS, macOS, Windows, web viewer, web remote, server. Linux only if it is nearly free: the clicker part is, because keyboard mode lives on the phone; effects on X11 are feasible; Wayland overlays are hard and not worth your time. Say "Linux: clicker yes, effects on X11" and move on.

The condition that makes this scope safe: build in the order that discovers integration problems earliest, and keep the store submissions free of pieces that are not solid.

## Build order

1. **Protocol and session model, first, before any new client.** One message schema for all controllers (phone app, web remote, watch) and all targets (companion, web viewer). Sessions with several controllers for group mode and an optional "whose turn" lock. Message types: slide actions; the pointer stream with its type; effect on and off; slide state and thumbnails from target to controllers; timer sync; Pro and license signals; pairing by code and by remembered identity; a room code for managed companions. Decide this on paper in a day or two. It is the one decision everything else inherits.
2. **Companion.** Effects, pairing (proximity, code, QR), the connection toast, the license key, hotkey-triggered effects for use without a phone, auto-start, auto-update, managed-mode hooks (a config file with a room name and a no-UI flag, even if the admin page comes later), the notarized Mac build, the Microsoft Store package.
3. **Phone apps, both.** Purchase infrastructure built and hidden, Pro badges on, analytics events defined, string tables for localization from the first screen, group mode, the controls from the UX file.
4. **Web viewer and web remote.** The PDF viewer first; the remote as the second controller client.
5. **Watches.** W1 on both; W2 if cheap.
6. **Linux,** last, if at all.

## Launch sequencing

- **November to December:** closed testing (TestFlight, Play closed testing) with friends and one Reddit call. A minimal iOS submission early still shortens the first real review, even with the keyboard mode treated as given.
- **December or January:** store submissions as free apps with Pro badged and unpriced; companion live on the website and in the Microsoft Store; web viewer live. No "beta" wording in the App Store.
- **Late January to February:** the push (communities, Product Hunt, Show HN, video, German teacher networks), timed to the semester presentation wave. If the watches are not solid by then, push without them and ship them in the first update rather than delaying the push; nobody remembers a watch feature that arrived three weeks later, everyone remembers a launch that crashed.
- **From month one:** university conversations for room mode, and letters of intent.

## Deterrence by breadth

Agreed that breadth deters: a clone on one phone platform with no watch, no web and no companion looks inferior in the store and in any comparison table. The cheap deterrents beyond breadth: a ratings count in the hundreds within three months, localized listings in ten languages, a compatibility page listing tested combinations, a comparison page against the alternatives, Microsoft-signed and notarized companions, a privacy sheet, and the group and room features that need a server a weekend clone will not run. None of these is a moat alone; together they make "I could vibe-code this" visibly false.

## The irreversible decisions (decide now; they cost later if wrong)

1. Package names and bundle identifiers: the Android app keeps the old package (in-place update); the iOS app and the companion get names you will keep for years.
2. The protocol and session model above.
3. Purchase product identifiers, and the free, Pro and Pro+ boundary communicated as "credit from day one; Pro removes it and adds". Never promise "free forever".
4. The purchase record designed for an optional identity later.
5. The credit policy (toast plus effect credit) from day one.
6. The privacy posture: no accounts, no personal data, on-device speech later. It is a selling point for institutions; do not erode it for a metric.
7. Localization infrastructure from the first screen.
8. Analytics events for the funnel from the first build.
9. Installer identities for the companion (a stable MSI product code and PKG identifier) so institutions can upgrade without re-deploying.
10. The old Pro app: unpublish at the free launch, grandfather its buyers.

## Timeline

| When | What |
|---|---|
| October | Founder-service contact and the Berlin application; protocol on paper; companion core; website skeleton with legal pages and the business waitlist |
| November | Phone apps with hidden purchases and group mode; web viewer; minimal iOS submission; closed testing starts |
| December | Web remote; watches; polish; localization; store assets; soft launch if testing is clean |
| January | Store launch (free phase); companion in the Microsoft Store; stipend start if Berlin; university conversations begin |
| Late January to February | The push; the day-90 clock starts at the push |
| March to May | Pro priced with thumbnails, jump and notes; rehearsal analytics; business license live; transcription prototype |

## What I am not sure about

- Whether the protocol can be settled in a day or two. If it takes a week, that week is still the best-spent week of the project.
- The Microsoft Store review time for a tray app with overlay behaviour. Submit early.
- Pushing without watches if they slip: you may prefer to hold the push a week instead. Either is fine; holding more than two weeks is not.
