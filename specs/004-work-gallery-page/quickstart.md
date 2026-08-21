# Quickstart: Validating the Work Gallery Page

No build step, server, or dependencies are required — this is a static
HTML/CSS site. Use this guide to manually verify the feature end-to-end
against the spec's acceptance scenarios and success criteria.

## Prerequisites

- The repository checked out locally on branch `004-work-gallery-page`.
- A modern browser (Chrome, Firefox, Safari, or Edge).

## Setup

Serve the repo root as static files (any static server works; opening
`index.html`/`work.html` directly via `file://` also works since there is
no server-side logic). For example, from the repo root:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000/index.html`.

## Validation Scenarios

### 1. Reach the Work page from the landing page (User Story 3, SC-002)

1. Load `index.html`.
2. Click "Work" in the header nav.
3. **Expected**: `work.html` loads, showing the same header/footer as the
   landing page and a 10-tile thumbnail grid.

### 2. Compare the grid to the mockup (User Story 1, SC-001, SC-005)

1. Open `assets/page_mockups/ShelleyCerny_WebsiteWork.jpg` side-by-side
   with `work.html`.
2. **Expected**: same 10 projects, same left-to-right/top-to-bottom order
   (see `data-model.md`'s Project Catalog), same overall palette (cream
   background, teal panel, mustard footer) and typography as the mockup
   and as the already-shipped landing page.
3. Confirm all 10 thumbnails are visible without any click/scroll beyond
   normal page scroll (SC-001).

### 3. Click through every thumbnail (User Story 2, SC-002, SC-003)

For each of the 10 tiles:

1. Click the tile.
2. **Expected**: navigates to that project's own `work/<slug>.html` page
   (see `contracts/page-contract.md` for the slug list), showing only that
   project's images, its title as an `<h1>`, and a "Back to Work" link.
3. Click "Back to Work".
4. **Expected**: returns to `work.html`.

Repeat for all 10 projects. Zero broken links, zero images from the wrong
project appearing on any detail page.

### 4. Console error check (SC-002)

1. Open browser dev tools → Console.
2. Repeat scenario 3 for at least 3 projects.
3. **Expected**: no console errors or warnings during navigation or image
   loads.

### 5. Responsive breakpoints (SC-004)

Using dev tools' responsive/device mode, check `work.html` and at least one
`work/<slug>.html` page at:

- ~375px (mobile)
- ~768px (tablet)
- ~1440px (desktop)

**Expected** at every width: no overlapping or cut-off thumbnails/images,
the grid reflows to fewer columns as the viewport narrows, and the header/
footer behave the same way they already do on `index.html` at the same
widths.

### 6. Keyboard-only navigation (edge case coverage)

1. From `work.html`, press Tab repeatedly.
2. **Expected**: focus visibly moves through every thumbnail link in grid
   order, then into the footer; each is activatable with Enter.
3. On a detail page, Tab to the "Back to Work" link and activate it with
   Enter.
4. **Expected**: returns to `work.html`.

### 7. Accessibility spot-check

1. Inspect a few `<img>` elements on `work.html` and on 2-3 detail pages.
2. **Expected**: every image has non-empty, descriptive `alt` text
   naming the project (and specific piece, where applicable) — no empty
   `alt=""` on content images, no generic `alt="image"` placeholders.

## Done

All 7 scenarios passing constitutes the feature working end-to-end per the
spec's Success Criteria (SC-001–SC-005).
