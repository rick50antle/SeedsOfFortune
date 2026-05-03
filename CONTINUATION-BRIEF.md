# Seeds of Fortune Talk — Continuation Brief
**Last updated:** May 2, 2026  
**Talk date:** Monday, May 4, 2026 (Zoom, ~45 min)  
**Audience:** ~40 high school juniors, majority women, at Yale  
**Topic arc:** Information asymmetry in markets → lens for capstone projects

---

## What this talk is

Rick Antle (Yale) introduces Akerlof's lemons model to Seeds of Fortune students as a framework for understanding information problems they might tackle in capstone projects. The main interactive tool is `akerlof-lemons.html` — a React-based presenter tool with ~14 steps.

---

## What was built this session

All files live in `/Users/ra1/Claude-Cowork-Projects/Seeds of Fortune Talk/`.

### Completed deliverables

| File | What it is | Status |
|------|-----------|--------|
| `graphics-review.html` | Scored all 7 main graphics in akerlof-lemons.html against 3 criteria | Done |
| `design-sketches-c0.html` | First-round concept sketches for the c0 opener | Done (superseded) |
| `design-sketches-c0-v2.html` | Second-round sketches; user selected Variation 1 (straight rows) | Done (superseded) |
| `design-sketches-buyer-cell.html` | 4 options for collapsing buyer's 4 cars to one image | Done (superseded) |
| `marketplace-deck.html` | First interactive dual deck (v1) | Done (superseded) |
| `marketplace-deck-v2.html` | **Primary c0 opener** — dual flip-deck + You simulation | ✅ Final |
| `loss-visualization.html` | **Loss breakdown slide** — animated bars across 4 outcomes | ✅ Final |

### Key design decisions locked in

**4-car market (1 per tier):**
- Mint — $20,000 (gold `#c9a227`)
- Good — $14,000 (green `#22c55e`)
- Fair — $8,000 (orange `#f97316`)
- Lemon — $2,000 (red `#dc2626`)
- Average = $11,000

**The $20K simulation:**
- Buyer = "You"; offer $20K to get a car guaranteed
- Fair deal only if Mint draw (1 in 4 = 25%)
- Overpaid if Good (+$6K), Fair (+$12K), or Lemon (+$18K) = 3 in 4 = 75%
- Expected value received = $11K = 55% of $20K paid
- Average loss = $9,000

**Pedagogy:** Experience-first — student spins and experiences uncertainty before theory is explained. Running record lets the 3/4 burn pattern emerge empirically.

**Buyer visual:** Stacked gray car thumbnails (3-layer shadow deck) showing "all 4 look the same." Seller cards flip one at a time revealing colored car + quality badge + price.

---

## What `marketplace-deck-v2.html` contains

**Left panel:** Seller flip-deck — 4 cards, each with colored car SVG + tier badge + price. Shadows disappear as cards are revealed. Done state shows mini-row of all 4 cars + value range.

**Right panel:** Static 4 gray car thumbnails (stacked). Below: simulation panel — "Offer $20,000" button triggers spin animation (7 flashes with escalating delays [80,80,90,100,120,150,200ms] for slowing-down feel), then reveals outcome with verdict (✓ Fair deal / ⚠ Overpaid / ✕ Overpaid).

**Running record:** `totals`, `fairCt`, `burnedCt` counters update live with each draw. Resets with "Start over."

---

## What `loss-visualization.html` contains

4 outcome rows, each: colored car SVG + tier badge + "1 in 4" chip + animated split bar (value received = tier color left, money burned = red right) + dollar amounts.

Bar proportions: Mint 100%/0%, Good 70%/30%, Fair 40%/60%, Lemon 10%/90%.

Animation triggers on load (150ms delay) via `.animated` class toggle on CSS custom properties `--vw` / `--lw`.

Dark Yale-blue summary panel: "3 in 4 overpay" (red), "1 in 4 fair deal" (green), "$9,000 avg loss" (gold).

Expected value bar: green gradient, animates to 55% width = $11K/$20K.

Gold insight box: "The $20K offer isn't naive — it's rational. The problem is you can't tell which car you're getting... That gap is costing you $9,000 on average."

---

## Remaining work

### High priority (before May 4)

1. **Rick reviews loss-visualization.html** — confirm animation speed, $9K figure prominence, whether to add a "Try again" button, whether the insight box wording is final.

2. **Integrate into akerlof-lemons.html** — replace step c0 (current token grid) with:
   - `marketplace-deck-v2.html` content as the new c0 opener
   - `loss-visualization.html` as a new step immediately following
   - Confirm with Rick before touching the main file

3. **Fix remaining graphics in akerlof-lemons.html** — `graphics-review.html` flagged:
   - Token Grid: Mint color is blue (should be gold `#c9a227`); labels are 9px (invisible on Zoom)
   - Cost Escalation panel: doesn't convey the $40→$10M scale
   - Other panels: minor label size / contrast issues

4. **PowerPoint deck** — Full 45-min talk deck not started. This is the biggest remaining asset.

### Lower priority

- Mobile-optimize any standalone files (probably not needed — this is a Zoom presenter tool, not student-facing HTML)
- Archive design sketch files once integration is confirmed

---

## Key files to read when resuming

| If you're resuming... | Read first |
|----------------------|-----------|
| Any akerlof-lemons work | `akerlof-lemons.html` (full React tool, ~14 steps) |
| c0 integration | `marketplace-deck-v2.html` + `loss-visualization.html` |
| Graphics review decisions | `graphics-review.html` |
| PowerPoint | Read `pptx/SKILL.md` before starting |
| Tutorial work | `interactive-tutorial-builder/SKILL.md` |

---

## Color palette (project standard)

```
primary:    #00356b  (Yale blue — headers, buttons)
sand:       #f5f1e8  (page background)
accent:     #c9a227  (gold — highlights, Mint tier)
earth:      #8b7355  (secondary text)
earthLight: #d4c4a8  (borders, dividers)
earthDark:  #5c4d3d  (dark text on light)
clayLight:  #e8dcc8  (info cards)
success:    #22c55e  (Good tier, fair deal)
warning:    #f97316  (Fair tier)
error:      #dc2626  (Lemon tier, burned)
```

---

*Brief written May 2, 2026. Talk is May 4. Two days remaining.*
