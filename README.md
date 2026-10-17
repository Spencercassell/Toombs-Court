# Toombs Court

Leasing & marketing website for 1 Toombs Court, Nantucket, MA — a new rental development leased directly by McNeil Development. Built per `BRIEF.md`.

Static HTML/CSS/vanilla JS. No build step, no framework, no backend. Deploys on Vercel as-is.

## Project structure

```
toombs-court-site/
├── index.html          # single-page site — all sections
├── css/styles.css      # all styling (design tokens at the top)
├── js/main.js          # nav, scroll-reveal, availability rendering, gallery lightbox, inquiry form
├── data/units.json     # single source of truth for unit-type availability & pricing
├── images/             # optimized WebP assets only (no raw originals committed)
├── favicon.svg
├── BRIEF.md             # the build brief this site was built from
└── README.md
```

## Updating unit availability

Edit `data/units.json`. The homepage fetches this file at runtime and renders the unit-type cards in the Availability section — no HTML changes needed for a rent or availability update.

- `unitTypes[]` — one entry per unit type (`studio`, `1br`, `2br`, `3br`). `startingRent` / `rentDisplay` drive the card. `sqft` and `count` are currently `null` because the source catalogue doesn't publish per-unit specifics; fill them in once that data exists and the card will show it automatically.
- `property.availabilityDate` — the headline release date shown across the site.
- `excluded[]` — properties/releases intentionally left out (Lot A, 123 Orange Street — both May 1, 2027). Move an entry here into `unitTypes`/a new property block once it's in scope.
- `workforceHousing.note` — the paragraph rendered under the unit grid.

When a **new release** (e.g. Lot A, May 1, 2027) is ready to publish, duplicate the `property`/`unitTypes` shape for it and extend `js/main.js`'s `renderUnits()`/hotspot logic to switch between releases — the current version assumes a single active release, matching what's in scope today.

## Open `[TBD]` items

Marked in-repo so they're easy to grep (`grep -rn "\[TBD\]"`):

1. **Inquiry form endpoint** (`index.html` `<form action="https://formspree.io/f/[TBD]">`) — create a Formspree form (or a Vercel serverless function) and drop the real endpoint in. Until then, `js/main.js` falls back to opening a pre-filled `mailto:` to `ryan@mcneil-development.com` so inquiries aren't lost.
2. **Leasing inbox** — the brief's catalogue footer lists `ryan@mcneil-development.com`; the docx's "Open Questions" section separately lists `sxc@mcneil-development.com`. The site currently uses `ryan@mcneil-development.com` everywhere. Confirm which is canonical and update `index.html` (3 places) + `js/main.js` (mailto fallback) if it should be the other address.
3. **Unit square footage, floor plans, and per-unit counts** (`data/units.json` → `sqft`, `count`, `features`, `floorPlanImage`) — the catalogue only publishes starting rent by unit type, not individual unit specs. Fill in once available.
4. **`numberOfAccommodationUnits`** in the JSON-LD block (`index.html` `<head>`).
5. **Logo / wordmark** — no standalone Toombs Court logo file was supplied; the hero/nav use a text wordmark ("Toombs *Court*") in Fraunces. Swap in a mark if/when one exists.
6. **Custom domain** — none requested; site ships on the default Vercel subdomain.

## Branding

- Primary palette is drawn from the Toombs Court photography (cedar-shingle tan, white trim, slate, soft coastal sky blue) — see `:root` in `css/styles.css`.
- McNeil Development's navy/red brand (`--mcneil-navy`, `--mcneil-red`) is used only in credit contexts: the About the Developer section and the footer, per the brief ("subtle... McNeil shows up as a 'Developed by' credit").
- Fonts: **Fraunces** (display/serif) + **Jost** (body/sans), matching the type pairing used on McNeil's existing site (`Website Development Project RJM`) for brand consistency, loaded from Google Fonts.

## Images

All images in `images/` are pre-optimized WebP, converted from the source files in `Toombs-court/` on the Desktop (`cwebp`, quality 78–90, resized for web). The architectural site plan was rendered from the source PDF at 250dpi and compressed the same way. No raw/full-resolution originals are committed (see `.gitignore`).

## Local preview

No build step required — just serve the directory statically, e.g.:

```bash
npx serve .
# or
python3 -m http.server 8000
```

## Deploy

Pushing to `main` on `Spencercassell/Toombs-Court` triggers a Vercel deployment once the repo is linked to a Vercel project (Vercel dashboard → Add New → Project → import this repo; framework preset "Other", no build command, output directory `.`).
