# Quickstart: Validating the Services Page

No build step, server, or dependencies are required — this is a static
HTML/CSS site. Use this guide to manually verify the feature end-to-end
against the spec's acceptance scenarios and success criteria.

## Prerequisites

- The repository checked out locally on branch `006-services-page`.
- A modern browser (Chrome, Firefox, Safari, or Edge).

## Setup

Serve the repo root as static files (any static server works; opening
`services.html` directly via `file://` also works since there is no
server-side logic). For example, from the repo root:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000/services.html`.

## Validation Scenarios

### 1. Reach the Services page from every existing page (User Story 2, SC-004)

1. Load `index.html`, `work.html`, `contact.html`, and at least 2 project
   detail pages (e.g. `work/the-yoga-space.html`, `work/bouncy.html`).
2. On each, click "Services" in the header nav.
3. **Expected**: every one lands on `services.html`, with zero broken links.

### 2. Compare the page to the mockup (User Story 1, SC-003)

1. Open `assets/page_mockups/ShelleyCerny_Website_Services.png`
   side-by-side with `services.html`.
2. **Expected**: same blob pattern background sized/positioned like the
   Contact page's checkerboard pattern, same off-white card with rounded
   corners and a strong drop shadow, same "Services" heading style as the
   landing page's "Hi I'm Shelley," heading, same 3-column-by-2-row icon
   grid, and the same overall palette/typography as the rest of the site.

### 3. Verify all six services render completely (User Story 1, SC-001)

1. On `services.html`, visually confirm all six grid items are present, in
   order: UX/UI Design, Brand Identity, Print Design, Social Media Design,
   Web Design, Illustration & Hand Lettering.
2. For each, confirm the icon, subtitle, and description are all visible
   and match the content in `data-model.md`.
3. **Expected**: no missing icons, no truncated or cut-off text.

### 4. Responsive breakpoints (SC-002)

Using dev tools' responsive/device mode, check `services.html` at:

- ~375px (mobile)
- ~768px (tablet)
- ~1440px (desktop)

**Expected** at every width: no overlapping or cut-off content (card,
heading, and all six grid items remain fully visible and readable), the
grid reflows to fewer columns as needed on narrower widths, and the
header/footer behave the same way they already do on `index.html` at the
same widths.

### 5. Console error check

1. Open browser dev tools → Console.
2. Load `services.html` and repeat scenario 1 (nav-in from each page).
3. **Expected**: no console errors or warnings during navigation or image
   loads.

### 6. Accessibility spot-check

1. Inspect each of the six `<img>` service icons.
2. **Expected**: non-empty, descriptive `alt` text identifying the service
   each icon represents — no empty `alt=""` or generic `alt="image"`
   placeholder.

## Done

All 6 scenarios passing constitutes the feature working end-to-end per the
spec's Success Criteria (SC-001–SC-004).
