# Seeds of Fortune Talk — Continuation Brief
**Last updated:** May 3, 2026 (session 9 — v4.2 executed)
**Talk date:** Monday, May 4, 2026 (Zoom, ~45 min)
**Audience:** ~40 high school juniors, majority women, at Yale
**Topic:** Information asymmetry as a lens for capstone projects

---

## STATUS

**v4.2 executed AND browser-verified in place on `akerlof-lemons-v4.html` (Session 9, 2026-05-03).** All six R12–R17 revisions applied. STEPS reduced 16 → 15 (z0 deleted) with c12 (abstraction) reordered before c11 (Carfax). Capital step (i0) reframed around trust+institutions; iPhone step (p0) FixCard expanded with the upstream-pricing-power mechanism; new CrisisCallout component renders below i0's FixCard with the Great Depression / 2008 / MBS-ratings beat. JSX compiles cleanly; render-dispatch simulation confirms all 15 steps render the expected components in the expected order. **Chrome MCP came online mid-session after Rick installed the extension and served the file via `python3 -m http.server`** — full visual click-through completed; one bug caught and fixed during verification (markdown asterisks rendering literally → added `formatEmphasis` helper). v3.0 remains the fallback. **Talk is tomorrow (Mon May 4); v4.2 is shipping.**

---

## WHY V4.0 EXISTS — THE CORE INSIGHT

v3.0 opened with mechanics ("flip these cards, click this offer button") before the student had any reason to care. Rick re-framed the talk around a **problem-first opening**: you've inherited $20K from your rich uncle, you need a car, you open Facebook Marketplace. Now everything downstream answers a question the student is already asking.

Five locked-in design moves drove the restructure:

1. **Problem-first hook.** Inheritance + need + Marketplace listings. The student is the protagonist from second one.
2. **Repair-cost framing for car tiers.** Don't assert tier values; derive them from "how much does it cost to bring this car up to mint?" Mint $0, Good $6K, Fair $12K, Lemon $18K. Values to you: $20K / $14K / $8K / $2K.
3. **Symmetric ignorance baseline first.** Before introducing asymmetric information, work out what happens if NEITHER side knows. The contrast IS the lesson.
4. **The market doesn't fail; it freezes.** The Lemon market still works. What's destroyed is allocational efficiency — good cars stuck with sellers who'd rather sell, buyers stuck with cars they don't want. Name "allocational efficiency" explicitly. It matches the academic register Seeds of Fortune is trying to cultivate.
5. **Carfax as entrepreneurial opportunity.** Not just "the fix" — an entrepreneur saw an information problem and built a business that profits while restoring market function. "Profit motive pointed at a real problem produces social good as a by-product." The good side of economics.
6. **"It wasn't about the lemons" — the pedagogical reset.** After 20 min of lemons/cars, slow down and reframe. The whole point is that this pattern transfers. iPhones and capital markets are then APPLICATIONS, not more stories.

---

## THE 17-STEP SPEC

Step structure is grouped into 7 acts. Each step listing below includes everything needed to build it: headline, narrative (~final copy), insight box copy, render kind, parameters, and component to use.

### Act 1 — Your Problem (Steps 1–4)

**Step 1 — `c0` (NEW kind: `hook`) — The Inheritance**
- **Headline:** "Your rich uncle just died."
- **Narrative:** "He left you $20,000. You're sad — but you also need a car. You pick a make and model you want, and you do your homework. A mint-condition one is worth $20,000. You can afford exactly one good car. You open Facebook Marketplace."
- **Insight:** none on this slide (let the hook breathe)
- **Component:** NEW `HookSlide` — minimal visual. Money icon ($20,000), arrow, blank car icon. Could include a Marketplace logo at the bottom. Quiet, sets the stage.
- **Parameters:** none

**Step 2 — `c1` (NEW kind: `population`) — The Population**
- **Headline:** "What's actually out there"
- **Narrative:** "Of cars of this model on the used market, here's what your research tells you: 1 in 4 is mint condition. 1 in 4 needs about $6K of repairs to bring it up to mint. 1 in 4 needs $12K. 1 in 4 needs $18K. The cars are out there in equal numbers across these four tiers."
- **Insight:** "Average value across the population: $11K. ($20K + $14K + $8K + $2K) / 4. This number will matter in a minute."
- **Component:** NEW `PopulationView` — 4 cars side by side, each with: condition label (Mint / Good / Fair / Lemon), repair cost tag ($0 / $6K / $12K / $18K), and "value to you" tag ($20K / $14K / $8K / $2K). Use existing `CAR_TIERS` data and `TIER_STYLES` colors.
- **Parameters:** activeTiers: [0,1,2,3], infoMode: 'fixed' (show all values labeled)

**Step 3 — `c2` (NEW kind: `listings`) — The Listings (the puzzle)**
- **Headline:** "What you actually see on Marketplace"
- **Narrative:** "You browse Facebook Marketplace and find four cars of your model. Every single seller is asking $20,000. The listings look identical. The photos are similar. The descriptions are similar."
- **Insight:** "Three of these cars aren't worth $20K to anyone who has to do the repairs. Why is everyone asking the mint price? Because the seller knows what they have, and you don't. (Hold this thought — we'll come back to it.)"
- **Component:** NEW `MarketplaceView` — 4 identical gray car silhouettes, each with a "$20,000" price tag below. Maybe a subtle Facebook Marketplace-style frame. Visually FLAT (deliberately uniform) to contrast with Step 2's varied population.
- **Parameters:** none

**Step 4 — `c3` (existing kind: standard step with `LotCalculation`) — Symmetric Ignorance + Economist's Offer**
- **Headline:** "What if no one knew?"
- **Narrative:** "Let's start with a thought experiment. Suppose the sellers don't know what they have either — they're as in the dark as you. Each seller would expect their car to be average value: $11K. So you offer $11K. Sellers accept (it matches their own expectation). It's a fair coin toss across all four cars."
- **Insight:** "This is the BASELINE: a market with symmetric ignorance. Everyone's guessing. Nobody has an information advantage. We'll see what happens here, then change ONE thing."
- **Component:** Existing `TokenGrid` + `LotCalculation`, infoMode: 'symmetric', offer: $11K
- **Parameters:** activeTiers: [0,1,2,3], infoMode: 'symmetric', offer: 11000, showCalc: true

### Act 2 — The Burn (Steps 5–6)

**Step 5 — `c4` (existing kind: `spin`) — Spin at $11K**
- **Headline:** "Try it. Offer $11,000."
- **Narrative:** "Click 'Offer $11,000.' A seller at random accepts (because in symmetric ignorance, all four are equally likely to take your offer). What did you actually get? Click again. And again."
- **Insight:** "On AVERAGE, $11K is fair. But you don't get to average across many draws — you only get one car. Run the spin a few times. Notice you almost never get the 'average' outcome — you either overpay or underpay, often by a lot. Variance is the lesson."
- **Component:** EXISTING `SpinExperience`, BUT MODIFIED — change offer button from $20K to **$11K**. Update the running tally framing from "naive buyer" to "rational buyer at the average price." See "MODIFICATIONS TO EXISTING COMPONENTS" section below.
- **Parameters:** none (spin is self-contained)

**Step 6 — `c5` (existing kind: `lossViz`) — Loss-viz + Bankruptcy Callout**
- **Headline:** "What $11K actually buys you"
- **Narrative:** "The four equally likely outcomes side by side. Two of them feel okay — Mint and Good leave you with cash to spare. Two of them hurt — Fair and Lemon leave you with a car you cannot afford to fix."
- **Insight:** "Important wrinkle: you started with $20K. After paying $11K for the car, you have $9K left. Mint needs $0 repairs (✓). Good needs $6K (✓ — $3K to spare). Fair needs $12K (✗ — short $3K). Lemon needs $18K (✗ — short $9K). 2 of 4 outcomes leave you with an un-driveable car. Variance with a bounded downside is much worse than the textbook 'expected value = $0' suggests."
- **Component:** EXISTING `LossVisualization`, MODIFIED — add a bottom-bar "affordability" indicator on each of the 4 outcome bars (✓ green or ✗ red), and a bankruptcy callout at the bottom. See "MODIFICATIONS" below.
- **Parameters:** none

