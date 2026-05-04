# Session 11 Brief — Seeds of Fortune Talk

**Talk:** Mon May 4, 2026 · 6 PM Zoom · ~40 HS juniors · Yale Women in Economics / Seeds of Fortune
**Status as of end of Session 10 (May 3, 2026 late evening):** `akerlof-lemons-v4.html` is at **v4.4.0** — the major Session-10 restructure shipped (all problems first → synthesis → diagnosis → pivot → fixes → capstone). Speaker notes synced. JSX compiles cleanly. The interactive is rough-in done; this session is about everything that wraps around it.
**Producer mode applies:** Rick sets vision, Claude builds, Claude flags. Don't co-write — draft and react.

---

## ⛳ FIRST READS (in this order, don't skip)

1. **This brief** (top to bottom).
2. **Global skills directive** at `/Users/ra1/YALEiE-Local/accounting-pedagogy-skills/CLAUDE.md` (or wherever the global hostloop CLAUDE.md is mounted in this session). The relevant skill for this session is **`interactive-tutorial-builder`** — load it via `Skill: anthropic-skills:interactive-tutorial-builder` before touching any code in `akerlof-lemons-v4.html`.
3. **Open Brain** — Rick's external thought system. Before starting work, run targeted searches via `mcp__2467bd2c-d90f-4be4-86fe-21c8e894be8f__search_thoughts`. Suggested first queries:
   - `"Rick Antle bio Yale teaching philosophy"` — for the Going-In intro material.
   - `"Madoff feeder fund 217 Canner Associates"` — Rick's direct personal credential on information failure (he was sole-member trustee for two Madoff feeder fund liquidating trusts). This is the single strongest credibility hook for this audience.
   - `"Diamond Dybvig bank runs Yale Nobel colleagues"` — Diamond and Dybvig shared the 2022 Nobel for the canonical model of bank runs; their work is directly the mechanism behind the Great Depression card in the invFix slide. Highest-leverage Nobel-colleague citation for this talk.
   - `"Robert Wilson Stanford Joel Demski Antle pedigree"` — Rick's PhD pedigree (taught by Wilson, the "big influence" — 2020 Nobelist; advised by Demski). Use for Going-In if Rick wants to lead with academic lineage.
   - `"Seeds of Fortune talk allocational efficiency growth"` — to find the Session-10 thought capturing Rick's "more than allocational efficiency" wedge.
   - `"Wilton Anderson Oklahoma State $400 accounting"` — Rick's origin story (father was a steelworker, originally wanted to be a lawyer, got "bought" into accounting for $400 by Prof. Anderson). Useful for warming the audience.
   - `"information asymmetry pedagogy three states"` — for connecting back to the c10 / synthesis content if the wedge needs a new beat there.
4. **Auto-memory `MEMORY.md`** index — for the Producer-role expectation, reveal-pattern conventions, and anything else that has accumulated.
5. **`akerlof-lemons-v4.html`** v4.4.0 — at minimum scan the @changelog block for v4.4.0 (Pass A/B/C entries) and the STEPS array (now 18 entries: c0..c8, p0, i0, synth, c10, c12, combFix, invFix, z1).
6. **`speaker-notes.html`** v4.4.0 — 18 steps in 8 acts, in sync with the deck. Note the placeholder blocks at the top (`Going In`) and bottom (`Coming Out`) — those are this session's deliverables.

---

## 🚦 SHIPPING STATE

- File: `akerlof-lemons-v4.html` v4.4.0 — JSX compiles cleanly. Click-through across the new structure verified by Rick at end of Session 10.
- 18 steps total, in this order: **c0, c1, c2, c3, c4, c5, c5b, c6, c7, c8, p0, i0, synth, c10, c12, combFix, invFix, z1**.
- v3.0 (`akerlof-lemons.html`) remains the disk fallback — DO NOT TOUCH.
- v4.0–v4.3.x history is in the `@changelog` block at the top of `akerlof-lemons-v4.html`. Read it once if you want the full prior context; otherwise the most recent entries (Pass A/B/C of Session 10) are the load-bearing ones.
- `speaker-notes.html` is in sync as of v4.4.0. Mirror any deck change there.
- The PowerPoint deck wrapper: still not started. Out of scope unless Rick promotes it.

