# Wavelength 🎯

A browser-based implementation of the [Wavelength](https://wavelength.zone/) party game, played in Spanish.

## How to Play

1. Set up teams (2–5) and enter player names.
2. The **Psíquico** (Psychic) looks at the hidden target on the spectrum board and gives a one-word clue hinting at where it falls between two opposite concepts (e.g. between *Frío* and *Caliente*, they might say *"Café"*).
3. The team discusses and drags the needle to where they think the target is.
4. Click **Ocultar** to lock in the answer, then **Confirmar** to reveal the target.
5. Score points based on how close the needle is to the center:
   - 🔵 **5 pts** — Bullseye
   - 🟠 **3 pts** — Close
   - 🟡 **1 pt** — Near
   - ⬜ **0 pts** — Miss
6. Click **Siguiente** to pass to the next team, or **Omitir** to skip the current clue pair.

## Running Locally

No build step required. Just open `index.html` in a browser:

```bash
open index.html
```

Or serve it with any static file server:

```bash
npx serve .
```

## Deployment

Pushes to `main` automatically deploy to GitHub Pages via `.github/workflows/static.yml`.

## Project Structure

```
index.html   # Entire application — HTML, CSS, and JS in one file
```

All game content (clue pairs) and logic live in `index.html`. To add new spectrum pairs, append entries to the `clues` array in the script section, following the `["low/negative", "high/positive"]` convention.