### Act 3 — The Sellers Wake Up + Cascade (Steps 7–10)

**Step 7 — `c6` (existing kind: standard) — Sellers Wake Up; Mint Walks**
- **Headline:** "Now flip ONE thing: sellers know what they have."
- **Narrative:** "Same setup. Same four cars. Same $11K offer. But now each seller knows the value of their car. Watch what happens. The Mint owner says: 'My car is worth $20K — I'm not selling it for $11K.' Walks away."
- **Insight:** "This is **information asymmetry** — the seller knows; you don't. One word change in the rules, and the entire dynamic of the market shifts."
- **Component:** Existing `TokenGrid` + `LotCalculation`, infoMode: 'seller', activeTiers: [1,2,3] (Mint walks)
- **Parameters:** activeTiers: [1,2,3], infoMode: 'seller', offer: 11000, showCalc: true

**Step 8 — `c7` — Good Walks; Pool is Fair + Lemon, Avg = $5K**
- **Headline:** "Good walks too. The pool you're drawing from changed."
- **Narrative:** "The Good owner does the same math. 'My car is worth $14K. I'm not selling for $11K either.' Walks. Now the only sellers who'd accept your $11K are Fair and Lemon. The pool you're actually drawing from has an average value of $5K — and you're paying $11K for it. Expected loss: $6K. Plus a 50% chance of the un-fixable Lemon."
- **Insight:** "Your offer didn't draw a random sample. It systematically attracted the worst. Economists call this **adverse selection**."
- **Component:** Existing `TokenGrid` + `LotCalculation`, infoMode: 'seller', activeTiers: [2,3]
- **Parameters:** activeTiers: [2,3], infoMode: 'seller', offer: 11000, showCalc: true (with new pool average displayed)

**Step 9 — `c8` — You Revise to $5K; Fair Walks**
- **Headline:** "You're not stupid. You revise your offer."
- **Narrative:** "If the pool is now Fair and Lemon, the new fair price is $5K. So you offer $5K instead. The Fair owner says: 'My car is worth $8K — no thanks.' Walks."
- **Insight:** "Each rational revision drives out the next-best seller. The market isn't 'failing' randomly — it's unraveling along a predictable information fault line."
- **Component:** Existing `TokenGrid` + `LotCalculation`, infoMode: 'seller', activeTiers: [3], offer: 5000
- **Parameters:** activeTiers: [3], infoMode: 'seller', offer: 5000, showCalc: true, showSpiral: true

**Step 10 — `c9` (NEW kind: `frozen`) — The Lemon Market Works; Everything Else is Frozen**
- **Headline:** "The Lemon market is the only one that works."
- **Narrative:** "Lemon sellers and Lemon-tolerant buyers find each other at $2K. That trade happens. Both sides walk away happy. But every other potential trade has stalled. The Mint owner is stuck holding a car they wanted to sell. The Good owner is stuck. The Fair owner is stuck. You're stuck shopping in the Lemon market when you'd rather have a Mint."
- **Insight:** "The market hasn't disappeared. The GOOD market has frozen. Nobody's bleeding on the floor — there's just an entire layer of trades that should have happened and didn't. That's the cost. And it's invisible if you're not looking for it."
- **Component:** NEW `FrozenMarketView` — left side: Lemon traded ($2K, ✓ trade happened, both happy). Right side: Mint, Good, Fair sellers each shown stuck holding their car, with greyed-out arrows toward absent buyers ("would have paid $20K / $14K / $8K"). Visually the contrast between "1 trade happens" and "3 trades blocked" is the message.
- **Parameters:** activeTiers: [0,1,2,3] (show all 4, but only Lemon is "active/traded")

### Act 4 — The Diagnosis (Step 11)

**Step 11 — `c10` (NEW kind: `concept`) — Allocational Efficiency**
- **Headline:** "Allocational efficiency"
- **Narrative:** "One of the central jobs of a market is to move goods to whoever values them most. When that happens, both sides walk away better off, and the economy as a whole is richer because nothing is sitting in the wrong hands. That's allocational efficiency. Asymmetric information breaks it. The good cars don't reach the buyers who want them. Capital doesn't reach the companies that would deploy it best. The economy is poorer not because resources don't exist, but because they can't find their way to the right hands."
- **Insight:** "Hold this concept. It's the lens for everything that comes next. Markets aren't just for buying and selling — they're a sorting mechanism. When the sorting breaks, real value disappears."
- **Component:** NEW `ConceptCard` — primarily typographic. Big phrase "Allocational Efficiency" centered, definition below, then a clean diagram: a Mint car icon flowing along an arrow to a buyer icon (the trade that should happen). Maybe a faded version of the same arrow ghosted to show the trade that ISN'T happening because of asymmetric info.
- **Parameters:** none

### Act 5 — The Fix as Opportunity (Step 12)

**Step 12 — `c11` (existing kind, modified content) — Carfax: Information Problem as Business Opportunity**
- **Headline:** "Carfax saw the problem and built a business."
- **Narrative:** "In 1984, an entrepreneur looked at the used-car market and saw an information problem worth solving. They built a database of vehicle histories — accidents, ownership, service records. For about $40, a buyer can pull a full history. Carfax got rich. The market got better. Both buyers and Mint sellers won."
- **Insight:** "Every information problem is a business opportunity in disguise. Carfax found one in used cars. Profit motive pointed at a real problem produces social good as a by-product. **This is the good side of economics.** It's also a hook for your capstones — wherever you find an information problem, you've found a potential business."
- **Component:** Existing `FixCard`, MODIFIED text. Keep the visual structure (icon + cost tag + before/after), update the copy to match the entrepreneurship framing.
- **Parameters:** activeTiers: [0,1,2,3], infoMode: 'fixed', showFix: true

### Act 6 — The Abstraction (Step 13)

**Step 13 — `c12` (NEW kind: `abstraction`) — It Wasn't About the Lemons**
- **Headline:** "It wasn't about the lemons."
- **Narrative:** "For the last 20 minutes we've been talking about lemons. About cars. About $20K and Carfax and Mint condition. **It wasn't about the lemons.** It wasn't about cars at all. The problem was: one side knew, and the other didn't. The fix was: making the knowledge shared. Cars are just where this pattern is easiest to see. Once you know what to look for, you'll see it everywhere."
- **Insight:** none — the slide IS the insight. Let it land.
- **Component:** NEW `AbstractionSlide` — visually striking. Big quiet typography. "It wasn't about the lemons." in serif, large. Sub-text smaller. Strip away decoration. Let it breathe. This is the talk's pivot moment.
- **Parameters:** none

### Act 7 — Applications + Capstone (Steps 14–17)

**Step 14 — `p0` (existing kind: standard, with seller-knows token grid) — iPhones**
- **Headline:** "Same pattern: used iPhones."
- **Narrative:** "Used iPhones on Marketplace. Battery health is the hidden quality. One seller has a phone with 42% battery health — nearly dead. They know. You can't tell from photos. Same structure as cars: hidden quality, posted price doesn't reveal it, market would unravel without a fix."
- **Insight:** "Apple built the fix INTO the device — Settings → Battery → Battery Health. The seller can't fake it in real time. Free for the buyer. Why did Apple do it? Self-interest. Resale value of old iPhones protects pricing power for new iPhones. **Aligned incentives.** Same logic as Carfax — solving the information problem creates value, and the solver captures some of it."
- **Component:** Existing `TokenGrid` + `LotCalculation`, then `FixCard`. Use `PHONE_TIERS`. Keep tight — this is now an APPLICATION, not its own narrative arc.
- **Parameters:** section: 'phone', activeTiers: [0,1,2,3], infoMode: 'seller' → 'fixed' (one combined step), offer: 425, showCalc: true, showFix: true
- **NOTE:** This used to be 2 steps (p0 + p1). Compressing to 1 because it's now an application of the principle, not a narrative.

