# Open-source / public-interest funding that pays an individual developer — detail file

Status 31 Oct 2026. Facts come from search summaries citing the official pages (prototypefund.de and nlnet.nl were blocked in the sandbox). Tags: [S] search summary of official page; [M] background knowledge, unverified.

## Headlines
1. **Prototype Fund, Class 03 — your single best "pays the bills" option.** Solo: up to **€47,500 for the 6-month main phase** (≈ €7.9k gross/month) plus an optional 4-month **Second Stage up to €31,667** → up to ~€79,000 over 10 months. Teams of up to 4 (must form a GbR): €95,000 + ~€63,000. **Deadline Mon 30 Nov 2026, 15:00 CET.** Funding starts **1 Jun 2027**. Historic odds ~8 % (avg. 291 applications, ~23 funded per round; Innovation line: up to 30 projects per class). [S]
2. **NLnet is not dead, but it changed.** The NGI Zero Commons Fund (the natural home for accessibility/local-first apps) closed with its final call on 1 Jun 2026; NGI Fediversity closed 1 Aug 2026. The EU successor is "Open Internet Stack". NLnet's **Restack** (1st open call) and **CodeSupply** (supply-chain security) are open: **deadline Tue 3 Nov 2026, 12:00 CET**, grants €5k–50k, individuals eligible, AI-related work generally out of scope. New rhythm: a deadline on the **3rd of every odd month** (next ≈ 3 Jan 2027, derived). Fit for you is narrow: CaptivePortalAutoLogin reframed as open-internet-stack work (RFC 8908/8910 Captive Portal API client). [S]
3. **FLOSS/fund (Zerodha)** — rolling, apply by publishing a `funding.json` manifest; grants reportedly USD 10k–100k; any OSI-licensed project worldwide; repos active Oct 2026. Low effort, worth doing in parallel once something is public. [M]
4. **Not realistic as monthly income** [M]: Sovereign Tech Agency (critical infrastructure only), GSoC / Outreachy / LFX Mentorship (one-off internships on *other* projects, ~USD 1.5k–7k), Open Source Pledge / thanks.dev (donation pools), Aktion Mensch (non-profits only), Mozilla Technology Fund (believed closed). Mozilla Builders (2024: up to USD 100k non-dilutive, local-AI theme) is between cohorts; check https://builders.mozilla.org — if a local-AI cohort opens, the on-device speech engine is a textbook match.

## Prototype Fund in detail
- **Funder/operator:** BMFTR (Federal Ministry of Research, Technology and Space), run by Open Knowledge Foundation Deutschland with DLR Projektträger. €19 m announced for the three lines (18 Aug 2026).
- **Lines (all same money and phases):**
  - **Innovation** — "data security and software infrastructure", up to 30 projects per class.
  - **Resilienz** — "freie Alternativen zu proprietärer, zentralisierter und dominierender Software" (open alternatives to Big Tech); Second Stage application mandatory → designed as a 10-month project.
  - **Up and Coming** — same fields, more coaching; for people who on 1 Jun 2027 are **≤25, or enrolled in a Bachelor/Master, or in an IT apprenticeship** → you qualify through the Master enrolment (confirm wording).
- **Eligibility:** individuals or teams ≤4; 18+; individuals must live in Germany; software only, open-source licence; companies, associations and universities cannot apply. One listing says applicants should be self-employed/freelancers paying tax in Germany (registration timing unclear).
- **Student gotcha:** FAQ applies the **working-student rule** to enrolled students: no full-time project work while studying full-time, **max 20 h/week during the semester**. Whether the amount shrinks pro rata is not stated (20 h × 26 weeks × €50 ≈ €26k, own arithmetic). This collides with using "Up and Coming" via enrolment. Options: ask the Prototype Fund office hour how they treat an enrolled student taking zero modules / a Urlaubssemester; or apply in Innovation/Resilienz and exmatriculate before 1 Jun 2027 (BAföG ends then anyway).
- **Money mechanics:** flat €50/hour recognised (~950 h per 6 months); paid **in instalments in arrears** after payment requests and proof of use → you pre-finance; true grant, no VAT; **taxable income** (EÜR); counts against BAföG (own income above allowance, ~€6,240 per approval period quoted — verify year).
- **Timeline:** applications 1 Oct–30 Nov 2026; formal check + pre-selection, expert jury, then formal application to the ministry; decision date for Class 03 not published (previous cycles: ~Feb/Mar); funding Jun–Nov 2027, Second Stage ~Dec 2027–Mar 2028.
- **Fit of your projects (judgement):** privacy-preserving LLM-analytics extension (ShadowAI open core) = high (data security). On-device speech-coach engine as a reusable library = medium-high (Resilienz: local AI as alternative to cloud AI; ask whether the commercial AnyPresent app may use the funded code — normally yes under the open licence). CaptivePortalAutoLogin = medium (infrastructure, but small; needs a bigger story). Senior phone tool = low-medium (off the stated topics unless framed as reusable accessibility infrastructure).
- **Links:** https://www.prototypefund.de/en/application · https://www.prototypefund.de/en/up-and-coming · https://www.prototypefund.de/en/innovation · https://www.prototypefund.de/en/faq · https://www.prototypefund.de/en/evaluation · https://bewerben.prototypefund.de/ · tax wiki https://wiki.prototypefund.de/index.php?title=Steuern

