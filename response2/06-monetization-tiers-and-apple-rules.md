# Monetization: the catalogue, badging, feedback for discount, Apple's rules, the sibling app's relay

## Clarifying what I meant about effects and the credit

The standard effects (laser styles, spotlight, magnifier, the screens) are free with the credit drawn by the companion or the viewer. Pro removes the credit and adds the bounded extras. Additional effects, fun pointers and cosmetic packs are separate purchases that everyone pays for, Pro included, exactly as you intended. The web viewer is Pro whenever a Pro phone is in the session; the web remote used alone is always the free tier. We agree; the earlier wording was ambiguous.

## The catalogue

| Product | Price (placeholders to test) | What it contains | Why it exists |
|---|---|---|---|
| Free | €0 | every connection mode, next and previous, screens, timer, standard effects with the credit, polls up to 50 voters, the presentation log (last five talks), group mode, watch basics, three fun pointers | spread; everything the audience sees |
| Pro, one-time | €9.99, €6.99 at launch | no credit, custom shortcuts and presets, edge styles and extra standard effects, log history, the 7-day pass at €1.99 as its sibling | the €8 buyer: "as good as a clicker, no watermark", bounded forever |
| Pro+, subscription | €3.99 a month or €24.99 a year, Pro included | transcripts and overviews, slide info for PowerPoint and Keynote, unlimited audience, exports, prepared poll sets and quiz mode, themes, priority support | the user who presents weekly: unbounded, ongoing-value features that keep arriving |
| Pro+ Lifetime | €79 to €99 | Pro+ as it exists plus future updates, excluding features with ongoing server cost | the €200 user who hates subscriptions; priced at about four years of the yearly plan |
| Cosmetics | €0.99 to €1.99 each, €4.99 packs, seasonal items; the stunts at €99 ("My face, I don't know why you'd buy this") and €399 ("You have too much money") | pointers and effects seen by the room | fun, social video, and the occasional headline; kept visually apart from the business products |
| Business, license key | €15 a seat a year or €39 a seat once, packs with discounts, invoice | no credit on licensed companions and viewers, Pro+ per seat, deployment packages, a human to email | companies and trainers who expense software and never buy in-app |
| Institution and Event | from the pilots | room mode, admin page, event mode | later |

Three consumer products plus cosmetics is the limit. A fourth tier confuses the paywall, costs you review cycles, and the power-user population in this niche is too small to segment further. The gap between the €8 and the €200 user is captured by Pro+ Lifetime plus cosmetics plus, for the real power user, a business seat.

## Badging and the "take away" rule

Fine: features that are new go behind Pro or Pro+. Fine: features that are free in the launch phase and badged "Pro, free during the launch phase" get priced later; nobody is surprised. Not fine: removing something a user had, unbadged, without a perk. The badge from day one is what makes "take away" into "the launch phase ended", and early users keep what they had through the early-user perk. Launch-phase copy: "Everything is free while we launch. Early users keep Pro."

## Feedback for a discount

"Give feedback after five talks, get 50% off Pro" is allowed and good. Mechanics:

- **iOS:** Apple offer codes support consumables, non-consumables and non-renewing subscriptions since iOS 16.3 (expanded at WWDC25), with custom codes at a discounted price and a quota of a million codes a quarter. Create a custom code at the discounted price and show it after the form is submitted. Note that Apple is retiring the old promo codes for in-app purchases as of March 2026; offer codes are the mechanism now.
- **Android:** a second, discounted Pro product unlocked locally after the form, or a Play promo code (500 a quarter, enough for feedback givers).
- **Never tie it to a store rating.** Both stores forbid incentivized ratings. The discount is for your own form.

## Apple's rules 3.1.1 and 3.1.3(b), explained for your design

What 3.1.1 governs: the mechanisms the iOS app itself uses to unlock its own features. Inside the app, features may be unlocked only by in-app purchase; the app may not accept license keys, codes, QR scans or similar to unlock anything. Reviewers do apply this to license-key entry fields in apps, and forum reports show them rejecting product-key unlocks even when the developer cited 3.1.3(b).

What 3.1.3(b) governs: an app may let a user use features they bought on another platform or on your website, provided the same features are also sold as in-app purchases in the app. Reviewers apply it narrowly, and the pattern they accept most reliably is an account login (username and password), not a key.

Your design under these rules:

1. The iOS app unlocks Pro and Pro+ only through in-app purchase. No key field, no code field, nothing.
2. The companion is a desktop app outside the App Store. Whether it draws a credit is its own business; a license key entered there is a desktop license. Apple has no rule about what a Mac tray app draws.
3. The web viewer is a web page; same.
4. The phone shows "Licensed by this computer" as information only, and the phone's own Pro features (shortcuts, log history, transcripts) stay locked unless bought in the app. Nothing on the phone changes because of the desktop key, so 3.1.1 never comes into play.
5. If you ever want a business seat to unlock phone-side features too, do it under 3.1.3(b) with an account-style sign-in (the optional email link discussed before), and only while the same features exist as in-app purchases. Expect a reviewer to ask; have the answer ready.
6. Do not link from the iOS app to the website's business page or prices. Since May 2025, apps on the United States storefront may link to web checkout, and the EU has its own rules, but your design does not need either and relying on them adds review risk for no gain.

So the sentence "it sounds like it wouldn't be allowed" comes from reading 3.1.1 as governing other platforms. It governs the iOS app's own unlocks, and the design never does one outside the store.

## Switching platforms

Repurchasing after a switch from Android to iPhone is normal and the stores expect it. The optional email link can fix it in year two for the few who care. Nothing to do now beyond keeping the purchase record ready for an optional identity.

## The keyboard and mouse sibling and its relay

Arithmetic at Cloudflare's rates (incoming messages at a twentieth of a request, requests at about $0.15 per million beyond the included million):

- A mouse at 60 updates a second is 216,000 messages an hour, so 10,800 requests, so about $0.0016 an hour.
- A thousand users at twenty hours a month is 216 million requests, about $32 a month.

Not "very costly" in money, but it is unbounded usage that a free tier should not carry. Decision: the sibling app ships Bluetooth-only; if people ask for an internet mode, it becomes a Pro+ feature capped at 30 updates a second. The relay protocol and the session code are already shared, so adding it later is a switch, not a build.

## What I am not sure about

- **All price points** are placeholders; the launch phase is for learning them.
- **Pro+ Lifetime** sells well in deal communities and can cannibalize the yearly plan; keep it slightly uncomfortable (four years of yearly) and watch the mix.
- **Reviewer consistency** on the informational "Licensed by this computer" line. It unlocks nothing, so I expect no issue; if a reviewer objects, drop the line, since the companion behaves the same without it.

## Sources checked

- Developer-forum readings of 3.1.1 versus 3.1.3(b), including a rejection of product-key unlocks and the acceptance of login-based access: https://developer.apple.com/forums/thread/740710 and https://developer.apple.com/forums/thread/713044 and https://developer.apple.com/forums/thread/825551
- The May 2025 United States storefront change on external purchase links: https://ptkd.com/journal/apple-rejection-3-1-1-in-app-purchase-links
- Offer codes for all in-app purchase types, custom codes, quotas, and the retirement of promo codes for in-app purchases: https://developer.apple.com/documentation/storekit/implementing-offer-codes-in-your-app.md and https://developer.apple.com/documentation/storekit/supporting-offer-codes-in-your-app.md and https://aso.dev/app-store-connect/monetize/
