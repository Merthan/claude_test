# AnyPresent briefing 04: Monetization and pricing

## Short answer

Free core, one one-time Pro unlock, one cheap short pass, and business licenses sold on the desktop side where Apple's and Google's cuts and volume-purchase limits do not apply. No subscription at launch, no ads ever, no accounts, nothing paywalled on the connection paths. Business money and student spread do not conflict because they are the same product with a different checkout: students keep the free tier with the watermark, businesses buy an invoice-able license for their machines. Confidence: high on the structure, medium on the exact prices.

## Principles that follow from the product's usage pattern

1. **People present a few times a year.** A tool used episodically converts badly to subscriptions and well to one-time purchases and moment-of-need passes. PPTControl's $4.99 a month is the thing students complain about; do not copy it.
2. **Never paywall reliability.** The connection ladder (keyboard mode, companion, relay, direct link) is the trust feature. A user whose Bluetooth failed and who then hits a paywall for the relay leaves a one-star review. The relay cost on Cloudflare is negligible at your scale, as you have checked.
3. **The free tier must be genuinely good.** Clicker, gyro laser, black screen, timer, and the effects with a small watermark. If the free tier feels crippled, ratings fall and the spread stops.
4. **The paid reason must be visible to the user and to the audience.** No watermark, more effects, later notes and watch. The watermark is the conversion lever for anyone who presents to people they want to impress.
5. **No accounts** (you are right). Purchases live in the store account; the phone tells the companion "Pro". For businesses, the license lives on the computer instead.

## The catalogue I would launch with

| Item | Type | Price | What it unlocks |
|---|---|---|---|
| Free | | €0 | All connection modes, next and previous, start and end show, black screen, gyro laser, timer with vibration, spotlight and magnifier with the "anypresent.com" credit |
| AnyPresent Pro | Non-consumable in-app purchase | €9.99 standard; €5.99 for the first two to three months as a launch price, announced as such in the paywall | No watermark, extra effects (ring, blur, fun pointers), custom key bindings, and everything added later (notes, jump to slide, watch) |
| 7-day pass | Apple: non-renewing subscription; Google: a managed product consumed on purchase | €1.99 | Pro for seven days, for the thesis defence, the wedding speech, the one conference talk |
| Business license | Sold on the website for the desktop companion, via a merchant of record (Paddle or Lemon Squeezy) | €29 per computer one-time, or €15 per computer per year; packs of 5, 20 and 100 with discounts; invoice with VAT handled by the merchant of record | Removes the watermark and unlocks Pro features for every phone that connects to that computer; later adds custom branding (your logo instead of ours) and an MSI or PKG for IT deployment |

Why these prices: the anchors are an €8 clicker, a $49.99 PPTControl lifetime, and a €130 Logitech Spotlight. €9.99 one-time sits under "cheap clicker plus shipping" and far under the alternatives, and your old $4.99 bought a clicker without effects. If conversion holds above 2% at €9.99, test €12.99 after six months. One-time purchases cannot have store introductory offers, so the launch price is simply a lower price for a period; say "launch price until March" in the paywall copy, and when you raise it, everyone who bought keeps it automatically. That is your grandfathering, and it costs nothing.

## Why not subscription-first, and when to add one

Subscription revenue dominates app-store income across the industry, and the RevenueCat numbers you quote are about subscription apps. But those numbers describe apps people use weekly. A clicker used in March and again in November churns at the first renewal and earns the resentment that shows in PPTControl's ratings. Expected revenue per user from a €9.99 one-time purchase at 2% conversion is higher than from a €19.99 annual plan that only 0.5% of students accept and 60% cancel.

Add a yearly plan ("Pro+") only when you have a feature with ongoing cost or ongoing value: transcripts, cloud features, or a business feature set that is updated continuously. Not before. Keep the one-time Pro available alongside it forever; removing it is what breaks trust.

## Getting money from business without hurting students

The trick is that the watermark is drawn by the companion, so the unlock can live on either end:

- Consumers unlock on the phone (store purchase). The phone tells the companion "no watermark".
- Businesses unlock on the computer (website license). The companion tells every connecting phone "this machine is licensed".

