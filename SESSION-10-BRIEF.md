# Session 10 Brief — Seeds of Fortune Talk

**Talk:** Mon May 4, 2026 · 6 PM Zoom · ~40 HS juniors · Yale
**Status as of end of Session 9 (May 3, 2026 evening):** v4.3.10 shipping; speaker-notes.html in sync. Major restructure pending — Rick's batch of 10 feedback items below.
**Producer mode applies:** Rick sets vision, you build, you flag.

---

## ⛳ FIRST READS (in this order, don't skip)

1. **This brief** (top to bottom)
2. **`/var/folders/.../d9d0ed7b0f2fdec2/CLAUDE.md`** — Rick's global skills directive. `interactive-tutorial-builder/SKILL.md` is the relevant skill for this work. **Read the skill before writing code.**
3. **Memory:** `MEMORY.md` index in the auto-memory folder
4. **`akerlof-lemons-v4.html`** — at minimum scan the STEPS array (currently 16 steps) and the @version comment (4.3.10)
5. **`speaker-notes.html`** — the prep doc, kept in sync with the deck

---

## 🚦 SHIPPING STATE

- File: `akerlof-lemons-v4.html` v4.3.10 — JSX compiles cleanly, all visual changes verified by Rick clicking through
- 16 steps total: c0, c1, c2, c3, c4, c5, **c5b** (NEW precursor "ONE thing changes"), c6, c7, c8, c10, c12, c11, p0, i0, z1
- v3.0 (`akerlof-lemons.html`) remains the disk fallback — DO NOT TOUCH
- Speaker notes file is in sync; mirror any deck changes there

---

## 📐 ESTABLISHED PATTERNS (use these — don't reinvent)

### Click-to-advance reveals
The dominant pattern across the deck. Every component built this session uses it:

```jsx
const TOTAL_BEATS = N;
const [beat, setBeat] = useState(1);  // or 0 if first reveal happens on click
const advance = () => setBeat(b => Math.min(b + 1, TOTAL_BEATS));
const reveal = (visible) => ({
  opacity: visible ? 1 : 0,
  transform: visible ? 'translateY(0)' : 'translateY(6px)',
  transition: 'opacity 0.4s ease, transform 0.4s ease',
  pointerEvents: visible ? 'auto' : 'none',
});
```

Outer div has `onClick={advance}` and `cursor: beat < TOTAL_BEATS ? 'pointer' : 'default'`. Bottom of slide has dot indicator (one per beat) + "click to continue ▸" hint that hides at final beat. Reference HookSlide, PopulationView, MarketplaceView, LossVisualization, RuleChangeSlide, CascadeSlide, CascadeRevisionSlide.

### Speaker notes vs. on-screen content
- **Narrative** (in STEPS) = SPEAKER SCRIPT, hidden by default. Visible only when 📝 button toggled on (or `?notes=1`). Rendered with a "📝 SCRIPT" label.
- **Insight** (in STEPS) = on-screen lightbulb, always visible at App level — UNLESS you want it timed to a specific beat, in which case set `step.insight = null` and render the lightbulb inline in the component on the right beat.

### Tier color palette (don't override)
- Mint = gold `#c9a227`
- Good = green `#22c55e`
- Fair = orange `#f97316`
- Lemon = red `#dc2626`

Don't paint Mint green just because it's a "positive outcome" — that breaks the tier identity used everywhere else. Bar/icon colors track TIER. Verdict pills (BARGAIN green / OVERPAID red) are a separate channel and CAN use positive/negative coloring.

### Cascade pattern (TokenGrid + LotCalculation across beats)
For slides where TokenGrid + LotCalculation need to update across beats (sellers walking, offer changing), build a custom kind component that owns beat state and re-renders TokenGrid + LotCalculation per beat with computed activeTiers/offer. CascadeSlide (c6) and CascadeRevisionSlide (c7) are the references.

### Headline suppression
For typographic slides where the slide IS the slide (AbstractionSlide c12, RuleChangeSlide c5b), the App suppresses the headline via:
```jsx
display: (step.kind === 'abstraction' || step.kind === 'ruleChange') ? 'none' : 'block'
```
Add new kinds to that check as needed.

---

## 🛠️ WORKING ENVIRONMENT

- **Local server:** Rick runs `python3 -m http.server 8000` from the talk folder. File:// is blocked by Chrome MCP — always use `http://localhost:8000/akerlof-lemons-v4.html?v=N`. Bump `N` after each edit to bust cache.
- **Chrome MCP:** Online ("Mac mini Chrome" — `list_connected_browsers` returns it). The actual outer click handler can be flaky to drive programmatically; trust the JSX compile + the proven pattern, let Rick click through and report. Don't burn cycles trying to programmatically click-test cascade slides.
- **JSX-compile check after every edit:**
  ```
  cd "/sessions/.../Seeds of Fortune Talk" && node -e "const fs=require('fs'),babel=require('/tmp/node_modules/@babel/core');const html=fs.readFileSync('akerlof-lemons-v4.html','utf8');const m=html.match(/<script type=\"text\/babel\">([\s\S]*?)<\/script>/);try{babel.transformSync(m[1],{presets:['/tmp/node_modules/@babel/preset-react']});console.log('OK');}catch(e){console.error('FAIL:',e.message);}"
  ```
