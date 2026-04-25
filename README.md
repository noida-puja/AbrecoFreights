# Abreco Freight — Brand Identity Pitch

A multi-page brand-identity site for **Abreco Group** (founded 2010, Jebel Ali, Dubai), with the **Freight vertical** as the founding fire.

Presented by **Puja Raghav** · HR Team · Abreco Freight Vertical · [noida.puja@gmail.com](mailto:noida.puja@gmail.com).

## Structure

| File | Purpose |
|---|---|
| `index.html` | Landing page — hero, animated 6-callout infographic showcase, vision summary, nav cards, footer |
| `story.html` | Deep 22-panel pitch — 12 chapters on the logo + 8 chapters on company info (journey, network, services, leadership, credentials, why, connect) |
| `infographic.html` | Standalone product-style infographic (1800×1350) — six numbered callouts around the logo |
| `infographic.png` | Rendered infographic at 3600×2700 (retina) |
| `logo.png` | Transparent-background logo (generated from the source JPEG) |
| `WhatsApp Image 2026-04-21 at 12.07.36 PM.jpeg` | Original logo source |
| `Screenshot 2026-04-25 212827.png` | Original sample text from user's first draft |

## Scripts

| Script | What it does |
|---|---|
| `make_transparent_logo.py` | Converts the logo JPEG → `logo.png` with transparent background (alpha = 255 − min(R,G,B), with white-decontamination so the colours stay vivid) |
| `render_infographic.py` | Renders `infographic.html` → `infographic.png` via Playwright at 2× DPR |
| `snap.py` | Visual verification — opens `index.html` and `story.html` in headless Chromium, screenshots key sections into `screens/` |

## Running locally

Just open `index.html` in a browser — everything is self-contained (Google Fonts loaded via CDN, logo as a relative `logo.png` reference).

To re-render the static infographic or take fresh visual checks:

```bash
pip install playwright pillow
python -m playwright install chromium
python make_transparent_logo.py    # if logo needs re-converting
python render_infographic.py       # regenerates infographic.png
python snap.py                     # captures screens/ for review
```

## Design system

- **Type:** Fraunces (display serif, variable opsz/SOFT axes) + Inter (body sans), via Google Fonts
- **Colour:** Brand red `#e63048`, navy `#0e4f8a`, sky `#1f93cd`, cream `#d4c5a0`; ink/off-white on near-black background for the dark theme
- **Theme:** Dark editorial across the live pages, light editorial for the static infographic
- **Annotations:** Thin SVG leader lines + ring-and-core dot markers (brand-coloured) — Apple/Stripe spec-sheet style

## Animation rules — landing showcase

The landing-page infographic cycles through six callouts:

| Beat | Time | Visible |
|---|---|---|
| 01 The Founding Fire | 0s | 1 |
| 02 The Word | 3s | 1+2 |
| 03 The Body of Fire | 6s | 1+2+3 |
| 04 Two-Toned Depth | 9s | 1+2+3+4 |
| 05 The Forward Foot | 12s | 1+2+3+4+5 |
| 06 The Hidden 'A' | 15s | All 6 |
| **Hold** | 15–20s | All 6 stay |
| **Reset → restart** | 20.7s | back to 1 |

Animation pauses when the section is offscreen and resumes when scrolled back into view.
