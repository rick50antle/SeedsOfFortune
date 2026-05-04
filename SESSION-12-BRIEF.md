# Session 12 Brief — Seeds of Fortune Talk

**Talk:** Mon May 4, 2026 · 6 PM Zoom · ~40 HS juniors · Yale Women in Economics / Seeds of Fortune
**Status as of end of Session 11 (May 4, 2026):** `akerlof-lemons-v4.html` is at **v4.6.0** — 20 STEPS, JSX clean, speaker-notes synced. The Productive Efficiency concept slide (the one open design item from earlier in the day) has been built and shipped per Rick's design vote. There is no open design item carried into Session 12 — Session 11 closed clean.
**Producer mode applies:** Rick sets vision, Claude builds, Claude flags. Don't co-write — draft and react.

---

## ⛳ FIRST READS (in this order)

1. **This brief** (top to bottom).
2. **Global skills directive** at `/Users/ra1/YALEiE-Local/accounting-pedagogy-skills/CLAUDE.md`. Load **`interactive-tutorial-builder`** via `Skill: anthropic-skills:interactive-tutorial-builder` before touching code.
3. **Open Brain** — three thoughts from end of Session 11. Search:
   - `"Seeds of Fortune akerlof-lemons-v4 v4.5.5 shipping state"` — full state snapshot just before the productive-efficiency build
   - `"Seeds of Fortune Productive Efficiency concept slide"` — the design discussion + Rick's answers
   - `"productive efficiency pedagogical tension textbook"` — the dynamic-vs-productive nuance to flag if it comes up
4. **Auto-memory `MEMORY.md`** — Producer-role expectation, reveal-pattern conventions.
5. **`akerlof-lemons-v4.html`** v4.6.0 — scan @changelog v4.5.0 → v4.6.0 entries and the STEPS array. The new step is `prod`; the new component is `ProductiveEfficiencyCard`.
6. **`speaker-notes.html`** — synced to v4.6.0 (20 slides).

---

## 🚦 SHIPPING STATE (v4.6.0)

- File: `akerlof-lemons-v4.html` v4.6.0. JSX compiles cleanly.
- 20 steps in this order: **c0, c1, c2, c3, c5, c4, c5b, c6, c7, c8, p0, i0, synth, more, c10, prod, growth, combFix, invFix, z1**.
- v3.0 (`akerlof-lemons.html`) remains the disk fallback — DO NOT TOUCH.
- The v4.5.x and v4.6.0 changelog at the top of the file has the full Session-11 history (passes 1 through 7).

---

## ✅ WHAT SESSION 11 DELIVERED (recap)

Across seven sub-passes (v4.5.0 → v4.6.0), Session 11 delivered:
- **Polish pass on the click-through** (v4.5.0): c5 moved before c4, c12 retired, NEW `more` slide between synth and c10, NEW `growth` wedge after c10, UnraveledMarketView now beat-driven, "stack" wording replaced with "trust system" everywhere user-visible, TRUST surfaced as the through-line.
- **Bug fix + Apple body tightening** (v4.5.1): Apple body restructured (problem before fix, no overclaim); UnraveledMarketView gets `key={step.id}` so beat state resets between p0 and i0; new `more` slide added with the regulatory-fix family panel (later replaced).
- **c7 final beat + more slide rewrite + invFix toolbox box** (v4.5.2): c7 ends at the $2K equilibrium; `more` slide drops fix discussion in favor of the SCALE INSIGHT (adverse selection is the failure mode of anonymous markets); invFix gets a "Ways this effect is eased in other markets" box that references ACA / inspectors / degrees.
- **Scale → trust → crisis arc** (v4.5.3): invFix beat 7 closing + z1 coda both rewritten to land the through-line.
- **Small cleanup** (v4.5.4): ModeBar removed from c3, invFix beat 4 header relabeled.
- **c7 headline + p0/i0 walked-tier fade** (v4.5.5): c7 headline → "Reduce your offer"; population grid in p0/i0 fades the three better tiers when the "trades that don't" panel reveals.
- **NEW Productive Efficiency concept slide** (v4.6.0): `prod` step + `ProductiveEfficiencyCard` between c10 and growth. Same purple chrome and three-state structure as c10. Definition: *"A market is productively efficient when the things that should be made actually get made — when capital reaches the projects that should be built."* Footer: *"Same wedge as allocational. Different consequence: not 'wrong hands' — 'never made.'"* Per Rick's design vote: definition (A) softened, structure parallel to c10, placement (a) between c10 and growth, visual reuse BuildingSVG.