---

## 📐 ESTABLISHED PATTERNS (use these — don't reinvent)

### Click-to-advance reveals
The dominant pattern. Per-beat reveals so Rick can pace each idea live. Standard scaffolding:

```jsx
const TOTAL_BEATS = N;
const [beat, setBeat] = useState(1);
const advance = () => setBeat(b => Math.min(b + 1, TOTAL_BEATS));
const reveal = (visible) => ({
  opacity: visible ? 1 : 0,
  transform: visible ? 'translateY(0)' : 'translateY(8px)',
  transition: 'opacity 0.4s ease, transform 0.4s ease',
});
```

Outer div: `onClick={advance}`, `cursor: beat < TOTAL_BEATS ? 'pointer' : 'default'`, `userSelect: 'none'`. Bottom: dot indicator (one per beat) + "click to continue ▸" hint that hides at final beat.

Reference components: HookSlide, PopulationView, MarketplaceView, LossVisualization, RuleChangeSlide, CascadeSlide, CascadeRevisionSlide, AbstractionSlide (v4.4.0 rebuild), SynthesisSlide, CombinedFixesSlide, InvestmentFixesSlide.

### Speaker notes vs. on-screen content
- **Narrative** (in STEPS) = SPEAKER SCRIPT, hidden by default. Visible only when 📝 toggled in header (or `?notes=1`). Rendered with a "📝 SCRIPT" label.
- **Insight** (in STEPS) = on-screen lightbulb at App level — UNLESS timed to a specific beat, in which case set `step.insight = null` and render the lightbulb inline in the component.

### Tier color palette (don't override)
Mint = gold `#c9a227` · Good = green `#22c55e` · Fair = orange `#f97316` · Lemon = red `#dc2626`. Bar/icon colors track TIER. Don't paint Mint green just because it's a "positive outcome."

### Headline / narrative suppression
Typographic slides where the slide IS the slide (`abstraction`, `ruleChange`, `synthesis`) suppress both the App-level headline (`display: 'none'`) and the App-level narrative box. Add new kinds to those checks if you build more typographic slides.

### Section + section-color
Sections used: `car`, `phone`, `investment`, `concept`, `pivot`, `closing`. SECTION_COLORS in App resolves the badge color. If you add new sections, register them there.

---

## 🛠️ WORKING ENVIRONMENT

- **Local server:** Rick runs `python3 -m http.server 8000` from the talk folder. File:// is blocked by Chrome MCP — always use `http://localhost:8000/akerlof-lemons-v4.html?v=N`. Bump `N` after each edit to bust cache.
- **Chrome MCP:** Online ("Mac mini Chrome" — `list_connected_browsers` returns it). The actual outer click handler can be flaky to drive programmatically; trust the JSX compile + the proven reveal pattern, let Rick click through and report.
- **JSX-compile check after every edit (run from the bash tool):**
  ```
  cd "/sessions/.../Seeds of Fortune Talk" && node -e "const fs=require('fs'),babel=require('/tmp/node_modules/@babel/core');const html=fs.readFileSync('akerlof-lemons-v4.html','utf8');const m=html.match(/<script type=\"text\/babel\">([\s\S]*?)<\/script>/);try{babel.transformSync(m[1],{presets:['/tmp/node_modules/@babel/preset-react']});console.log('OK');}catch(e){console.error('FAIL:',e.message);}"
  ```
- **Dev mode jump buttons:** triple-click the header to enable.
- **Open Brain:** captures by `mcp__...__capture_thought`, retrieved by `search_thoughts`. Capture session-end observations there so future sessions inherit context. Open Brain holds Rick's thoughts on pedagogy, real-world examples (Madoff, Nathan's Famous, Apple, etc.), bio material, and prior session decisions.