**Step 15 — `i0` (existing kind: standard) — Investment Capital**
- **Headline:** "Same pattern: $20M stakes."
- **Narrative:** "Four companies seeking investment capital. Management knows their true financial prospects. Investors see the pitch deck — not the real books. Same structure. Same unraveling. Same need for a fix. The Securities Exchange Act of 1934 mandated that public companies file audited financial statements, GAAP-compliant, reviewed by independent CPAs. Information became standardized, mandatory, verifiable."
- **Insight:** "The fix costs a public company $100K to $10M+ per year in audit and compliance. Carfax was $40. Why so much more? Because the trades being unblocked are enormous — capital flowing to the right companies, jobs being created, retirement savings being deployed. The cost of the fix scales with the stakes."
- **Component:** Existing `TokenGrid` + `LotCalculation` + `FixCard`. Use `INV_TIERS`. Like Step 14, compressing 3 prior steps (i0/i1/i2) into 1.
- **Parameters:** section: 'investment', activeTiers: [0,1,2,3], infoMode: 'seller' → 'fixed', offer: 11, showCalc: true, showFix: true

**Step 16 — `z0` (existing kind: cost escalation) — The Cost of the Fix Scales with the Stakes**
- **Headline:** "The fix costs what the trades are worth."
- **Narrative:** "Three markets. Same underlying problem. Three very different solutions. $40 for a Carfax report. Free for Battery Health. $100K to $10M+ per year for a public company's compliance. The economics is identical — only the price tag of the fix changes."
- **Insight:** "When you see information infrastructure that looks expensive — auditors, rating agencies, compliance officers, financial data services — that's not waste. That's the price of trades that wouldn't otherwise happen. Allocational efficiency at scale."
- **Component:** Existing `CostEscalation` panel (log-scaled bars). Update caption text per the new framing.
- **Parameters:** showEscalation: true

**Step 17 — `z1` (existing kind: capstone) — Capstone Connections**
- **Headline:** "What's the information problem in your capstone?"
- **Narrative:** "Each of your four capstone topics is, at its core, an information problem. Look at them through this lens and you'll see new questions. New angles. Maybe new businesses."
- **Insight:** Per-topic hooks below.
- **Component:** Existing `CapstoneConnections`. UPDATE per-topic copy to match the lens we just built. New copy:
  - **Topic #1 — Recessions, Credit, and the Financial System (🏛):** "Lenders can't directly see which borrowers will repay. Credit scores, employment data, and recession signals are the information infrastructure. In a downturn, that infrastructure gets noisier — and good borrowers get worse rates or no loan at all. Allocational efficiency cracks under stress."
  - **Topic #2 — Investment Banks & Capital Markets (🏢):** "An IPO is an information event. Investment banks exist partly to bridge what the company knows about itself and what investors can verify. Research desks, roadshows, audited financials, ratings — every piece is information infrastructure. Without it, only the most desperate companies could raise capital."
  - **Topic #3 — Fintech (📲):** "Fintech is largely the business of solving information problems at scale. Credit scoring on thin-file borrowers. Fraud detection. Robo-advisor disclosure. Mobile banking that brings underserved customers into a system that can verify them. Every fintech company is an answer to 'what couldn't we measure before?'"
  - **Topic #4 — Housing Finance & Structured Credit (🏠):** "Lenders can't see borrower quality directly — credit scores, appraisals, MBS ratings exist to make hidden information shared. When that infrastructure misjudges (think 2008), allocational efficiency collapses dramatically. The trades that DO happen end up moving capital to the wrong borrowers."
- **Parameters:** showCapstone: true

---

## MODIFICATIONS TO EXISTING COMPONENTS

### `SpinExperience` (lines 438–685 in v3.0)
- Change offer button label from "$20,000" to "$11,000"
- Change offer amount logic from 20000 to 11000
- Update tally framing: "Offers / Fair deals / Overpaid" stays, but the *meaning* of "fair" changes. At $11K, "fair" = paying ≤ value-to-you. So:
  - Mint draw ($20K value, paid $11K) = bargain (gain $9K) — LABEL: "BARGAIN"
  - Good draw ($14K value, paid $11K) = bargain ($3K gain) — LABEL: "BARGAIN"
  - Fair draw ($8K value, paid $11K) = overpaid ($3K loss) — LABEL: "OVERPAID"
  - Lemon draw ($2K value, paid $11K) = badly overpaid ($9K loss) — LABEL: "OVERPAID"
- Result card text: "You paid $11K. The car is worth $X to you. [Bargain/Overpaid] by $Y." Plus a smaller line about repair affordability.
- Reset behavior unchanged.

### `LossVisualization` (lines 687–840 in v3.0)
- Reframe headline ("$11K offer" not "$20K offer")
- 4 outcome bars: pay $11K, get $20K/$14K/$8K/$2K → net +$9K / +$3K / -$3K / -$9K
- Add new layer below each bar: affordability indicator
  - Mint: "$0 repairs needed" ✓ green
  - Good: "$6K repairs, $3K cash to spare" ✓ green
  - Fair: "$12K repairs, short $3K" ✗ red
  - Lemon: "$18K repairs, short $9K" ✗ red
- Bottom callout box: "2 of 4 outcomes leave you unable to fix the car you bought. Even though you 'broke even on average,' real-world variance has a bounded downside."

### `FixCard` (lines 865-882 + FIX_DATA at 841-864)
- Update the car/Carfax card text to match Step 12's entrepreneurship framing
- Visual structure unchanged

### `CostEscalation` (lines 883-925)
- Caption update only — see Step 16
- Bars unchanged (log-scaled $40 / free / $100K-$10M+/yr)

### `CapstoneConnections` (lines 927-948)
- Replace per-topic copy with the Step 17 wording above
- Topic icons (🏛 📲 🏠 💳) — wait, the brief uses 🏛 🏢 📲 🏠 but v3.0 uses 🏛 📲 🏠 💳. Reconcile to 🏛 🏢 📲 🏠 (Recessions, Capital, Fintech, Housing).

---

## NEW COMPONENTS TO BUILD

| Component | Step | Purpose |
|---|---|---|
| `HookSlide` | 1 | Inheritance setup, minimal visual |
| `PopulationView` | 2 | 4 cars with repair-cost + value-to-you tags |
| `MarketplaceView` | 3 | 4 identical silhouettes, all $20K listings |
| `FrozenMarketView` | 10 | Lemon traded vs. 3 stuck sellers |
| `ConceptCard` | 11 | Allocational efficiency definition + diagram |
| `AbstractionSlide` | 13 | "It wasn't about the lemons" — typographic, quiet |

All 6 should follow v3.0's color palette and component conventions (use existing `colors`, `TIER_STYLES`, `renderShape`).

---

## STEP STRUCTURE QUICK TABLE