- **Dev mode jump buttons:** triple-click the header to enable.

---

## 🎯 RICK'S BATCH OF 10 (the next session's work)

These came in at end of Session 9, after the c7 walkthrough was verified. Take them in order — items 5–10 form the major structural restructure (problems separated from fixes; Fixes get their own section).

### 1. c6 caption fix
"Sellers don't wake up. Sellers have **better information**." — Reword the c6 narrative + caption + (optionally) headline. The "wake up" phrasing implies they were asleep before, which is wrong. They've always known their car; we just hadn't accounted for it.

### 2. c8 (FrozenMarketView) — soften the Lemon trade
"The Lemon-tolerant buyer isn't *necessarily happy*. He didn't get the kind of car he would have gladly paid for, but at least he didn't overpay for the car he got." — Update FrozenMarketView's left side (the Lemon trade) to not say "both happy". More like: "Trade happens. The buyer didn't get what they really wanted — but at least didn't overpay for what they got."

### 3. c8 — drop "Invisible if you're not looking for it."
Rick: "I don't know what 'Invisible if you're not looking for it.' means." Remove that line from the c8 insight. Replace with something cleaner if needed, or just trim.

### 4. c10 (ConceptCard / Allocational Efficiency) — risk asymmetry under shared ignorance
Rick wants this nuance added: "Markets also work [under symmetric ignorance], but **both seller and buyer bear risk**. The seller may not know and may never know, but the buyer would come to learn it the hard way." So the three-state ConceptCard's middle panel ("shared ignorance — works") should add the wrinkle that risk is borne asymmetrically *over time* even when info is symmetric *at the point of trade*.

