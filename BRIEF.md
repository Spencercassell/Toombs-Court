# Toombs Court — Leasing & Marketing Website Build Brief

Source: `Source toombs.docx` (Desktop/Toombs-court), transcribed to Markdown.

## 1. Project Overview

- **Developer:** McNeil Development
- **Property:** Toombs Court (new development), 1 Toombs Court, Nantucket, MA
- **Purpose:** A property-focused leasing and marketing website that showcases Toombs Court and drives leasing inquiries for units available January 1.
- **Design reference:** [101california.com](https://101california.com) — copy its single-property, premium feel: full-bleed hero photos, simple navigation, lots of whitespace, refined typography, and content built entirely around the building.

## 2. Deliverables

1. A responsive static website (HTML, CSS, vanilla JavaScript).
2. All code committed and pushed to the GitHub repository `Toombs-Court` (Spencercassell/Toombs-Court).
3. Deployed on Vercel through the linked project (a push to `main` should trigger deployment).
4. A `README.md` covering project structure, how to update unit availability, and any content still marked `[TBD]`.

## 3. Source Materials

All source files are in the `Toombs-court` folder on the Desktop.

- **`Images/` folder:** Neighborhood/amenity photography (Nantucket Meat & Fish Market, Nantucket Health Club, beach, bike path). Optimize every image before use (WebP, compressed, lazy-loaded).
- **`Exterior Buildings and Site Plan/` folder:** Exterior photos of Lot B and Lot C, plus the architectural site plan PDF.
- **`Catalogue.pdf`:** The only source for unit and offering data. **Use only Toombs Court units with January 1 availability** (1 Toombs Court – Lots B & C). Ignore Lot A (May 1) and 123 Orange Street (May 1).
- **`Market/` folder:** Fisher Real Estate's 2026 Nantucket guide — pull news, market statistics, neighborhood highlights. Attribute sources and do not invent content.
- **`Map/` folder:** The centerpiece of the Location section.
- **Site plan:** The base layer for the interactive availability feature.
- **`Website Development Project RJM`** (Desktop, separate existing repo): Source for *subtle* McNeil Development branding (logo, accent color, typography cues) only — not touched or copied wholesale. Toombs Court stays the primary brand; McNeil shows up as a "Developed by" credit, in the About section, and in the footer.

## 4. Site Structure

A single-page scrolling site with a sticky, anchored navigation bar:

1. **Hero** — full-bleed exterior photo, property name, short tagline, CTAs ("View Availability", "Schedule a Tour").
2. **Overview** — short property introduction and key highlights.
3. **Availability** — the core feature (see §5).
4. **Location** — the map as a highlight (see §6).
5. **Gallery** — exterior and supporting images with a lightbox viewer.
6. **Neighborhood & News** — curated items from the market guide.
7. **About the Developer** — brief McNeil Development profile.
8. **Leasing Inquiry / Contact** — inquiry form plus leasing contact details from the catalogue.
9. **Footer** — logos, contact info, legal/copyright line.

## 5. Availability Feature

- Extract the January 1 units from the catalogue into `data/units.json` as the single source of truth.
  - **Note:** the catalogue only publishes aggregate rent-by-unit-type for "1 Toombs Court – Lots B & C" (Studio / 1BR / 2BR / 3BR), not individual unit IDs, floors, square footage, or counts — leasing is confirmed by phone. Fields that aren't published are marked `[TBD]` rather than invented, per §9.
- **Site plan:** highlight Lot B and Lot C (the available buildings) on the rendered site-plan image; clicking/tapping a lot shows the unit-type/rent summary for that release.
- **Exterior photo callouts:** Lot B and Lot C exterior photos are paired with their availability info in the Availability section.
- **Unit-type list:** a card view of Studio/1BR/2BR/3BR with starting rent, kept in sync with the site plan.
- Every unit type gets an "Inquire" button that pre-fills the inquiry form.

## 6. Location & Map

- Feature the map prominently in a full-width section with a clear property marker.
- Static map image as the primary visual (`Bike Path and Map.png`).
- Short location selling points (access, transit, nearby amenities) taken from the source files only.

## 7. Design & Branding

- Premium and minimal: big imagery, restrained color palette, elegant serif/sans font pairing.
- Color palette based on the Toombs Court photography (warm cedar-shingle tan, white trim, slate, soft coastal sky blue), with McNeil Development's navy/red accents used sparingly (credit areas only).
- Mobile-first, fully responsive design.
- Subtle scroll-in animations that respect `prefers-reduced-motion`.
- Accessibility: WCAG 2.1 AA (alt text, color contrast, keyboard navigation, form labels).

## 8. Technical Requirements

- Static HTML/CSS/JS, no build step. Deploys on Vercel as-is.

```
toombs-court/
├── index.html
├── css/styles.css
├── js/main.js
├── data/units.json
├── images/ (optimized assets only)
└── README.md
```

- **Performance:** responsive `srcset`, WebP images, lazy loading, minimal dependencies.
- **SEO:** page title, meta description, Open Graph/social preview image, favicon, schema.org structured data for the property type.
- **Inquiry form:** Formspree-compatible static form (no backend in this repo).
- No raw full-resolution originals committed. `.gitignore` added.

## 9. Content Rules

- Use only facts from the source files. Never invent rates, square footage, dates, or statistics.
- If something is missing, insert `[TBD]` and list it in the README.
- Copy is concise, confident, and professional — premium leasing site tone.

## 10. Deployment Workflow

1. Build and preview locally.
2. Commit and push to `main` on `Spencercassell/Toombs-Court`.
3. Confirm the Vercel deployment succeeds and share the live URL.
4. Check the live site on desktop and mobile.

## 11. Acceptance Checklist

- [ ] Only Toombs Court January 1 units are shown
- [ ] Site plan highlights available lots and is interactive
- [ ] Exterior photos used in the hero and availability sections
- [ ] Map featured in the Location section
- [ ] Market news/highlights included and attributed
- [ ] Subtle McNeil Development branding applied
- [ ] Responsive, accessible, and performant
- [ ] Pushed to GitHub and live on Vercel

## 12. Contact / Open Items

- Residential leasing inquiries: **(617) 780-1627** / **ryan@mcneil-development.com** (per Catalogue.pdf footer). The docx also lists `sxc@mcneil-development.com` under "Open Questions" — both are surfaced; `[TBD]` which is the canonical leasing inbox.
- Domain: no custom domain requested — Vercel-assigned URL is fine.
