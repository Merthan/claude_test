# AnyPresent: context and request for an independent opinion

*Prepared 7 Oct 2026 by the founder (with help from another assistant). Everything here is context, not a conclusion.*

## What I'm asking you for

I'm a solo developer relaunching an old app as a new product called **AnyPresent**. I'd like your **own, independent opinion**: long, detailed and honest. Please think hard about what matters most, challenge my assumptions, and tell me where you'd do things differently.

Other assistants have given me opinions. I deliberately left their estimates and recommendations out of this file so you can judge for yourself. The facts in the appendix were gathered from public sources in late September 2026. Treat them as data you can question or check.

**What I most want your view on:**

1. **Is it worth the effort?** Given the market, the competition and my situation (questions at the end), is building this properly worth months of my time? What would make it worth it, and what would make it not?
2. **Marketing and spread.** How well can this be marketed, and how? I bought **anypresent.com**. My best case: most school and university students use it for free (with a watermark), the name becomes known that way, and money comes from people who pay to remove the watermark and from business users. Is that realistic? What would you do instead or in addition?
3. **Monetization.** My ideas are in "My current ideas" below. What model would you choose, and what would you avoid? How would you get money from business contexts without hurting spread among students?
4. **UX and UI flow.** Especially:
   - how the connection modes should be presented and chosen,
   - onboarding for people who give up quickly,
   - how the phone app and the desktop companion should work together,
   - what the first five minutes should feel like.
5. **Features vs. bloat.** Which features belong in the first version, which later, and which never? Bloat only matters to me if it makes people more likely to skip the app.
6. **Startup or tool.** Could this be a startup, for example with German stipends such as EXIST or the Berliner Startup Stipendium? Or is it better built as a bootstrapped tool? What would make it more fundable?
7. **Name and brand.** Is "AnyPresent" a good name for this product and for the watermark strategy?
8. **Anything I'm not asking but should be.**

Please give your own numbers if you think they help, such as expected users, revenue or timelines, and explain how you got them. Where you're unsure, tell me what data would decide it.

## About me

- Solo developer in Berlin, publishing as "Appless". Currently a university student that finished his Bachelors and has a year they could use however while enrolled officially in the Masters (but not doing courses actively or at all).
- I build fast with LLM-assisted development.
- I think my quality and feature set can beat existing competitors such as PPTControl.

## Product history

- **The old app.** "Bluetooth Presenter [No Setup]", Android, released June 2021, plus a separate paid Pro app at $4.99.
  - The phone pretends to be a Bluetooth keyboard (HID), so nothing has to be installed on the computer.
  - Features: next/previous slide, the phone's volume buttons as clicker with the screen off, vibration timers, black/white screen, laser pointer via trackpad, custom key bindings.
- **Numbers (AppBrain estimates):**
  - About 46,000 lifetime installs of the free app and about 1,200 of the Pro app.
  - Ratings: 3.77★ free (165 reviews), 4.0★ Pro (64).
- **Revenue:** usually €50–100 a month, about €100 at best for a couple of months. A tiny amount also came from ads. Marketing was minimal: a few Reddit posts and free codes.
- **Problems:**
  - It failed to connect on some devices.
  - It was English only.
  - There was no iPhone version, so every interested iPhone user was lost.
  - The app hasn't been updated since late 2023, so Google Play now hides it for using an outdated Android version target. It gets about 38 installs a month.

## Current state (October 2026)

**Built and working as proofs of concept:**

- **iPhone app:** Bluetooth keyboard/mouse mode works on iPhone with nothing installed on the computer. This uses a workaround that other App Store apps (Bluetouch, btkbd) also use.
- **Gyro pointing** (moving the pointer by moving the phone, like Logitech Spotlight) works very well.
- **Desktop companion** in Rust, one codebase for macOS and Windows (Linux possible but ignored for now). It runs as a tray app.
  - On-screen effects work: **spotlight** (darkens everything except a circle around the pointer) and **magnification**.