### 5. c12 (AbstractionSlide) — REWORK
- Should unfold with **beats** (it's currently typographic but all-at-once)
- **Don't mention Carfax** — at this point in the deck (post-restructure), the fix hasn't been introduced yet
- The big punchline beat: **"It wasn't about the cars, it was about the information."** (note: "cars" not "lemons")
- Just the problem, no fix

### 6. p0 (iPhones) — strip the fix
Show the same problem (greyed-out "Good phones" walking, only Lemon market remains). **Don't show Battery Health fix yet.** Same pedagogical structure as c6 (cars problem) — adverse selection plays out, ends at the unraveled state.

### 7. i0 (Capital) — needs setup + strip the fix
Rick wants more setup. Suggested wording: "You have four investment opportunities. One is worth $20K, one is worth $14K, etc. If the seller knows more than you about the value of each particular investment..."
Then: show the market collapsing to only the lowest-value investments. **Don't show the SEC stack fix yet.**

(Note: investment values currently in INV_TIERS are in millions ($M). Rick's wording uses $K — match what the visual shows. Either keep $M and update Rick's script, or convert. Confirm with Rick when picking this up.)

### 8. NEW SLIDE — "Same problem, different markets"
After cars (c6/c7/c8), iPhones (p0), capital (i0) all show the SAME problem. New slide says:
> "Different markets, same problem: **Information**. Not the lack of it, the **distribution** of it. When sellers know more about what they're selling than the buyers, **adverse selection** applies and markets don't work so well."

This is the new abstraction slide that synthesizes the three problems before any fixes are introduced. Probably typographic, beat-by-beat reveal. Lands the "distribution not lack" insight cleanly.

### 9. NEW SLIDE — Concrete fixes (one slide)
Carfax + Apple Battery Monitor — both on ONE slide. Side-by-side cards showing each fix. The cars FixCard and the iPhone FixCard, repurposed and consolidated.

### 10. NEW SLIDE — Investment fixes + caveats
"How about investments? This is tougher. More abstract than cars or phones. **Always involves risk, no matter how much you know.** Then: things that ease the problem." This is the SEC institutional stack slide, but framed differently — acknowledging risk is irreducible, then listing what eases. The crisis callout (Great Depression / 2008 / MBS ratings) probably stays attached.

---

## 🔄 IMPLIED STRUCTURAL CHANGE

The new arc (post-Session-10) becomes:

| # | ID | Section | Beat |
|---|----|---------|------|
| 1 | c0 | hook | inheritance (3 beats) |
| 2 | c1 | population | 4 cars + repair + value (6 beats) |
| 3 | c2 | listings | 4 listings + lightbulb (6 beats) |
| 4 | c3 | symmetric | $11K, sellers don't know (standard) |
| 5 | c4 | spin | $11K spin |
| 6 | c5 | lossViz | 4 outcomes + summary (6 beats) |
| 7 | c5b | ruleChange | "ONE thing changes" (5 beats) |
| 8 | c6 | cascade (cars problem) | 5 beats (REWORD per item 1) |
| 9 | c7 | cascadeRevision (cars problem) | 4 beats |
| 10 | c8 | frozen (cars problem) | (REWORD per items 2+3) |
| 11 | p0 | NEW iPhones problem (no fix) | per item 6 |
| 12 | i0 | NEW capital problem (no fix) | per item 7 |
| 13 | NEW | "Same problem, different markets" | per item 8 — the synthesis |
| 14 | c10 | concept (allocational efficiency) | (per item 4 — add risk wrinkle) |
| 15 | c12 | abstraction (REWORKED — beats, no Carfax) | per item 5 |
| 16 | NEW | Concrete fixes: Carfax + Battery | per item 9 |
| 17 | NEW | Investment fixes (SEC stack + risk caveat + crisis) | per item 10 |
| 18 | z1 | capstone connections | unchanged |

That's ~18 steps (up from 16). The order moves: **all problems first → synthesis → concept → pivot → fixes → capstone**. This is a real arc improvement: pattern recognition compounds, then fixes are presented as solutions to a problem the audience now feels.

The current STEPS array order has c10 before c12. Item 5's reworked c12 ("It wasn't about the CARS, it was about the INFORMATION") may want to move so that c10 (concept) comes AFTER c12 (the punchline) — or stays before. Confirm with Rick when sequencing.

---

## ⚠️ FLAGS / DECISIONS TO RAISE WITH RICK

1. **i0 units ($K vs $M).** Rick's item 7 wording uses $K but INV_TIERS uses $M. Ask which.
2. **Where does c10 (concept) go in the new arc?** Before or after c12 (the abstraction)? The current order has c10 → c12 → c11. Item 5 may want c10 → NEW synthesis → c12, or c12 → c10, etc.
3. **"Same problem, different markets" slide — typographic or visual?** Could be a clean typographic slide like c12, or could reuse a faded/iconographic visual showing the three markets side by side.
4. **Crisis callout placement.** Currently attached to i0 (capital) FixCard via `crisesBeat: true`. Where does it live in the new structure? Probably with item 10's investment-fixes slide.
5. **CapstoneConnections (z1)** — unchanged unless Rick wants the per-topic copy adjusted to reflect the new "fixes ease, don't solve" framing.

---

## 🛠️ EXECUTION ORDER (suggested for next session)

Do tactical fixes (items 1–4) first since they're small and reduce churn. Then the bigger items (5–10) which together form the structural restructure.

1. Pass A — Items 1, 2, 3, 4 (caption + insight rewordings; ConceptCard middle-panel wrinkle)
2. Pass B — Items 5, 6, 7 (rework c12, strip fix from p0, expand+strip i0)
3. Pass C — Items 8, 9, 10 (add 3 new slides: synthesis, concrete fixes, investment fixes)
4. Reorder STEPS array, verify dispatcher handles all kinds, JSX-compile, click-through
5. Sync speaker-notes.html (renumber slides, add new entries, update changed ones)

Estimated effort: 4–6 hours of focused work. Talk is at 6 PM tomorrow so ~20 working hours available.

---

## 📁 FILES IN WORKSPACE

| File | Status |
|------|--------|
| `akerlof-lemons-v4.html` | v4.3.10 — shipping |
| `akerlof-lemons.html` | v3.0 — disk fallback, DON'T TOUCH |
| `speaker-notes.html` | In sync as of v4.3.9 caption update; needs slide-numbering bumps when c5b structure changes again |
| `CONTINUATION-BRIEF.md` | The big canonical brief through Session 9 — still valid for the v4.0 design rationale and locked decisions |
| `SESSION-10-BRIEF.md` | THIS FILE — what's on deck for Session 10 |

---

## 🚀 PROMPT TO START SESSION 10

```
Session 10 — finishing the talk for tomorrow's 6 PM run.

Read in order:
1. /Users/ra1/Claude-Cowork-Projects/Seeds of Fortune Talk/SESSION-10-BRIEF.md
2. Your global skills directive (interactive-tutorial-builder is the relevant skill)
3. Auto-memory MEMORY.md

Status: v4.3.10 shipping with 16 steps; Rick's flagged 10 follow-ups
(items 1–4 small, items 5–10 a real restructure that moves all
problems before fixes and adds 3 new slides). Run those in 3 passes
(A: 1–4, B: 5–7, C: 8–10), with Rick reviewing after each pass.

Producer mode applies: Rick sets vision, I build, I flag. Local server
will be running on port 8000. Chrome MCP should be online.

Talk is at 6 PM today. Ship.
```