---

## 🎯 SESSION 11 — THE THREE PIECES OF WORK

These three pieces wrap around the interactive, not inside it. The deck itself is rough-in done; what's missing is the live performance frame.

### Piece 1 — "Going In": Rick introduces himself and hands the audience into the interactive

Audience: ~40 high school juniors at Yale, majority women, headed toward econ/finance via Yale Women in Economics. They've never met Rick. They probably don't know what an accounting professor does. They need to walk away from the first 60 seconds thinking "this guy is the right person to be telling me this."

The strongest credibility hook (verified via Open Brain on `217 Canner Associates`):
> Rick is the **sole member of 217 Canner Associates LLC**, which served as trustee for the liquidating trusts of two Madoff feeder funds (Greenwich Sentry Fund and Greenwich Sentry Partners Fund).

That's a direct, personal, *teach-from-experience* connection to the largest information-asymmetry-driven fraud in modern history. He doesn't just teach this stuff; he was the guy whose job it was to clean up after one of the most notorious information asymmetries of our lifetime.

Other Going-In ingredients to consider (all sourced from Open Brain — search those queries first):
- William S. Beinecke Professor of Accounting at Yale SOM; adjunct at Yale Law.
- PhD Stanford 1981. Co-author of *Financial Accounting* textbook.
- Origin: father was an **ironworker** (not a steelworker — important detail; an ironworker erects structural steel on construction sites); second in family to attend college; originally wanted to be a lawyer; got "bought" into accounting for $400 by Prof. Wilton Anderson at Oklahoma State.
- **Stanford pedigree (the deepest, cleanest hook for *this* audience):** Rick was taught at Stanford by **Robert Wilson** — the "big influence" of his PhD years. Wilson later won the 2020 Nobel with Paul Milgrom for auction theory (a Nobel substantially about how information asymmetry shapes prices when bidders know more than auctioneers). Rick's PhD advisor was **Joel Demski**, a foundational figure in the economics of accounting / information economics. So the lineage runs: taught by Wilson (2020 Nobelist on info-and-prices) → advised by Demski → Yale faculty since 1985.
- **Yale colleagues who later won the Nobel in economics: Williamson, Holmstrom, Milgrom, Shiller, Phil Dybvig, and Douglas Diamond.** The single highest-leverage citation for *this* talk is **Diamond + Dybvig** — they shared the 2022 Nobel (with Bernanke) for the canonical Diamond–Dybvig 1983 model of bank runs, which is **directly the mechanism behind the Great Depression bank-run content in the invFix slide.** Suggested live framing: "Two of my Yale colleagues, Doug Diamond and Phil Dybvig, won the Nobel in 2022 for explaining exactly the kind of bank run we're going to look at in a few minutes." This converts a general "Nobel adjacency" claim into a specific, content-relevant credential.
- Co-founded Compensation Valuation Inc. (employee stock options) and RJA Asset Management.

**Deliverables for Piece 1 (Claude drafts, Rick reacts):**
1. A standalone "Going In" intro slide (or 2-slide sequence) that lives **before** c0 in the deck — NEW kind, probably typographic/photo. Rick on screen, Rick's hook line, transition into "Your rich uncle just died." Keep it under 90 seconds of speaking time.
2. The corresponding entries at the top of `speaker-notes.html` — replace the existing `⟶ Going In · TO BE WRITTEN` placeholder with the real script.

**Decisions to surface:**
- Headshot or no headshot? (If yes, Rick will need to drop a JPG into the workspace folder.)
- One slide or two? (My instinct: one slide with 3 reveal beats — name/role · Madoff hook · "you're about to be a buyer" handoff.)
- Does Rick want the Anderson/$400 origin story in there, or save that for warming, only used if there's silence to fill?

### Piece 2 — The "more than allocational efficiency" wedge

Rick's note from end of Session 10:

> *Points out that more than allocational efficiency is at stake. No investments mean less is produced means …*