- **Bluetooth HID with a vendor channel:** besides normal keyboard/mouse input, the phone sends a custom signal (currently "mouse button held down") that the companion uses to trigger effects.
- **Volume buttons as clicker on iPhone** work technically, but Apple may reject it (guideline 2.5.9). On-screen controls are good without it.

**Not built yet:** anything that uses the internet (relay, website fallback).

**Infrastructure decided:** Cloudflare Workers, free plan at first and the $5/month plan later. I've already checked this is sufficient, so **please don't recalculate it**.

**Domain:** anypresent.com bought. TMview and DPMAregister show no entries for "AnyPresent".

## Planned connection modes

The phone app should always find a way to connect:

1. **Direct iPhone ↔ Mac** link (another connection method between Apple devices), when available.
2. **Bluetooth GATT**, a direct data connection to the companion, when the companion is installed.
3. **Bluetooth HID**, the phone as keyboard/mouse with nothing installed. This is the fallback when the companion isn't installed or GATT fails.
4. **Internet relay** through Cloudflare with code pairing. For when Bluetooth doesn't work, which is common: it often breaks when the phone or laptop is also connected to headphones or fitness trackers. This needs the companion.
5. **Website fallback** on anypresent.com.
   - For computers where nothing can be installed and Bluetooth fails, or where someone wants the effects without installing anything.
   - The user opens their file in the browser. PDF is recommended; PPTX and Google Slides via PDF export also work.
   - The phone controls it over the internet, and effects are drawn in the browser.
   - The file is processed locally in the browser.
   - Animations aren't supported in this mode; I found no project that renders them well enough.

## My current ideas (not decided)

**Monetization**
- Mostly free at the start to reach as many people as possible.
- Later price increases, with grandfathering of earlier buyers.
- **Watermark "AnyPresent"** (possibly the web address) while spotlight or magnifier mode is on. Removing it costs a bit more than the basic paid features.
- Earlier ideas: a cheap 7-day pass for one-off presenters, student discounts, possibly class or club codes.
- Getting money from business contexts in some way.

**Growth**
- The watermark is seen by every audience.
- Teachers recommending it to students; students seeing it at other students' presentations.
- Short videos of the effects, including fun pointers that might spread on social media.
- Pitching it as an alternative to buying a physical presenter.

**Possible features**
- The companion reads the .pptx and sends speaker notes to the phone or a smartwatch.
- Automatic transcripts with slide changes time-stamped.
- More effects (blur, ring, fun pointers).
- Smartwatch control (Wear OS, Apple Watch).
- Possibly a separate "mouse & keyboard, nothing to install" app later, cross-promoted.

**My views so far**
- AI feedback on presentation quality is far-fetched for me (no training data, LLM output not reliable enough).
- Whatever is most likely to benefit the product should be implemented. Bloat is not bad unless it makes less people download or pay for the app. "all-in-one presentation suite" is in theory possible but you need to judge if that direction makes more sense. 

## What I'm unsure about

- Whether this is worth the effort compared with other uses of my time.
- How big this can realistically get, and what limits it most.
- Whether the free-with-watermark strategy spreads the way I hope, and whether it hurts conversion or professional use.
- How to price: free vs cheap vs higher prices later, one-time vs subscription, what to charge businesses.
- The right UX for five connection modes without confusing people.
- Which features to build first, and when bloat starts to hurt. Or if bloat is required to make it startup-able. 
- Whether to apply for stipends first (and possibly not sell before that) or launch and sell directly.
- I could add a "website" version for the controls too which only uses the relay and sends them to the viewer website or the companion too, not sure if this is worth it though (maybe as a basic limited version that might help it spread?) 

## Appendix: facts gathered (late Sep 2026, please verify)

### Competitors and alternatives

**Presenter apps and built-in remotes**
- **PPTControl** (Android, iOS, Apple Watch): needs a desktop app.
  - About 3,700 Android installs a month, ~160k lifetime.
  - Rated 3.1★ on Android, 3.9★ on iOS (24 US ratings).
  - $4.99/month, $19.99/year or $49.99 lifetime.
  - Redesign on 2 Sep 2026 that advertises better connection stability.