| # | ID | Section | Kind | Component | Key params |
|---|----|---------|------|-----------|------------|
| 1 | c0 | Hook | hook | HookSlide (NEW) | — |
| 2 | c1 | Cars | population | PopulationView (NEW) | tiers: [0,1,2,3] |
| 3 | c2 | Cars | listings | MarketplaceView (NEW) | — |
| 4 | c3 | Cars | standard | TokenGrid + LotCalc | symmetric, $11K |
| 5 | c4 | Cars | spin | SpinExperience (MOD) | $11K offer |
| 6 | c5 | Cars | lossViz | LossVisualization (MOD) | + bankruptcy |
| 7 | c6 | Cars | standard | TokenGrid + LotCalc | seller, [1,2,3], $11K |
| 8 | c7 | Cars | standard | TokenGrid + LotCalc | seller, [2,3], $11K |
| 9 | c8 | Cars | standard | TokenGrid + LotCalc | seller, [3], $5K, spiral |
| 10 | c9 | Cars | frozen | FrozenMarketView (NEW) | all tiers, only Lemon active |
| 11 | c10 | Concept | concept | ConceptCard (NEW) | — |
| 12 | c11 | Cars | fix | FixCard (MOD) | car fix |
| 13 | c12 | Pivot | abstraction | AbstractionSlide (NEW) | — |
| 14 | p0 | Phones | standard+fix | TokenGrid + LotCalc + FixCard | seller→fixed |
| 15 | i0 | Capital | standard+fix | TokenGrid + LotCalc + FixCard | seller→fixed |
| 16 | z0 | Pattern | cost | CostEscalation (MOD caption) | — |
| 17 | z1 | Pattern | capstone | CapstoneConnections (MOD copy) | — |

---

## LOCKED DECISIONS