The talk currently lands the diagnosis at "allocational efficiency" — things end up in the wrong hands; the Mint owner is stuck. That under-sells the stakes for an audience whose intuition about "why economics matters" is built around growth, jobs, and standard of living.

The deeper wedge: information asymmetry doesn't just **misallocate existing assets**. It **suppresses new production.** When companies can't get capital because investors can't tell good opportunities from bad, the good opportunities don't get funded. Things don't get built. Drugs don't get developed. Factories don't get expanded. Jobs don't get created. The macro consequence of micro information asymmetry is reduced economic growth.

**The chain to make explicit:**
1. Asymmetric info → investment market unravels (we already showed this in i0).
2. Capital doesn't flow to good opportunities.
3. Good opportunities don't get built. Production doesn't happen.
4. Less aggregate production → slower growth → fewer jobs, lower wages, less wealth.

This is bigger than "the Mint owner is stuck." It's "the country is poorer."

**Where it goes — three options for Rick to pick from:**

| Option | Where | What it looks like |
|---|---|---|
| A | New beat inside `c10` (ConceptCard) | Add a 4th visual cell or a sub-line to the asymmetric-state panel: "And it's not just *who has* the assets — it's *what gets made*. No good investments funded → less production → slower growth." |
| B | Standalone slide between `invFix` and `z1` | New kind, 3–4 beats. The chain laid out plainly: capital frozen → projects unbuilt → fewer jobs, slower growth. Acts as a bigger-stakes coda before z1's capstone hand-off. |
| C | Inside `invFix` as a 7th beat | After the closing-insight panel, one more reveal: "And the cost isn't only that capital sits idle. It's that the things that capital would have built — don't get built." |

My instinct: **Option B** is cleanest pedagogically (lets Rick take a breath, shifts register from "look at the mechanism" to "feel the stakes") but **Option A** is cheapest to ship and Option C is the smallest scope-add. Surface this trade-off and let Rick decide.

**Deliverables for Piece 2 (Claude drafts, Rick reacts):**
1. The slide (or in-place beat) per Rick's chosen option, following the established reveal pattern.
2. STEPS array entry + dispatcher wiring (if Option B).
3. Speaker-notes entry mirroring the new content.
4. JSX compile check + version bump (probably v4.5.0 since this is content arc, not patch).

**One nuance to flag before drafting:** the existing `c10` ConceptCard already has a "shared ignorance also works" middle panel — that's the *symmetric* ignorance state where markets clear at the average. The growth wedge applies to the asymmetric state, not the symmetric one. So inside c10 the wedge would attach specifically to the right-most "asymmetric breaks" panel.

### Piece 3 — "Coming Out": closing the talk after z1

Currently `z1` (capstone connections) ends with the navy "Wherever you find an information problem" coda baked into the App, then nothing. Rick needs a graceful exit: a moment that signals "the interactive is done, you're going to do something with this," and a hand-off back to whoever runs the rest of the program.

Things that probably belong in the close:
- A one-line "what to do with this": the specific instruction to look at their capstone project through this lens — what's the asymmetry, who knows what the other side doesn't, where could a fix come from?
- An invitation: questions, follow-up, contact path if they want to talk more about it after the talk. (Rick to decide how open he wants this to be — his Yale email is on his bio.)
- A thank-you: to Seeds of Fortune, to Yale Women in Economics, to the host who invited him.
- Optional: a reading or watching recommendation. Akerlof's 1970 paper is short and famous; Michael Lewis on 2008 (*The Big Short*) is right in their wheelhouse.

**Deliverables for Piece 3 (Claude drafts, Rick reacts):**
1. The closing slide (NEW, after z1) OR a "Coming Out" page in the speaker-notes only (if Rick prefers spoken-only close with no new slide).
2. The corresponding entry at the bottom of `speaker-notes.html` — replace `⟶ Coming Out · TO BE WRITTEN` with the real script.

