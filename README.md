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

## Inquiry form delivery

The leasing form (`#inquiryForm` in `index.html`) posts to [FormSubmit.co](https://formsubmit.co) — a signup-free static-form backend, chosen because no Formspree/SMTP account or API key was available to configure:

- Action: `https://formsubmit.co/ryan@mcneil-development.com` (native fallback if JS is off)
- `js/main.js` submits via `https://formsubmit.co/ajax/ryan@mcneil-development.com` (fetch/AJAX) so the page shows an inline success message instead of navigating away
- Hidden `_cc` field also sends every inquiry to `sxc@mcneil-development.com`
- Hidden `_subject` / `_template=table` give the email a clear subject line and a readable table layout
- `_captcha=false` keeps submission frictionless; re-enable (remove that field) if spam becomes a problem
- A hidden `_honey` field is a basic spam honeypot

**One-time setup required:** FormSubmit activates a destination address on its *first* submission — that submission triggers a confirmation email to `ryan@mcneil-development.com` with an activation link. Until that link is clicked, inquiries won't be delivered. Submit the form once after launch and have Ryan click the confirmation email. If the fetch ever fails (network issue, address not yet activated), `main.js` falls back to opening a `mailto:` pre-filled to both `ryan@mcneil-development.com` and `sxc@mcneil-development.com` so the inquiry isn't lost.

## Open `[TBD]` items

Marked in-repo so they're easy to grep (`grep -rn "\[TBD\]"`):

1. **Unit square footage, floor plans, and per-unit counts** (`data/units.json` → `sqft`, `count`, `features`, `floorPlanImage`) — the catalogue only publishes starting rent by unit type, not individual unit specs. Fill in once available. (The 2BR floor plan shown under Availability and in the Gallery is illustrative, not tied to a specific numbered unit.)
2. **`numberOfAccommodationUnits`** in the JSON-LD block (`index.html` `<head>`).
3. **Logo / wordmark** — no standalone Toombs Court logo file was supplied; the hero/nav use a text wordmark ("Toombs *Court*") in Fraunces. Swap in a mark if/when one exists.
4. **Custom domain** — none requested; site ships on the default Vercel subdomain.
5. **Form captcha** — currently disabled (`_captcha=false`) for a frictionless submit. Revisit if the inbox starts getting spam.

## Branding

- Primary palette is drawn from the Toombs Court photography (cedar-shingle tan, white trim, slate, soft coastal sky blue) — see `:root` in `css/styles.css`.
- McNeil Development's navy/red brand (`--mcneil-navy`, `--mcneil-red`) is used only in credit contexts: the About the Developer section and the footer, per the brief ("subtle... McNeil shows up as a 'Developed by' credit").
- Fonts: **Fraunces** (display/serif) + **Jost** (body/sans), matching the type pairing used on McNeil's existing site (`Website Development Project RJM`) for brand consistency, loaded from Google Fonts.

## Images

All images in `images/` are pre-optimized WebP, converted from source photography (`cwebp`, quality 78–90, resized for web):

- Exterior, map, and amenity photos from `Toombs-court/` on the Desktop (the public marketing source folder named in `BRIEF.md`).
- The architectural site plan, rendered from the source PDF at 250dpi and compressed the same way.
- Nobadeer Beach and Surfside Beach gallery photos, and the three 2BR interior photos (kitchen, living room, double-vanity bath) plus the 2BR floor plan shown under Availability — these came from a separate "Source interior" folder, not the financial/deal-file material elsewhere on the McNeil Development drive, which was deliberately left out of this site.

No raw/full-resolution originals are committed (see `.gitignore`).

## Local preview

No build step required — just serve the directory statically, e.g.:

```bash
npx serve .
# or
python3 -m http.server 8000
```

## Deploy

Live at **https://toombs-court.vercel.app**. The Vercel project (`cre18/toombs-court`) is already linked to `Spencercassell/Toombs-Court` — every push to `main` redeploys automatically.