## NLnet in detail
- **Open now:** Restack 1st open call (2026-11R, "healthy/scalable open internet stack") and CodeSupply (software supply-chain security). Deadline **3 Nov 2026, 12:00 CET**; request €5,000–50,000 (larger grants need a completed earlier grant). NGI Taler status unclear; a planned third programme "ELFA" not yet listed.
- **Eligibility:** individuals, informal groups, companies, foundations (no fiscal host as applicant); "European dimension" is a knock-out criterion (≥60 % of funds to Horizon-eligible countries — Germany is fine); FOSS licence for all software/hardware; proposal in English; AI projects generally out of scope for Restack.
- **Process:** review typically 4–6 months from deadline to announcement (derived); milestone-based payments against invoices, not a salary [M].
- **Funded examples (2025–26):** an Android-alternative OS with long-term support; an Android XMPP client update; AccessKit iOS support. No senior-phone / captive-portal / local-AI example found.
- **Links:** call https://nlnet.nl/news/2026/20260903-call.html · pause notice https://nlnet.nl/news/2026/20260612-NGIZero-stocktaking.html · schedule change https://nlnet.nl/news/2026/20260803-phaseshift.html · https://nlnet.nl/restack/ · https://nlnet.nl/codesupply/ · https://nlnet.nl/propose/ · office hour https://nlnet.nl/officehour/

## Smaller or lower-fit items
- **GSoC 2027** [M]: open to any adult; you work on a participating org's project; stipend ~USD 750/1,650/3,300 by project size (Germany top tier); contributor applications ~Mar–Apr 2027. https://summerofcode.withgoogle.com
- **LFX Mentorship** [M]: 3–6 months, low-thousands USD, mostly cloud/infra. https://mentorship.lfx.linuxfoundation.org
- **Outreachy** [M]: ~USD 7,000 for 13 weeks; eligibility includes "faces under-representation, systemic bias or discrimination in the tech industry of your country", judged by essay (child of immigrants is neither automatic yes nor no); next window probably Feb–Mar 2027; full-time commitment on a host project. https://www.outreachy.org/apply/eligibility/
- **GitHub Accelerator / Secure Open Source Fund** [M]: for existing projects with users; 2026 status unknown.
- **Media Tech Lab (Media Lab Bayern)**: not researched; ask whether Bavarian residence and a media use case are required.
- **Civic Coding / Civic Innovation Platform (BMAS)** [M]: funds organisations/challenges via intermediaries; 2026/27 status unknown. https://www.civic-coding.de
- **netidee (Austria)** [M]: Austrian connection likely required. **Prototype Fund Switzerland**: Swiss applicants; 2026 round closed 6 Sep 2026.
- **Aktion Mensch / Fernsehlotterie / "digitale Teilhabe" programmes** [M]: non-profits only → route = partner e.V. applies and commissions you (plausible for the senior phone tool later).
- **Recurring small income:** GitHub Sponsors, Liberapay, Open Collective; Open Source Pledge and thanks.dev distribute company donations (no application).

## Rules of thumb
- Do not fund the same deliverable twice (NLnet + Prototype Fund).
- Prototype Fund money (Jun–Nov 2027) is incompatible with a running BSS/EXIST stipend (both exclude other living-cost funding) — sequence them: e.g. BSS/EXIST first, Prototype Fund later, or vice versa.
- Settle enrolment/BAföG/health-insurance/tax status (Freiberufler vs Gewerbe) before June 2027.

## Could not verify
Strictness of the Prototype Fund topic filter; Class 03 decision date; recent winners in accessibility/Android/local AI; effect of the 20 h/week cap on the amount; NLnet acceptance rate and next deadline (3 Jan 2027 derived); FLOSS/fund current terms; Mozilla Builders 2026/27; Media Tech Lab rules.