Either signal removes the watermark. This gives you four things at once: an invoice-able purchase (companies cannot expense in-app purchases easily and Apple's volume purchase program does not cover in-app purchases at all), no 15 to 30% store cut on business revenue, a natural "classroom license" (the teacher's laptop is licensed, every student phone that connects is clean), and a product for IT departments (installer, no accounts, no telemetry, a privacy sheet).

Apple's rule 3.1.3(b) explicitly allows an app to honour features acquired on other platforms or your website provided the same items are also available as in-app purchases in the app. Pro is, so this is allowed. What is not allowed is advertising the website purchase inside the iOS app (3.1.1 and 3.1.3). The companion and the website can advertise it freely; the phone app simply shows "Licensed by this computer". The EU's Digital Markets Act loosens some of this inside the EU, but you do not need to rely on it.

Later business features, only if inquiries arrive: custom branding on the spotlight, MDM-friendly installers, a status page for IT, transcripts with slide timestamps (doc 06). Do not build any of these before someone asks.

## Students, discounts and class codes

Do not create a student SKU; the free tier is the student discount. For a class, club or course where a teacher wants every student clean, give the teacher codes:

- iOS: Apple offer codes support one-time unlocks and up to a million codes a quarter. Generate a batch per class in App Store Connect.
- Android: Google caps promo codes at 500 a quarter, which is too few for classes. License the teacher's laptop through the companion instead, which covers Android and iOS phones alike.

Selling Apple offer codes for cash outside the app is a grey area; use them as free marketing (which is their purpose) and route paid classroom business through the companion license.

## Android specifics: the old apps

- **Update the old free app in place** (same package name) and rename it. You keep ~46,000 installs' worth of history, the existing installed base receives the update, and the listing's keyword history survives. Google will show it again once it targets a current Android version. A fresh listing starts from zero on all three. Medium confidence that this beats a fresh listing; the risk is the old 3.77-star average, which recency weighting will overtake within a few months of good reviews.
- **Grandfather the old Pro app's ~1,200 buyers**: the new app can check whether the old Pro package is installed and signed with your key, and unlock Pro automatically. Keep the Pro app listed but pointed at the new app, then unpublish it after a year. A paid app cannot be made free and back, so do not touch its price.

## Store mechanics you should set up on day one

- Apple's App Store Small Business Program and Google's 15% tier: both bring the cut to 15% below one million dollars a year. Enrol before the first sale.
- Regional pricing: accept the stores' automatic equalization, then lower the price tiers in India, Brazil, Turkey and Indonesia if installs there are high and conversion is near zero.
- Prices in the paywall should show the local currency the store reports, not a hard-coded euro figure.

## What to avoid

- **Ads**, including in the free tier. Your old app's ad revenue was tiny, ads kill professional use and teacher recommendations, and they create GDPR work for nothing.
- **A mandatory subscription for the basic clicker.** It is the single fastest way to a 3-star rating in this category.
- **Paywalling any connection mode.** Reliability is the brand.
- **A separate paid app.** It splits ratings and search, risks Apple's duplicate-app rule 4.3, and cannot be reversed on Google.
- **Accounts or your own license-key entry inside the iOS app.** Apple's 3.1.1 forbids your own unlock mechanisms; keep license keys on the desktop side.
- **Lifetime deals on third-party deal sites at steep discounts.** They attract users who never present and dilute the price anchor. Free codes to real communities are fine.

## Expected revenue mix after a year (guess, to be replaced by data)

Roughly 60% one-time Pro, 25% passes, 15% business licenses. If business is above 30%, build the branding and IT features. If passes are above 40%, your pricing of Pro is too high relative to the pass.

## What I am not sure about

- **€9.99 versus €7.99 versus €12.99** for Pro. I would launch at €5.99 as the launch price and move to €9.99, then test. The pass at €1.99 may cannibalize Pro; if more than 40% of revenue is passes, raise the pass to €2.99 or shorten it to 72 hours.
- **Whether businesses buy at all.** No evidence either way. Offer the license with a one-page sheet and count inquiries for six months.
- **App Review's consistency** on honouring a desktop-side license in the iOS app. The rule allows it; individual reviewers vary. Keep the wording in the app neutral ("Licensed by this computer") and never mention a price or a website.
- **The in-place Android update** could confuse some existing users. A single "What's new" screen explaining the rename handles most of it.
