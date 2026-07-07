# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

GapCalc is a free, client-side web calculator suite for South African welders and fabricators. Live at [gapcalc.com](https://gapcalc.com).

## Development

No build system or package manager. The entire app is a single `index.html` file — open it directly in a browser or serve it:

```bash
python -m http.server 8000
```

There are no tests, no compilation step, and no dependencies to install.

## Architecture

Everything lives in `index.html` (~6,800 lines): HTML structure, CSS (in `<style>`), and JavaScript (in `<script>`). The app is a tab-based SPA with fourteen calculator/utility tools, all calculations run client-side with zero external JS dependencies.

**Tools and their main calculation functions:**

| Tool | Function | What it does |
|------|----------|--------------|
| Gap Calculator | `calcGaps()` | Equal bar/slat spacing — formula: `gap = (frame - bars*width) / (bars-1)` |
| Cut List | `calcCutList()` | Plans cuts from stock lengths with kerf compensation, offcut sizes, waste % |
| Weight Calculator | `calcWeight()` | Steel (7.85 g/cm³) and timber order weight; bakkie load indicator |
| Angle Cuts | `calcAngle()` | Short/long point, cut face, offset; generates SVG cut diagrams dynamically |
| Rod Estimator | `calcRodEstimator()` | Rod type recommendations by material/joint/position; quantity with skill wastage |
| Job Costing | `calcCosting()` | Material + labour + consumables + delivery; margin vs. markup; printable ZAR quote |
| Bolt Spacing | `calcBolts()` | Evenly spaces bolts, screws, rivets, or hinges along a length |
| Drill Reference | (static lookup, `setDrillUnit()`) | Tap, clearance, and countersink drill sizes; metric and imperial |
| MIG Wire Estimator | `calcMIG()` | Wire diameter, joint type, thickness → kg needed and reels to buy |
| Weld Settings Guide | `calcSettings()` | Recommended MIG/flux-core settings; includes a weld defect troubleshooter |
| Job Timer | `startTimer()` / `stopTimer()` et al. | Tracks time per task; totals send straight to Job Costing |
| Paint & Primer Coverage | `calcPaint()` | Paint/primer/rust-converter quantity from surface area (`calcSurfaceArea()`, `calcOptimalTins()`) |
| Sheet Metal Flat Pattern | `calcSheet()` | Flat blank size and bend allowance with K-factor per material |
| Pipe & Tube Bending | `calcBend()` | Developed length and overbend angle for pipe/tube bends |

**Key globals and data structures:**
- `BAR_PRESETS`, `GAP_PRESETS` — preset arrays for the gap calculator
- `PROFILE_FIELDS`, `TIMBER_PRESETS` — metadata for weight calculator profiles
- `wMaterial`, `wProfile`, `labourMode`, `vatEnabled`, `deliveryEnabled` — UI state globals
- Results render via direct `.innerHTML` assignment; no virtual DOM or state framework

**Analytics:** Google Analytics (`gtag.js`) fires events on each calculator use.

**Styling:** Dark theme, `#f5820a` orange accent, CSS custom properties, fully responsive. Fonts loaded from Google Fonts (DM Sans, DM Mono, Bebas Neue).

## Important Context

- All prices/weights use South African context (ZAR, bakkie load, local steel suppliers)
- The angle cuts SVG diagrams are generated dynamically — see `drawAngleDiagram()` or similar functions for the SVG logic
- Job costing supports dynamic line items (add/remove materials and consumables rows)
- Creator: Brendan Glover — [@brendanglover_x](https://x.com/brendanglover_x)