**Decisions to surface:**
- Slide or no slide? (My instinct: yes, one slide — gives the audience a place to rest their eyes during the close, and signals "we are now in the conclusion.")
- How open does Rick want the door? (Email visible on screen vs. just spoken vs. "ask Seeds of Fortune to put you in touch.")

### Piece 0 — Final polishing of v4.4.0 (whatever Rick flags)

Before any of the above, Rick may have feedback from his end-of-Session-10 click-through. Things to expect (based on the scope of Session 10's restructure):

- **Section labels** on the new slides: `🔄 The Pattern` (synth), `🌱 Two Markets, Two Fixes` (combFix), `🏢 Investment Fixes` (invFix). Rick may want these tightened.
- **invFix beat 5** crisis cards: tone and length are the most likely thing to tune. Each crisis is currently 2–3 sentences; if it's too long for live pacing, trim Enron and FTX first (the framing for those is more dispensable than the Depression and 2008).
- **invFix beat 1 wording**: "Investments are tougher." — Rick may want this softened or different.
- **synth beat 1**: "Cars. iPhones. Capital." — verify the order matches what Rick says aloud.
- **i0 preamble**: $M units verified; if Rick wants $K instead, change INV_TIERS values + UnraveledMarketView's `wouldHave` strings.
- **combFix card body length**: each card currently concatenates `FIX_DATA.X.body + ' ' + FIX_DATA.X.outcome`. If too dense, switch to `body` only and move `outcome` into a separate small-text row.

Take Rick's actual feedback first, work top-to-bottom through whatever he flags, JSX-compile after every edit. *Then* move to Pieces 1 → 2 → 3.

---

## ⚠️ STANDING FLAGS FROM SESSION 10

These didn't get raised during Session 10 but may matter:

1. **The CrisisCallout component** is still in the codebase but no longer rendered (it was attached to the old i0; the new InvestmentFixesSlide carries its own multi-crisis content inline). Safe to delete in Session 11 cleanup if Rick wants the file lighter, otherwise harmless.
2. **The CostEscalation component** is still in the codebase from v4.2 R16 and also unused. Same call.
3. **c11's STEPS entry and FixCard are gone**, but `FIX_DATA.car` still exists (used by CombinedFixesSlide). Don't remove it.

---

## 📁 FILES IN WORKSPACE

| File | Status |
|------|--------|
| `akerlof-lemons-v4.html` | v4.4.0 — shipping |
| `akerlof-lemons.html` | v3.0 — disk fallback, DON'T TOUCH |
| `speaker-notes.html` | v4.4.0 — synced, with `Going In` + `Coming Out` placeholders awaiting Session 11 |
| `CONTINUATION-BRIEF.md` | The big v4.0–v4.2 brief — still valid for design rationale and locked decisions |
| `SESSION-10-BRIEF.md` | Session 10 plan — done, archive value only |
| `SESSION-11-BRIEF.md` | THIS FILE |

---

## 🚀 PROMPT TO START SESSION 11

```
Session 11 — wrapping the talk. Read in order:
1. /Users/ra1/Claude-Cowork-Projects/Seeds of Fortune Talk/SESSION-11-BRIEF.md
2. Load the interactive-tutorial-builder skill before any code work
3. Open Brain — search for: "217 Canner Associates Madoff", "Rick Antle Yale bio",
   "allocational efficiency growth wedge", and anything else this session needs
4. Auto-memory MEMORY.md
5. akerlof-lemons-v4.html (scan @changelog v4.4.0 + STEPS array)

Status: v4.4.0 shipping at 18 steps. Three pieces of work:
- Piece 0: any polishing Rick flags from his click-through
- Piece 1: "Going In" — Rick's intro slide(s) + flow into c0
- Piece 2: the "more than allocational efficiency" wedge (3 placement options)
- Piece 3: "Coming Out" — closing slide / script after z1

Producer mode applies: Rick sets vision, I build, I flag.
Local server on :8000. Chrome MCP should be online.

Talk is at 6 PM today (or whenever Rick says). Ship.
```
