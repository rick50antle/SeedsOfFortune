# Seeds of Fortune Talk — Continuation Brief
*(Updated 2026-05-02, after session 2)*

---

## The Assignment

Rick Antle (Yale, rick.antle@yale.edu) is giving a **45-minute talk on Monday, May 4, 2026** to the Seeds of Fortune program at Yale — ~40 high school juniors (majority women), introduced to economics and finance via Yale Women in Economics. Students do capstone projects afterward.

**Goal:** Introduce information asymmetry in markets as a conceptual lens students can apply to their capstone work.

**Collaboration mode:** Producer. Rick sets the vision and direction; Claude builds assets and flags decisions that need his call.

---

## Talk Arc (locked)

| Segment | Time | Content |
|---------|------|---------|
| Hook | 5 min | Lived experience of an information gap |
| Akerlof + visual | 12 min | Used cars → iPhones → investment (see interactive tool) |
| History thread | 10 min | Light touch: Babylon → Pacioli → modern info processing |
| Thread to today | 8 min | SEC, financial disclosure |
| Capstone connection | 7 min | Information as hidden thread in all four capstone topics |
| Close | 3 min | Information as invisible infrastructure |

---

## Files in Workspace (`/Users/ra1/Claude-Cowork-Projects/Seeds of Fortune Talk/`)

| File | Status | Notes |
|------|--------|-------|
| `akerlof-lemons.html` | ✅ Complete (v2.0) | 14-step interactive presenter tool — see below |
| `CONTINUATION_BRIEF.md` | This file | — |

**Source material for history section:**
`/Users/ra1/Claude-Cowork-Projects/Accounting_Origins/` — Babylon/Pacioli content from Rick's prior tutorial project

---

## Interactive Tool: akerlof-lemons.html (v2.0)

**What it is:** A single-file React presenter tool (no build tools, opens in browser). Click through 14 steps on a projected screen while talking.

**Three-section arc:**

### Section 1: Used Cars (c0–c7, 8 steps)
- c0: Facebook Marketplace intro, all tokens gray (nobody knows)
- c1: Symmetric ignorance thought experiment — avg $11K, market works
- c2: Seller learns truth — information asymmetry introduced
- c3: Offer $11K — Mint and Good sellers refuse
- c4: Tiers 0+1 exit → new avg $5,600
- c5: Tier 2 exits → only lemons, avg $2K (death spiral badge)
- c6: Market failure conclusion — only lemons remain
- c7: Carfax fix (~$40) — Fix Card shown

### Section 2: iPhones (p0–p1, 2 steps)
- p0: Same structure applied to used iPhones, offer $420
- p1: Battery Health fix (free but effortful) — bridge to investment

### Section 3: Investment Capital (i0–i2, 3 steps)
- i0: 10 companies seeking capital, avg offer $11M
- i1: Strong companies exit → death spiral to $2M / distressed only
- i2: SEC 1934 fix + Cost Escalation panel ($40 → free → $100K–$10M+/yr)

### Closing (z0, 1 step)
- Cost Escalation summary + Capstone Connections panel

**Tier math (cars and investment share same proportions):**
- 2× Mint/Strong: $20K / $20M
- 3× Good/Solid: $14K / $14M
- 3× Fair/Struggling: $8K / $8M
- 2× Lemon/Distressed: $2K / $2M
- Full market avg: $11K / $11M
- After tiers 0+1 exit: $5.6K / $5.6M
- After tier 2 exits: $2K / $2M

**Key visual mechanics:**
- Token grid: tier rows (car SVGs / phone SVGs / building SVGs)
- Info-mode pill bar: No Info → Symmetric → Asymmetric → Fixed ✓
- Faded (18% opacity) tokens = exited sellers
- Calculation table with buyer's offer highlighted
- Fix Cards (section-specific)
- Death spiral badge (red)
- Dev mode: triple-click header → step-jump buttons

---

## The Escalating Cost Thread

This is the unifying narrative across all three sections:

| Market | Fix | Cost |
|--------|-----|------|
| Used cars | Carfax | ~$40 |
| Used iPhones | Battery Health (iOS) | Free, but buyer must seek it |
| Capital markets | SEC/Audit/GAAP | $100K–$10M+/yr |

The insight: the cost of the information fix scales with the stakes. Markets don't fail randomly — they fail along information fault lines.

---

## Capstone Connections (built into closing slide)

| Topic | Information angle |
|-------|-------------------|
| IPOs | Roadshow + S-1 filing = mandatory disclosure before pricing |
| Fintech / Robinhood | Democratized market data access (previously institutional-only) |
| Housing Finance | Mortgage underwriting = structured information gathering |
| Credit Markets | Credit scores = standardized info that solved the personal lending lemons problem |

---

## What Remains to Build

### 1. PowerPoint Deck (primary remaining asset)
The talk needs a slide deck to run alongside the interactive tool. Suggested structure:

- **Hook slides (5 min):** Open with a relatable information gap scenario — maybe buying something sight-unseen. No jargon, just the feeling.
- **Akerlof bridge (2 min):** "Here's the economist who formalized this" — 1 slide, Akerlof 1970, Nobel 2001. Then hand off to the interactive tool for the 10-min demo.
- **History thread (10 min):** Babylon clay tablets → Pacioli double-entry (1494) → telegraph/ticker → modern databases. Light touch, vivid images. Source: Accounting_Origins folder.
- **Thread to today (8 min):** SEC 1934 → GAAP → Sarbanes-Oxley → XBRL. Information disclosure as infrastructure.
- **Capstone connection (7 min):** One slide per capstone topic (or 2-slide cluster). Use the table above.
- **Close (3 min):** Information as invisible infrastructure — the "cost of knowing" framing.

**To build:** Read `pptx/SKILL.md` before starting. Check `Accounting_Origins/` folder for Babylon/Pacioli content to pull into history slides.

### 2. One-Page Leave-Behind (optional)
A single printed/PDF handout connecting information asymmetry to all four capstone topics. Could double as a reference card students keep. Not yet started.

---

## Design Decisions Already Made

- **Car framing:** Private sellers (Facebook Marketplace), not a dealer lot — seller's information acquired as byproduct of ownership
- **4-tier heterogeneous model** (not binary peach/lemon) — allows consistent cascade logic
- **iPhone example:** Included as bridge. The fact that the problem IS largely solved (Battery Health) is the point — it shows (a) same structure applies, (b) it was fixed, (c) but you have to do the work
- **Investment fix cost:** Emphasis on the institutional scale of SEC/audit costs vs. $40 Carfax
- **History section:** Light touch only. A little Babylon, a little Pacioli, a little modern. Not a deep historical narrative.

---

## Session Notes

- Session 1 (prior): Designed the arc, settled on 3-section structure, chose Option B (heterogeneous tiers), established escalating-cost-of-fix thread
- Session 2 (2026-05-02): Complete rewrite of akerlof-lemons.html → v2.0. 14 steps, SVG token shapes, full cascade math, fix cards, cost escalation panel, capstone connections. **PowerPoint not yet started.**

---

## Quick Context for Next Session

Read this brief first. Then check `akerlof-lemons.html` exists and open it to verify it renders. The next task is almost certainly the PowerPoint deck — read `pptx/SKILL.md` before writing any slides, and check `Accounting_Origins/` for usable history content.
