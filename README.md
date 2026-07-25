# Traveller Character Sheet — Juzo Okita

An interactive, self-contained web character sheet for **Juzo Okita**, a Star Marines veteran turned bounty hunter in the [*Traveller* 2nd Edition](https://www.mongoosepublishing.com/collections/traveller-2e) RPG.

> **Live:** https://traveller2e.pages.dev/

Built as a single static HTML file — no build step, no dependencies, no backend. Open `index.html` in a browser and it just runs. Edits persist locally via `localStorage`.

---

## The character

Juzo Okita — a 34-year-old human from Glisten, mustered out of the Star Marines as a Force Commander after a four-term career that ended in a moral crisis. The sheet encodes his full history: characteristics, skills (with specialities and DM totals), gear and finances, armour and weapons, a four-term career timeline, and his resignation letter to the childhood friend he was ordered to execute.

| | |
|---|---|
| **Name** | Juzo Okita |
| **Homeworld** | Glisten |
| **Career** | Star Marines → bounty hunter |
| **Rank** | Force Commander (ret.) |
| **Signature loadout** | Gauss Rifle (lazer sight), Poly Carapace armour, frag/aerosol/stun grenades |

## Features

- **Editable in-browser** — characteristics, skills, inventory, and finances are all live-editable; the sheet recomputes DMs and totals as you type.
- **Dice-roll helper** — click a characteristic to roll 2d6 ± mod.
- **Skill study tracker** — log weeks/periods spent training a skill.
- **Load/encumbrance** — running totals for carried mass with an encumbered indicator.
- **Career timeline** — a visual five-stage (Academy + 4 terms) history.
- **Declassified letter** — the backstory, rendered as a RESTRICTED in-universe letter.
- **Sound toggle** — optional UI feedback sounds, mutable.
- **Cyberpunk/HUD aesthetic** — Orbitron/Rajdhani/Inter, scanline overlay, neon accents, fully responsive.

## Repository contents

| Path | Purpose |
|---|---|
| `index.html` | The complete, self-contained character sheet (HTML + CSS + JS in one file). |
| `Avatar.png` | Character portrait, referenced by the sheet. |
| `CharacterSheet.md` | Structured data extract the sheet was transcribed from (source of truth). |
| `Career.txt` | Raw career-term notes. |
| `Backstory.txt` | Raw text of the resignation letter. |
| `1.png` – `4.png` | The original scanned character-sheet pages the data was transcribed from. |

## Run locally

No tooling required. Either:

1. Open `index.html` directly in a browser, or
2. Serve the folder (handy for accurate asset paths):

```powershell
python -m http.server 8000
# → http://localhost:8000
```

## Deploy

The sheet is deployed to **Cloudflare Pages** as static assets. The deploy bundle is just `index.html` + `Avatar.png`:

```powershell
npx wrangler pages deploy . --project-name=traveller2e --branch=main
```

## Tech notes

- Single-file build: one `index.html`, no external JS/CSS (only Google Fonts via CDN).
- State versioned under `localStorage` key `juzo_okita_v2` with a `deepMerge` against defaults, so new fields added to the sheet don't break older saved data.
- All values defensive-coerced (`Math.max(0, …)`, `||0` fallbacks) so a partially-saved state never renders `NaN`.

## License

[MIT](LICENSE) — the code and sheet design are free to use and adapt. *Traveller* and related setting material are property of Mongoose Publishing; this is a fan-made character sheet and makes no claim on them.