- **Samsung PPT Controller:** free, for Galaxy Watch, ~1,700 installs a month, 4.3★. Since Android 15 it only works with Samsung phones.
- **WowMouse / WowMouse Presenter** (Doublepoint, watch gestures): removed in 2026 after Oura bought Doublepoint (March 2026). The paid Presenter app had ~580 installs.
- **Free alternatives:** Keynote Remote (Apple); Remote for Slides, a Chrome extension with 100k users.
- **Removed presenter apps:** Microsoft Office Remote (~2.2M installs), Remote for PowerPoint Keynote (~710k), Clicker Presentation Control (~290k).

**Nothing-to-install keyboard/mouse apps**
- **Appground "Bluetooth Keyboard & Mouse":** Android only.
  - About 100,000 installs a month, 9.7M lifetime, 4.3★ (45.8k ratings).
  - Presenter Mode is a paid feature.
- **Bluetouch:** Android ~330k lifetime; iOS 3.6★ from 168 ratings; $6.99 lifetime or $19.99/year.
- **btkbd:** iOS, 15 ratings, $3.99.

**PC remotes that need a desktop program**
- **Remote Mouse:** ~73,000 installs a month.
- **Unified Remote:** ~14M lifetime installs. Its Swedish company filed revenue of SEK 953k for 2025.

### Hardware and desktop tools

- **Amazon US:** the top 10 presentation clickers sell about 30,000 units a month together, mostly at $10–20. "Presentation clicker" gets ~7,700 searches a week (asinsight estimates, Aug 2026).
- **Logitech Spotlight:** ~500 units a month on Amazon US at $119.99. Its highlight effect needs Logitech's desktop software.
- **Logitech Spotlight 2** (June 2026): $129.99 / €129.99, from ~€105 in Germany.
- **Cheap clickers:** €8–16.
- **Desktop effect tools:** Microsoft PowerToys and ZoomIt (free); Presentify $14.99 (Mac); PointerFocus $12.50 (Windows).
- **"Best presentation remote" roundups** found in 2025–26 don't mention phone apps.

### Platforms

- **iOS share of mobile web traffic**, Aug 2026 (Statcounter): US 60.7%, Germany 27.5%, worldwide 32.4%.
- **RevenueCat "State of Subscription Apps 2026"** (all subscription apps): 17.3% of new apps reach $1k monthly revenue within two years, and 4.6% reach $10k. The median app earns ~$72/month one year after launch.

### Store and channel rules

- **Apple guidelines:**
  - 2.3.7: no prices, trademarked terms or other apps' names in titles, subtitles, screenshots or previews.
  - 2.5.9: apps that alter the volume buttons' function may be rejected.
  - 4.3: no near-duplicate apps.
- **Apple offer codes** support one-time unlocks, up to 1M codes a quarter.
- **Google Play:**
  - Promo codes are limited to 500 a quarter.
  - A paid app made free can't go back to paid.
  - Google suspends related developer accounts together.
- **Deal sites** (MyDealz and the Pepper network, Slickdeals) ban developers posting their own deals but friends have an account they could post from.

### Schools and universities

- In Germany, GDPR compliance largely decides whether teachers may recommend an app.
- Some university help pages recommend Remote for Slides or Keynote Remote for controlling slides from a phone.
- Reported trend: US colleges moving toward oral exams and in-class presentations because of AI-written homework (Fortune, April 2026).

### Stipend rules

**EXIST Gründungsstipendium**
- Solo founders and teams of up to 3.
- €1,000/month for students who have completed at least half their coursework, €2,500 for graduates, for 12 months.
- Plus up to €10k for costs (solo) and €5k for coaching.
- At least one founder needs a degree; teams made up mostly of students are funded only in exceptional cases.
- Business activity must not have started when the project begins.
- "Modifications of existing products without significant unique selling point" are excluded.
- About 55% of applications submitted by universities are approved.

**Berliner Startup Stipendium**
- Up to €2,500/month per person for up to 12 months, through incubators. Some incubators require teams and a degree.
- Students only in their final semester.
- Not possible after EXIST.
- The business must not be trading yet.

### Name check