The Going-In and Coming-Out slide work originally scoped in SESSION-11-BRIEF.md was DEFERRED — Rick's polish notes during the click-through took priority and the talk happens today. Those remain candidates for a future session if Rick wants them.

---

## 🎯 SESSION 12 — OPEN ITEMS

There are **no required deliverables** for Session 12. The deck is shipping at v4.6.0. Possible work for Session 12 if Rick wants it:

1. **Going-In** intro slide — Rick's bio + Madoff trusteeship hook + transition into c0. Originally scoped in SESSION-11-BRIEF.md piece 1. Strongest credibility hook: 217 Canner Associates LLC (Madoff feeder fund liquidating trustee).
2. **Coming-Out** closing slide — graceful exit after z1, capstone-lens instruction, contact path, thank-yous. Originally scoped in SESSION-11-BRIEF.md piece 3.
3. **Polish from the actual talk** — whatever notes Rick brings back from delivering it tonight (May 4, 6 PM).
4. **PowerPoint deck wrapper** for the history-of-accounting and capstone-connection sections. Still not started.

If Rick has nothing for Session 12, fine — close it. The talk is the deliverable.

---

## 🛠️ WORKING ENVIRONMENT (unchanged from Session 11)

- **Local server:** Rick runs `python3 -m http.server 8000` from the talk folder. Use `http://localhost:8000/akerlof-lemons-v4.html?v=N`. Bump `N` after each edit to bust cache.
- **Chrome MCP:** Online ("Mac mini Chrome").
- **JSX-compile check:** see SESSION-11-BRIEF.md for the full incantation. Always compile after every edit.
- **Dev mode jump buttons:** triple-click the header.
- **Open Brain:** captures via `mcp__...__capture_thought`, retrieved via `search_thoughts`.

---

## 📁 FILES IN WORKSPACE

| File | Status |
|------|--------|
| `akerlof-lemons-v4.html` | **v4.6.0** — shipping |
| `akerlof-lemons.html` | v3.0 — disk fallback, DON'T TOUCH |
| `speaker-notes.html` | v4.6.0 — synced (20 slides) |
| `SESSION-10-BRIEF.md` | done; archive value |
| `SESSION-11-BRIEF.md` | done; archive value |
| `SESSION-12-BRIEF.md` | THIS FILE |
| `CONTINUATION-BRIEF.md` | still valid for v4.0 design rationale |

---

## 🚀 EXACT PROMPT TO START SESSION 12

Paste this verbatim into a new Cowork session:

```
Session 12 — Seeds of Fortune talk follow-on. Read in order:

1. /Users/ra1/Claude-Cowork-Projects/Seeds of Fortune Talk/SESSION-12-BRIEF.md
2. Load the interactive-tutorial-builder skill before any code work
3. Open Brain — search:
     "Seeds of Fortune akerlof-lemons-v4 v4.5.5 shipping state"
     "Seeds of Fortune Productive Efficiency concept slide"
     "productive efficiency pedagogical tension textbook"
4. Auto-memory MEMORY.md
5. akerlof-lemons-v4.html — scan v4.5.x + v4.6.0 changelog, the STEPS array

Status: v4.6.0 shipping at 20 steps. Session 11 closed clean. There are
no required deliverables for this session. Possible work — Going-In intro,
Coming-Out closing, polish from the actual talk delivery, or PowerPoint
wrapper for the history + capstone sections. Tell me what you want.

Producer mode applies: I set vision, you build, you flag.
Local server on :8000. Chrome MCP should be online.
```
