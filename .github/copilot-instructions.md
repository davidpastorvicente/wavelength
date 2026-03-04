# Copilot Instructions

## Project Overview

This is a single-file Spanish-language implementation of the Wavelength party game. The entire application lives in `index.html` — HTML structure, CSS styles, and JavaScript game logic are all co-located in that one file. There is no build step, no package manager, and no test suite.

## Architecture

All game logic is inline JavaScript at the bottom of `index.html`. Key areas:

- **`clues` array** (line ~268): All Spanish spectrum concept pairs (e.g. `["Frío", "Caliente"]`). This is the primary content to extend.
- **Game state variables**: `players`, `targetAngle`, `currentPlayerIndex`, `isDragging`, `isTargetVisible`, `canMoveNeedle`.
- **`setTargetArea()`**: Generates a random `targetAngle` (-90 to 90) and renders the scoring zones via a `conic-gradient` on `#targetArea`.
- **`calculateScore(angle)`**: Compares needle angle to `targetAngle`; zones are ±4.5° (5pts), ±13.5° (3pts), ±22.5° (1pt), else 0.
- **Needle interaction**: Mouse and touch drag events on `#needleContainer` rotate `#needle` via CSS `transform: rotate()`. Angle is extracted by parsing the transform string.
- **Game flow**: `startGame()` → `newRound()` → player drags needle → toggle button cycles hide/reveal → score shown → `nextRound`.

## External Dependencies (CDN only)

- **TailwindCSS** (CDN) — utility classes; custom theme extends `primary` (#3b82f6) and `secondary` (#38a169), plus `orbitron` and `roboto` font families.
- **canvas-confetti** (CDN) — triggered on 5-point scores.
- **Google Fonts** — Roboto and Orbitron.

## Deployment

Deployed automatically to GitHub Pages on push to `main` via `.github/workflows/static.yml`. The entire repo root is uploaded as the artifact.

## Key Conventions

- The UI language is **Spanish** — all game text, button labels, clue pairs, and instructions are in Spanish.
- Score zone colors map to CSS classes: `.score-5` (#adc8da blue), `.score-3` (#ee7648 orange), `.score-1` (#fec942 yellow), `.score-0` (#eeefe8 off-white).
- The `conic-gradient` is centered at `50% 100%` (bottom center) and spans 0–180deg, matching the semicircle board layout.
- `canMoveNeedle` gates all drag interactions — it is only `true` after the target is hidden and before it is revealed.
- The toggle button (`#toggle`) changes text and color class to reflect current phase: "Ocultar" → "Confirmar" → hidden after reveal.
- Adding new clue pairs: append `["left concept", "right concept"]` to the `clues` array, keeping the convention of `[negative/low, positive/high]`.