- **17 steps total** (was 15). Pacing: ~42 sec/step within the ~12 min Akerlof segment. Tight but workable.
- **"Allocational efficiency" used explicitly** as a term — matches Seeds of Fortune academic register.
- **Carfax framing**: entrepreneurial opportunity, not just consumer fix. Include the line "Profit motive pointed at a real problem produces social good as a by-product. This is the good side of economics."
- **Step 13 phrasing**: "It wasn't about the lemons." (NOT "It wasn't about cars" — Rick's improvement; punctures 20 min of lemon-talk in one line)
- **Repair-cost framing** for car tiers: derive values, don't assert them
- **Symmetric ignorance baseline first**, then asymmetric reveal (was the inverse in v3.0)
- **All sellers ask $20K** in Step 3 — stylized teaching device, not realistic listing variation. The uniformity IS the lesson.
- **Bankruptcy callout in loss-viz** — keep it; powerful pedagogy on bounded downside
- **Compress phones to 1 step, capital to 1 step** — they're applications now, not narratives
- **Producer collaboration mode** stays — Rick sets vision, Claude builds and flags decisions

---

## OPEN QUESTIONS (None blocking — defaults stated)

1. **File management for v4.0**: build as new `akerlof-lemons-v4.html` first, validate, then rename to replace v3.0? Or rebuild in place with version-tag in the file? **Default: build as `akerlof-lemons-v4.html`, validate, then if Rick approves, rename to `akerlof-lemons.html` (keeping v3 in git history).**
2. **Step 13 visual**: pure typography or with a small symbolic graphic? **Default: pure typography — quietest possible. The line itself is the slide.**
3. **HookSlide visual**: include a stylized "rich uncle" element (top hat? envelope?) or stay neutral with just the dollar amount and car icon? **Default: neutral — the inheritance is in the narration, not the visual. Keeps the slide adult.**

---

## VERIFICATION CHECKLIST (before declaring v4.0 done)

- [ ] All 17 steps render and navigate
- [ ] SpinExperience offers $11K, tally labels updated to BARGAIN/OVERPAID
- [ ] Spin distribution looks roughly even across many runs
- [ ] LossVisualization shows affordability indicators + bankruptcy callout
- [ ] Cascade flows correctly: c6 (Mint walks) → c7 (Good walks, pool avg = $5K shown) → c8 (revise to $5K, Fair walks)
- [ ] FrozenMarketView shows clear contrast (1 trade vs. 3 stuck)
- [ ] ConceptCard introduces "allocational efficiency" cleanly
- [ ] AbstractionSlide loads with quiet, large typography
- [ ] Capstone wording uses Seeds of Fortune register (allocational, structured credit, financial inclusion)
- [ ] Color palette consistent with v3.0
- [ ] Zoom legibility check: project to a real screen
- [ ] Update this brief with session 4 ACTUAL build outcomes (vs. just plan)

---

## FILES IN WORKSPACE

| File | Status | Notes |
|------|--------|-------|
| `akerlof-lemons.html` | v3.0 — superseded but on disk | DO NOT MODIFY until v4.0 is validated |
| `akerlof-lemons-v4.html` | TO BUILD next session | The new 17-step version |
| `marketplace-deck-v2.html` | Archive | — |
| `loss-visualization.html` | Archive | — |
| `graphics-review.html` | Archive | — |
| `design-sketches-*.html` | Archive | — |
| `marketplace-deck.html` | Archive | — |
| `CONTINUATION-BRIEF.md` | This file | Canonical |
| `CONTINUATION_BRIEF.md` | Stale (older underscore version) | Can be deleted |

**Source for any history-section content (still TBD if used):** `/Users/ra1/Claude-Cowork-Projects/Accounting_Origins/`

**PowerPoint deck**: still not started. After v4.0 ships, the deck is the next priority.

---

## QUICK CONTEXT FOR NEXT SESSION

You're picking up after a planning conversation in which Rick redirected the structure of the interactive tool. **No code was written in session 4** — this brief IS the work product of that session. Read it, then read v3.0 (`akerlof-lemons.html`, ~1157 lines) to ground yourself in the existing component architecture. Then build `akerlof-lemons-v4.html` per the spec above. Don't relitigate the conceptual decisions — they're locked. Build first, flag if you hit something the brief didn't anticipate.

The 6 NEW components and the modifications to SpinExperience and LossVisualization are the bulk of the work. Everything else is wiring and copy.

---

## V4.1 REVISIONS — TO BE EXECUTED NEXT SESSION

Rick reviewed v4.0 in Session 6 (discussion only) and flagged 11 fixes. Decisions are locked. Apply these in place on `akerlof-lemons-v4.html`. **Net structural change:** step count drops from 17 → 16 because c6 and c7 collapse into one step (Mint AND Good walk together at $11K — they reason identically).

### The 11 fixes

**R1 — Step 3 (c2, MarketplaceView) insight: drop the "seller knows" attribution.**
Current: "Why is everyone asking the mint price? Because the seller knows what they have, and you don't."
Wrong: at this point the asymmetry hasn't been introduced yet. Every seller posts $20K because they're rational price-anchorers in a market where buyers can't tell quality from photos.
Fix: rewrite the insight to something like *"From the photos alone you can't tell which is which — and every seller is asking the most they could plausibly get. (Hold this thought — we'll come back to why the math here goes wrong.)"* Don't name the asymmetry yet.

**R2 — Step 5 (c4, Spin) — strip the entire top half.**
Current: SpinExperience top has a left "What each seller privately knows" flip-card panel and a right "Your 4 listings" panel. This is leftover from v3.0 where the spin demonstrated asymmetric information. In v4.0, the spin lives in the symmetric-ignorance world — neither side knows.
Fix: **delete the top two-column section entirely.** Go straight from the headline + narrative to the offer button + tally + result panel (the bottom half of SpinExperience as it stands). The interactive simulation IS the page.

**R3 — Compress old c6 + c7 into one step (call it c6) — Mint AND Good walk together.**
Current: c6 is "Mint walks" (activeTiers [1,2,3]); c7 is "Good walks, pool avg $5K" (activeTiers [2,3]).
Wrong: at $11K with sellers knowing, both Mint ($20K) and Good ($14K) refuse for the same reason — their cars are worth more than $11K. The cascade has them walking simultaneously, not sequentially.
Fix: collapse to one step. New c6:
- **Headline:** "Sellers wake up — you're left with the bottom half."
- **Narrative:** "Same setup. Same four cars. Same $11K offer. But now each seller knows what their car is worth. Mint's owner: 'Worth $20K — no thanks.' Good's owner: 'Worth $14K — no thanks.' Both walk. The only sellers who'd accept your $11K are Fair and Lemon. The pool you're now drawing from has an average value of $5K — you're paying $11K for it. Expected loss: $6K. Plus a 50% chance of the un-fixable Lemon."
- **Insight:** "Your offer didn't draw a random sample. It systematically attracted the worst. Economists call this **adverse selection**."
- **Order on page:** narrative first (setup), then visual showing the walk (TokenGrid with [2,3] active, Mint and Good faded), then insight. Don't show the post-state in the headline — let the experience precede the result.
- **Parameters:** activeTiers: [2,3], infoMode: 'seller', offer: 11000, showCalc: true.

After c6 (the merged step), the cascade continues with what was c8 (now c7) and c9 (now c8):

**R3a — Step 7 (was c8, now c7): "You revise to $5K. Fair walks."**
Unchanged content from v4.0 c8. Just renumbered.

**R3b — Step 8 (was c9, now c8): FrozenMarketView.**
Unchanged structure from v4.0 c9, BUT see R4 below.

(All step IDs after the merge: c0, c1, c2, c3, c4, c5, c6, c7, c8, c10, c11, c12, p0, i0, z0, z1 — 16 total. Note c9 is now skipped in the ID sequence so renumbering existing IDs isn't required; c10/c11/c12 keep their IDs to preserve git/disk continuity. **Or** renumber sequentially — choose whichever is cleaner. Recommend keeping existing IDs and just having a gap at c9 — saves churn in the App and step-dot rendering.)

**R4 — Step 10 (now step 8, c9): kill redundant text in FrozenMarketView.**
Three voices currently say the same thing: the visual carries it, the in-component footer ("1 trade happens. 3 don't…") repeats it, and then the narrative + insight repeat it again.
Fix:
- Remove the in-component yellow footer paragraph at the bottom of FrozenMarketView (the "1 trade happens. 3 don't…" panel).
- Keep the narrative box (it frames the moment).
- Shorten the insight to a single line, e.g. *"The market hasn't disappeared — the GOOD market has frozen. Invisible if you're not looking for it."*

**R5 — Step 11 (c10, ConceptCard): drop the premature "capital doesn't reach" line.**
Current narrative names capital markets before they've been introduced.
Fix: replace *"The good cars don't reach the buyers who want them. Capital doesn't reach the companies that would deploy it best. The economy is poorer..."* with something cars-only, e.g. *"The good cars don't reach the buyers who want them. The mint owner is stuck. A buyer who'd happily pay $20K for a verified mint car goes without. The economy is poorer not because the car doesn't exist, but because it can't find its way to the right hands."*

**R6 — Step 11 (c10, ConceptCard): foreground the symmetric-states-are-fine point. Add a third panel.**
Currently the card contrasts "with shared information ✓" vs "with asymmetric information ✕". The pedagogically correct framing is three states, not two:
- Shared full information ✓ — works
- Shared ignorance ✓ — also works (just trades happen at the average)
- Asymmetric information ✕ — breaks
Plus one extra line foregrounded in the narrative (per Rick's parenthetical, decision Q3): *"Even the suspicion that the other side knows more is enough to start the unraveling — buyers shade their offers down, sellers walk, and the spiral begins."*
Fix:
- Add a middle panel between the existing two: "✓ With shared ignorance — neither side knows; trades happen at the average." Visually parallel to the other two. Maybe two question-mark cars facing a buyer with an average-of-pool arrow.
- Add the suspicion line to the body narrative as a foregrounded sentence (not parenthetical).

**R7 — Step 12 (c11, Carfax): kill duplication between FixCard and narrative.**
The FixCard body and the narrative box both retell the 1984/$40/database story.
Fix: shrink the narrative to one line of setup — *"In 1984, someone saw a business in this gap."* Let the FixCard expand it. Insight box keeps the "good side of economics / capstone hook" framing.

**R8 — Step 13 (c12, AbstractionSlide): reasoning before conclusion.**
Currently the giant serif "It wasn't about the lemons." lands first, then the narrative below explains why.
Fix: restructure the AbstractionSlide so the reasoning leads visually and the punchline lands at the bottom. Internal layout (top to bottom):
- Small lead-in: *"For the last 20 minutes: lemons. Cars. $20K. Carfax. Mint condition."*
- Mid-size beat: *"The actual problem: one side knew, the other didn't."*
- Mid-size beat: *"The actual fix: making the knowledge shared."*
- A breath of whitespace.
- Climactic large serif at bottom: *"It wasn't about the lemons."*
Also: cut the narrative box on this step entirely. The slide IS the slide. (Keep the standard step header / nav bar; just suppress the italic narrative panel on this one step.)

**R9 — Step 14 (p0, iPhones): kill redundancies between insight and FixCard.**
Insight and FixCard both restate the Apple aligned-incentives story.
Fix:
- Shorten the narrative: *"Used iPhones on Marketplace. Battery health is the hidden quality. Sellers know; buyers can't see it. Same structure as cars."*
- Let FixCard carry the Apple-incentives detail (no change to FixCard text).
- Either cut the insight box, or replace with a one-liner: *"Same logic as Carfax — at a different price tag."*

**R10 — Step 15 (i0, Capital): rewrite the setup using Rick's framing.**
Current opening parachutes the student into "Four companies seeking investment capital."
Fix: replace narrative with (Rick's wording, lightly edited):
*"You've seen it in cars and phones. Now to somewhere less familiar. Imagine you run a company. You've spotted a profit opportunity, but to take advantage of it, you need cash. The stronger the opportunity, the more you'd want to put behind it. How do you get the cash? Two ways: borrow it, or take on a partner. Economists call the second one **raising capital**."*
- The transition cue *"Now to somewhere less familiar"* replaces "Now for something more abstract" (Rick's call: don't like "more abstract"; this is the chosen replacement, decision Q4). Two backups if Rick wants to swap during execution: *"Now to where the stakes get bigger"* or *"Same lens, less concrete ground."* I'd commit to the first unless Rick redirects.

**R11 — Step 15 (i0, Capital): redesign as one company / four possible opportunities + over-raise wrinkle (light touch).**
Current step has 4 buildings (companies) paralleling the 4 cars. Rick wants ONE company that has one of four possible investment opportunities. Investors can't see which opportunity is real; that's the asymmetry. Plus a one-line moral-hazard note that companies have an incentive to over-raise because existing equity pockets the surplus.
Fix:
- Update INV_TIERS from companies to opportunities. Tier labels become opportunity quality, not company quality. Suggested:
  - Strong opportunity ($20M needed, $20M return)
  - Solid opportunity ($14M needed, $14M return)
  - Weak opportunity ($8M needed, $8M return)
  - Speculative ($2M needed, $2M return)
- Visual: keep BuildingSVG (one building → one company), but change the four positions to show the four *possible opportunity profiles* the company might be raising for. Could be a single stylized building at the top with four "opportunity cards" below it (paralleling four car tiers). Or keep the existing four-position layout but with the headline reframed: "Same company, four possible profiles — investors can't tell which is real."
- Add a single line in the narrative or insight (light touch per decision Q5): *"And there's a wrinkle: if the company asks for more cash than the opportunity actually needs, existing owners pocket the surplus. So even weak-opportunity companies have a reason to ask big."*

### What stays the same

Everything else in v4.0 is locked. Specifically: HookSlide, PopulationView, MarketplaceView, the symmetric-ignorance c3, LossVisualization (with bankruptcy callout), CostEscalation, CapstoneConnections (already correct icons + copy), the App shell, color palette, sound utilities, navigation. Don't touch what isn't on the R1–R11 list.

### Verification checklist for v4.1

- [x] 16 steps total (c6+c7 merged)
- [x] No "seller knows" attribution before c6 (the merged "sellers wake up" step)
- [x] SpinExperience top half removed; goes straight to offer button
- [x] c6 headline does not pre-spoil; reasoning precedes result on page (`narrativeFirst: true` in the step config; App renders narrative before TokenGrid)
- [x] FrozenMarketView in-component footer removed
- [x] ConceptCard has three states (full info, ignorance, asymmetric) + suspicion line
- [x] No "capital" mention before step 15 (verified: c10 narrative now cars-only)
- [x] Carfax FixCard / narrative no longer duplicate (narrative shrunk to one line)
- [x] AbstractionSlide reads bottom-up (lead-in → reasoning → punchline; narrative box suppressed for this step)
- [x] iPhones step has no insight/FixCard duplication
- [x] Capital step uses one-company-four-opportunities frame + over-raise one-liner
- [ ] Click-through in real browser (Chrome MCP **NOT REACHABLE** in session 7 — needs manual pass before Mon May 4)
- [x] Update SESSION LOG with v4.1 actuals + any deviations

---

## V4.2 REVISIONS — TO BE EXECUTED NEXT SESSION

Rick reviewed v4.1 (Session 8, 2026-05-03) and flagged six revisions. Decisions locked. Apply in place on `akerlof-lemons-v4.html`. **Net structural changes:** step count drops from 16 → 15 because z0 (cost-escalation slide) is deleted (R16); slide ORDER changes because the abstraction (c12) moves before Carfax (c11) (R12).

### The six fixes

**R12 — Reorder: abstraction before Carfax.**
Current order: c10 (concept) → c11 (Carfax fix) → c12 (abstraction "It wasn't about the lemons"). Wrong: the abstraction is essentially a clean re-statement of the problem and the fix, and it currently lands AFTER Carfax has already shown a concrete instance of the fix. Pedagogically the abstraction should bridge from "cars-as-stand-in" to "the pattern generalizes," not summarize what we just walked through.
Fix: swap the two slides. New order: c10 → c12 (abstraction) → c11 (Carfax) → p0 → i0 → z1. Carfax becomes the first APPLICATION of the just-named principle (alongside iPhones and capital). Recommend keeping the existing IDs in their new positions (c12 still IDs as 'c12', c11 still IDs as 'c11') and just reordering the entries in the STEPS array — saves churn in everything that references IDs. The id-string now reading non-sequentially is fine; that's already the convention post-v4.1.

**R13 — Slide-by-slide narrative+insight redundancy audit, c10 to z1.**
Rick: "There are redundancies. I don't know why we have the text after the brown" — the brown narrative box and the yellow insight box often paraphrase each other. The fix is to walk every slide from c10 onward and decide which text block carries the load, then delete the other. Default rule: narrative box for setup ("here's what's in front of you"); insight box for the takeaway / lesson. If the FixCard or the visual already carries the takeaway, both text blocks may be unnecessary — collapse to just one or even zero. Specific candidates the auditor should check (non-exhaustive):
- **c10 (ConceptCard):** the ConceptCard component already carries the definition + three-state diagram. The narrative box and the insight box may both be cuttable to a single short line.
- **c11 (Carfax):** narrative is already one line ("In 1984, someone saw a business in this gap.") — keep. The insight (capstone hook) is doing real work — keep. Likely fine.
- **p0 (iPhones):** narrative + insight + FixCard all reference the same Apple/aligned-incentives idea. With R14 expanding the upstream-pricing point, decide which slot owns that detail.
- **i0 (Capital):** narrative is long, insight is dense, FixCard is dense. With R15 reframing toward trust+institutions, reset all three.
- **z1 (Capstone):** narrative is short ("Each topic is an information problem…"); CapstoneConnections does the work. Probably fine. Don't over-trim.

**R14 — iPhones (p0): expand the upstream pricing-power point.**
Currently the FixCard for phones briefly mentions "better resale value of old iPhones protects pricing power for new iPhones." Rick wants this expanded into a real beat because it's the cleanest illustration of aligned incentives in the talk. The mechanism, in plain language: thin resale market for used iPhones (caused by asymmetric info → adverse selection) means buyers of NEW iPhones can't recover much on resale, so their willingness to pay for new is anchored down. Apple solving the asymmetry (Battery Health) thickens the resale market, lifts used-iPhone prices, and so lifts new-iPhone willingness-to-pay. Apple isn't being charitable — it's protecting upstream pricing power. This is "profit motive pointed at a real problem produces social good as a by-product" with the upstream mechanism made unambiguous.
Fix: add the upstream-pricing-power point as a foregrounded sentence in either the FixCard outcome text or as a callout on the slide. Don't make it a wall of text — one or two sentences max. Suggested phrasing: "If used iPhones can't sell at fair prices, new iPhones become a worse deal — buyers price in a thin resale market. Apple fixing the asymmetry protects what people will pay for new ones. Self-interest, not generosity."

**R15 — Capital (i0): reframe from cost-of-fix to trust + institutions.**
The current i0 step leads with "the cost of the fix scales with the stakes." Rick wants this re-pivoted. The deeper point isn't that the fix is expensive — it's that the fix is HARD because it requires producing information people TRUST. Just generating disclosures isn't enough; they have to be credible. That credibility is constructed through stacked institutional mechanisms: regulations (SEC mandates), legal liability (officers, directors, auditors personally on the hook for false statements), independent auditing (CPAs verify the books, with their own liability and reputation at stake), accounting standards (GAAP makes disclosures comparable), and enforcement (SEC penalties, shareholder suits). Critical caveat Rick wants foregrounded: **"SEC disclosures, auditors, etc. don't fix the problem completely, but they do help ease it."** This is honest — regulation reduces the asymmetry, it doesn't eliminate it.
Fix:
- Drop the "$100K to $10M+ per year" framing as the headline lesson. Cost can stay in the FixCard as a parenthetical fact, not the main message.
- New core question for the slide: "How do you arrange for trustworthy information?"
- New core answer: **institutions** — regulations, liability, auditing, standards, enforcement — stacked on top of each other.
- Update FIX_DATA.investment to list these mechanisms cleanly. Either as a stack/list inside the FixCard or as a small "trust stack" diagram.
- Foreground "doesn't fully fix it; it eases it." This is also the bridge to R17 (when the stack fails or is bypassed, allocational efficiency collapses).

**R16 — Delete z0 (cost-escalation slide).**
Rick: "I don't really know why slide 15 is there." Slide 15 in v4.1 is z0 — the CostEscalation panel ($40 / Free / $100K-$10M+ on a log scale). With i0 reframed away from cost (per R15), this slide loses its anchor and becomes a detour right before the closing.
Fix: remove the z0 entry from the STEPS array. The CostEscalation component itself can stay in the codebase (commented or just unused) — easy to reinstate if Rick changes his mind. New step count: 15. New tail of the deck: ... p0 → i0 → z1.

**R17 — Add a "crises = information problems" beat between i0 and z1.**
Rick wants a line that says: when markets break — Great Depression, 2008 financial crisis — an information problem is suspect #1. This connects the Akerlof framework directly to the historical episodes the Seeds of Fortune students will encounter in their capstones, and it's the natural runway into z1's per-topic capstone connections.
Fix: add as either (a) a callout / insight block at the bottom of i0 (Capital) — the lightest touch, and honest because the SEC stack came from the Great Depression's information failures, or (b) a tiny new step between i0 and z1, kept very short — basically a typographic slide. Suggested phrasing: "When markets break — the Great Depression, 2008 — look for the information problem first. In 2008 it was MBS ratings: AAA-rated tranches that weren't AAA. The institutional stack was bypassed or compromised. The asymmetry came back. Allocational efficiency collapsed." Default: option (a) — append to i0 — to keep step count at 15. If Rick wants it as its own slide, it becomes a new step (16 again, but now with the abstraction-before-Carfax order from R12 and z0 removed per R16).

### What stays the same

Everything else in v4.1 is locked. Specifically: HookSlide, PopulationView, MarketplaceView, c3 symmetric ignorance, c4 spin (post-R2), c5 LossVisualization, c6 merged-cascade with `narrativeFirst`, c7 Fair-walks, c8 FrozenMarketView, c10 ConceptCard with three states, the App shell, color palette, sound utilities, navigation, CapstoneConnections topics+icons. Don't touch what isn't on the R12–R17 list.

### Verification checklist for v4.2

- [x] 15 steps total (z0 deleted; abstraction moved before Carfax; R17 attached as a callout on i0, not a separate step)
- [x] STEPS order: c0, c1, c2, c3, c4, c5, c6, c7, c8, c10, c12, c11, p0, i0, z1 (verified by render-dispatch simulation)
- [x] No narrative+insight content duplication on c10 → z1 after audit (c10 insight dropped; i0 narrative + insight + FixCard reset around the trust-stack frame; c11/p0/z1 already audited in v4.1; c12 narrative still suppressed by `kind === 'abstraction'`)
- [x] iPhones step has the upstream-pricing-power point foregrounded (FIX_DATA.phone.outcome rewritten — "If used iPhones can't sell at fair prices, new iPhones become a worse deal…")
- [x] Capital step's lead is "How do you arrange for trustworthy information?" (i0.headline updated)
- [x] Capital FixCard lists institutions (Regulations, Legal liability, Independent auditing, Accounting standards, Enforcement — five-layer numbered stack in FIX_DATA.investment.body)
- [x] Capital step states explicitly "don't fix the asymmetry. They *ease* it." (in i0.insight; "ease it" also echoed in FIX_DATA.investment.outcome)
- [x] Crises = information problems beat is present (new CrisisCallout component, rendered below i0's FixCard via `crisesBeat: true`; mentions Great Depression, 2008, MBS ratings, and the historical loop that the SEC stack itself was built in response to the Depression's information failures)
- [x] CostEscalation no longer rendered (z0 dropped from STEPS; CostEscalation component preserved in code per spec)
- [x] Click-through in real browser — **DONE in session 9.** Chrome MCP came online late in the session after Rick installed/connected the extension and ran a local Python HTTP server on port 8000. All 15 steps verified visually with screenshots and DOM reads: (a) c10 → c12 → c11 reads cleanly (concept → pivot → first application); (b) c12 renders bottom-up with the big serif punchline at the bottom (step 11 of 15); (c) i0 FixCard shows the five-layer numbered institutional stack with CrisisCallout sitting directly below it (step 14 of 15); (d) p0 FixCard outcome reads as the upstream-pricing-power story (step 13 of 15); (e) CostEscalation doesn't appear anywhere; (f) step dots show 15. **Bug caught and fixed during click-through:** v4.2 strings used `*emphasis*` and `**bold**` markdown syntax in narrative/insight/FixCard.body slots, but those slots interpolated raw strings — so asterisks rendered literally instead of as italic/bold. Fixed by adding a small `formatEmphasis` helper (~12 lines) that converts `*x*` → `<em>x</em>` and `**x**` → `<strong>x</strong>`, applied at the three render slots. Re-verified post-fix: 0 literal asterisks remaining, 3 `<em>` (trust/believed/ease) and the new `<strong>` (institutions) rendering on i0; "wedge" + "suspicion" rendering on c10.
- [x] Update SESSION LOG with v4.2 actuals + any deviations

---

## SESSION LOG

- **Session 1**: Designed 3-section arc, settled on heterogeneous tier model, escalating-cost-of-fix thread.
- **Session 2 (2026-05-02 morning)**: Built `akerlof-lemons.html` v2.0 (14 steps, 10-car model). Did graphics review. Built standalone `marketplace-deck-v2.html` and `loss-visualization.html` for c0 redesign.
- **Session 3 (2026-05-02 afternoon)**: Integration. Rebuilt cascade in 4-car terms. Folded spin + loss-viz into main tool. Applied all flagged graphics fixes. → v3.0 (15 steps).
- **Session 4 (2026-05-02 evening)**: PLANNING ONLY — no code. Rick re-architected the talk around problem-first opening (rich uncle inheritance), repair-cost tier framing, symmetric-then-asymmetric flow, allocational efficiency as named concept, Carfax as entrepreneurship, and "It wasn't about the lemons" pedagogical pivot. Result: this brief, which specs out v4.0 (17 steps). Saved 6 thoughts to Open Brain capturing the conceptual decisions.
- **Session 5 (2026-05-02 late evening)**: EXECUTED brief. Built `akerlof-lemons-v4.html` (1,637 lines). All 17 steps wired with 8 distinct render kinds (hook, population, listings, spin, lossViz, frozen, concept, abstraction; standard for c3/c6/c7/c8/c11/p0/i0; closing for z0/z1). Built all 6 new components (HookSlide, PopulationView, MarketplaceView, FrozenMarketView, ConceptCard, AbstractionSlide), modified SpinExperience ($11K offer, BARGAIN/OVERPAID labels, repair-affordability line on result), modified LossVisualization (single value bar per outcome, affordability indicators per row, bankruptcy callout), updated FIX_DATA copy for Carfax/Battery Health/SEC with entrepreneurship+aligned-incentives framing, updated CostEscalation caption to "The fix scales with the stakes," reconciled CapstoneConnections to 🏛 🏢 📲 🏠 with Step 17 wording. Added `concept` and `pivot` as new section keys with their own badge colors (royal purple for concept, amber for pivot). Loaded Lora serif via Google Fonts for ConceptCard heading and AbstractionSlide typography. JSX validated by compiling through @babel/preset-react locally — clean compile, no syntax errors. **Browser click-through deferred:** the Claude-in-Chrome MCP wasn't reachable in this session, so interactive verification (spin distribution, navigation, hover states, repair-affordability arithmetic) needs a manual pass before the talk. **Deviations from spec:** (a) Steps 14 (p0) and 15 (i0) use `infoMode: 'fixed'` rather than transitioning seller→fixed mid-step, since the static TokenGrid can't animate the toggle and the FixCard already carries the resolution narrative. (b) The summary panel in the modified LossVisualization replaces the single "expected loss" stat with a "2 in 4 can't afford repairs" stat to foreground the bounded-downside lesson over the textbook EV calc. (c) `c11` (Carfax) is rendered as a standard-kind step (TokenGrid with `infoMode: 'fixed'` + FixCard) rather than getting a bespoke kind, since the existing visual structure carries the framing once the FixCard copy is updated. v3.0 (`akerlof-lemons.html`) preserved on disk as fallback per brief.
- **Session 6 (next)**: Click through `akerlof-lemons-v4.html` in a real browser. Verify spin distribution looks even across many runs, that the cascade reads cleanly across c6→c7→c8→c9, and that ConceptCard + AbstractionSlide land at projection size. If everything works, decide whether to rename v4 → `akerlof-lemons.html` (per brief Open Question #1). Then start the PowerPoint deck.
- **Session 7 (2026-05-02 night)**: EXECUTED v4.1 revisions in place on `akerlof-lemons-v4.html`. All 11 fixes (R1–R11) applied per spec. **Net structural change:** STEPS array now has 16 entries (down from 17); the merged c6 absorbs old c6+c7. ID sequence: c0, c1, c2, c3, c4, c5, c6 (merged), c7 (was c8 — Fair walks), c8 (was c9 — FrozenMarketView), [gap at c9], c10, c11, c12, p0, i0, z0, z1 — matches the spec's listing exactly. **Component changes:** SpinExperience top half (flip-card panel + listings panel) deleted; dead state (`sellerIdx`, `flipping`, `flipSeller`) cleaned up. ConceptCard rebuilt as three panels (full info / shared ignorance / asymmetric) with new question-mark-buyer middle panel; definition copy is now cars-only. AbstractionSlide rebuilt bottom-up: small lead-in → two mid-size reasoning beats → whitespace breath → climactic large serif punchline at bottom; min-height bumped to 380px to give the layered structure room. FrozenMarketView yellow footer removed. **App rendering changes:** added `narrativeFirst` flag support (renders narrative before the visual cascade for c6); added `step.kind === 'abstraction'` suppression for the narrative box (c12). **Copy changes:** c2 insight (R1), c8 insight (R4), c10 narrative (R5+R6 suspicion line), c11 narrative shrunk to "In 1984, someone saw a business in this gap." (R7), p0 narrative + insight trimmed (R9), i0 headline + narrative + insight rewritten (R10+R11), INV_TIERS labels reframed Strong/Solid/Weak/Speculative (R11). Version bumped to 4.1; description block in the file's header comment now lists the 11 fixes for traceability. **Verification:** JSX compiles cleanly through `@babel/preset-react` (no syntax errors). Static string-match verification confirms all 11 revisions are present and the obsolete strings are gone. STEPS array length and ID sequence match spec. **Deviations from R-spec:**
  1. The R-list called for "two question-mark cars facing a buyer with an average-of-pool arrow" in the new ConceptCard middle panel; I rendered it instead as ONE question-mark car ↔ ONE question-mark buyer with a $11K bidirectional arrow. The pedagogical intent (both sides ignorant, trade still happens at the average) is preserved; the single-car-single-buyer composition is visually parallel to the other two panels (which also show one car ↔ one buyer), so all three states read symmetrically. Easy to swap to two cars if Rick prefers — the panel is locally contained.
  2. The i0 insight was lightly trimmed beyond the explicit R10/R11 wording — old phrasing "Carfax was $40. Why so much more?" was replaced with a tighter sentence about the SEC fix scaling with stakes. The over-raise wrinkle went into the narrative (per spec's "single line in the narrative or insight"). Slight residual redundancy remains between the i0 insight and the SEC FixCard outcome text; flagging in case Rick wants this trimmed before the talk (parallel to R7 for Carfax and R9 for iPhones).
  3. Step c12 still has `narrative` text in the data structure even though the App now suppresses the narrative box for `kind === 'abstraction'`. Left in place as documentation/reference; it doesn't render.
  4. **Browser click-through deferred AGAIN.** Chrome MCP returned an empty browser list across 7+ retry attempts (`list_connected_browsers` → `[]`, `tabs_context_mcp` → "extension not connected"). The extension may not be installed/signed in on Rick's Chrome at the moment. JSX-compile + static string verification stood in for browser verification. **Real-browser pass remains a TODO before the talk Mon May 4.** Easiest path: open `akerlof-lemons-v4.html` directly in Chrome (no server needed — it's a self-contained file), step through all 16 steps, and verify (a) spin runs and shows BARGAIN/OVERPAID labels, (b) c6 renders narrative-first with TokenGrid showing Mint/Good faded, (c) FrozenMarketView no longer has the yellow "1 trade happens" footer, (d) ConceptCard shows three panels stacked vertically, (e) AbstractionSlide reads top-to-bottom: small lead-in → two beats → big "It wasn't about the lemons." at the bottom.

- **Session 8 (2026-05-03 — discussion only)**: Rick reviewed v4.1 and flagged six v4.2 revisions (R12–R17). No code; this brief's V4.2 REVISIONS section is the work product of that session. Decisions locked.
- **Session 9 (2026-05-03)**: EXECUTED v4.2 revisions in place on `akerlof-lemons-v4.html`. All six fixes (R12–R17) applied per spec. **Net structural change:** STEPS array now has 15 entries (down from 16); z0 (cost-escalation slide) removed per R16; abstraction c12 moved before Carfax c11 per R12. Final ID order: c0 → c1 → c2 → c3 → c4 → c5 → c6 → c7 → c8 → c10 → c12 → c11 → p0 → i0 → z1. **Component changes:** new `CrisisCallout` component added (renders below i0's FixCard via `crisesBeat: true` flag); `CostEscalation` retained in code but no longer dispatched; closing-section dispatcher trimmed to z1 only. **Copy changes:** c10 narrative shortened to one paragraph (the ConceptCard now carries the definition + three-state diagram alone; insight dropped) per R13; c11 sectionLabel updated to "🌱 Application: Carfax" to match the new application framing; p0 sectionLabel updated to "📱 Application: iPhones" with insight rewritten to point at the upstream-capture mechanism rather than restating the price-tag comparison; i0 fully reset — headline now "How do you arrange for trustworthy information?", narrative recasts the company-needs-cash setup as a lead-in to institutions-as-fix, insight foregrounds "don't fix the asymmetry. They *ease* it." **FIX_DATA changes:** `FIX_DATA.phone.body` shortened to one line (Apple built the fix in, un-fakeable), `FIX_DATA.phone.outcome` rewritten as the full upstream-pricing-power mechanism (R14); `FIX_DATA.investment` rewritten as the five-layer trust stack with explicit numbered enumeration in `body` and "they ease it. That's as good as it gets." in `outcome` (R15). Version bumped to 4.2; header description block now lists the six fixes for traceability. **Verification:** JSX compiles cleanly through `@babel/preset-react` (no syntax errors); a render-dispatch simulator (parses the STEPS block with proper string-aware bracket counting and replays the App's per-step kind switch) confirms all 15 steps render the expected components — full dispatch table run with 15 / 15 asserts passing (c12 before c11; z0 absent; c10 has no insight; c12 suppresses narrative; i0 has FixCard + CrisisCallout + insight; SpiralBadge only on c7; no step renders CostEscalation; c6 narrative renders narrativeFirst). **Deviations from R-spec:**
  1. R17 placement: spec offered (a) callout on i0 or (b) tiny new step. I picked (a) — callout — to keep step count at 15 per the brief's preferred default. The CrisisCallout is implemented as its own React component (not just an extra block of insight text) so it renders with a distinct red-bordered "When the stack is bypassed" badge, visually separating it from the trust-stack message above it. The component includes a third sentence beyond the spec's suggested phrasing — that the SEC stack itself was built from the Depression's information failures — to close the historical loop and bridge into z1. Easy to trim if Rick wants it shorter.
  2. R13 audit on p0 and z1: I left both effectively as v4.1 trimmed them. p0 still has narrative (1 sentence), insight (1 sentence revised to point at upstream capture), and FixCard (now expanded with the R14 mechanism). z1 still has narrative + CapstoneConnections, no insight. In both cases the three blocks are short enough and pointing at different things that consolidating further felt like over-trimming. Flagging in case Rick wants either trimmed harder.
  3. **Browser click-through INITIALLY deferred, then RECOVERED later in the session.** Chrome MCP returned `[]` from `list_connected_browsers` and "extension not connected" across 8+ retries early in the session — same failure mode as session 7. After the SESSION LOG was updated with that as a deferred item, Rick installed/signed-in the Chrome extension and `list_connected_browsers` came back with "Mac mini Chrome." File:// URLs are blocked by the MCP, so Rick spun up `python3 -m http.server 8000` from the talk folder; I navigated the MCP-controlled tab to `http://localhost:8000/akerlof-lemons-v4.html?v=2` and stepped through every slide using the dev-mode jump buttons (triple-click the header to enable). All R12–R17 outcomes verified visually + via DOM reads.
  4. **Markdown emphasis bug caught and fixed during click-through.** I had introduced `*emphasis*` / `**bold**` markdown into v4.2 narrative/insight/FixCard.body strings (c10 narrative, i0 narrative, i0 insight, FIX_DATA.investment.body), but the rendering slots interpolated raw strings, so asterisks rendered literally on the page. Fix: added a small `formatEmphasis` helper just before `SpiralBadge` (~12 lines) that runs a `\*\*x\*\*|\*x\*` regex and emits `<strong>` / `<em>` JSX, then applied it at the three render slots in TutorialApp (narrativeFirst position, default narrative position, insight box) and at FixCard (body + outcome). Re-verified: 0 literal asterisks on i0 or c10 post-fix; all the intended emphasis renders as italic/bold. The helper handles strings without asterisks as a no-op so it's safe to call universally.