- SlideMate is a registered class-9 trademark.
- SlidePilot, SlideWand and Slidekick are already used by presentation tools.

## Questions for the founder

*Answers filled in before sending.*

1. Do you already have a university degree (e.g. a bachelor's)? When do you expect to graduate?
Yes, a bachelors in Wirtschaftsinformatik
2. How many hours a week can you put into this over the next 6–12 months?
I don't think it would take 6 months to get it running but 40h, already after a week I came pretty far, all of these POC were from just a week and due to being an android developer that side (and WearOS) should later take much less time too
3. What do you want from this project: income, a portfolio for future startups, learning, or a real company? In what order?
My previous app with ~50.000 downloads was already a nice number for portfolio, so I guess MOSTLY income, POSSIBLY a real company/startup. 
4. What would make the effort "worth it" for you: a monthly revenue level, a user count, a stipend?
Each one of these high enough would make it worth it
5. Android: will you reuse the old native Android code, build a new native app, or use a cross-platform framework? Must Android launch at the same time as iPhone?
I decided against cross platform now because the app needs MAINLY native code and the shared UI or payment stuff is easily translateable with LLMs without using e.g. Flutter (which I considered at the start, but doesn't make sense here)
6. Watches: which watches, and are they needed at launch?
I guess it would be better if I already have watches at the start? I have a WearOS 2 watch which I would use for testing, and I'd like the program to work on most Apple Watches, maybe Series 5 and up - connection either directly through wifi/https with my server relay or with the phone companion inbetween. 
7. Which connection modes work today, and on which computers and operating system versions have you tested them?
Windows MacOS both - iOS HID (+optional vendor data) and the old Android app HID (no vendor data, but should work too)
Additionally I tested if a e.g. 100-2000ms delay (over internet, which I likely won't even have) would be very bad and IT WOULDNT, so the internet mode should work perfectly fine.
8. Is the direct iPhone ↔ Mac link built or planned?
Planned but should be easy
9. Which features does the iPhone app have today: timers, black screen, jump to slide, notes?
iPhone was just a POC, LLM could build most of these pretty easily. Syncing slides for a reliable "jump to slide" (where e.g. 20 back events need to be sent) might be harder (or not compatible with all programs). Notes is not implemented but server allows communication between companion and app, so companion could read e.g. pptx, extract notes per slide and send those to phone (bluetooth should also work for that).
10. What does the current UI flow look like, from install to first slide change?
UI is not finalized but in general because volume button controls MIGHT not be allowed on Apple App Store those would be added later in an update (with a risk of being rejected, but its not a dealbreaker if volume buttons dont work).
In general the gyro/laser functionality works very well and its activated by long pressing a part of the screen (which resets the gyro to 0, even changing the rotation works flawlessly). If you imagine the phone held in a relaxed way on the side, The place where the thumb is closest to (top right corner) would be next slide, moving the thumb towards your arm would be the place you hold for laser control/spotlight while held. So the two important actions are easiest to press, screen is in a very dimmed/minimal state. MAYBE notes are added later to the bottom of the landscape mode if required and MAYBE laser just starts with a "next slide" long press instead (requiring no additional thumb movement). Previous slide is on the bottom, harder to reach because its pressed more rarely. 
11. Which markets and languages first: Germany, the US, other EU countries?
All I guess
12. Do you plan accounts or logins, or should everything work without one?
I dont think accounts/logins make sense. Unlocking "No Watermark" etc. should just be extra data sent by the phone (where the purchase happened)
13. Do you have any marketing budget, or is everything organic?
I could spend some but probably organic. I wouldn't want to spend over 200€ but 0 is better unless 200€ get me much further
15. Is there anyone who could join: co-founder, marketing help, testers?
I dont think so, but yes testers I could easily find through friends or reddit
16. What is your legal setup today (e.g. small business registration)? Did the old app's ads or sales run through it?
None currently
17. Is there a target launch date, e.g. before a semester starts?
No, no target. But I can easily be done before december I assume if I want
18. Would you be willing to work full-time on this for 12 months if a stipend paid for it?
Yes
