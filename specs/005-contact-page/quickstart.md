# Quickstart: Validating the Contact Page

No build step, server, or dependencies are required — this is a static
HTML/CSS site. Use this guide to manually verify the feature end-to-end
against the spec's acceptance scenarios and success criteria.

## Prerequisites

- The repository checked out locally on branch `005-contact-page`.
- A modern browser (Chrome, Firefox, Safari, or Edge).

## Setup

Serve the repo root as static files (any static server works; opening
`contact.html` directly via `file://` also works since there is no
server-side logic). For example, from the repo root:

```bash
python3 -m http.server 8000
```

Then open `http://localhost:8000/contact.html`.

## Validation Scenarios

### 1. Reach the Contact page from every existing page (User Story 2, SC-005)

1. Load `index.html`, `work.html`, and at least 2 project detail pages
   (e.g. `work/the-yoga-space.html`, `work/bouncy.html`).
2. On each, click "Contact" in the header nav.
3. **Expected**: every one lands on `contact.html`, with zero broken links.

### 2. Compare the page to the mockup (User Story 1, SC-004)

1. Open `assets/page_mockups/ShelleyCerny_Website_Contact.png` side-by-side
   with `contact.html`.
2. **Expected**: same checkerboard background pattern tiled across the
   full-bleed teal area, same off-white card with drop shadow, same photo
   overlapping the card's right edge with its own drop shadow, same "Say
   Hello!" heading style, same body copy position/padding, same button
   style and position, and the same overall palette/typography as the rest
   of the site.

### 3. Send an email via the CTA button (User Story 1, SC-001, SC-002)

1. Open browser dev tools → Console.
2. Click "Send Me An Email".
3. **Expected**: the OS/browser's default mail client opens (or a
   "choose an app" prompt appears, per standard `mailto:` behavior) with a
   new message pre-addressed to `shelley.cerny@gmail.com`; no console
   errors appear.

### 4. Responsive breakpoints (SC-003)

Using dev tools' responsive/device mode, check `contact.html` at:

- ~375px (mobile)
- ~768px (tablet)
- ~1440px (desktop)

**Expected** at every width: no overlapping or cut-off content (card, photo,
heading, body copy, button all remain fully visible and readable), and the
header/footer behave the same way they already do on `index.html` at the
same widths.

### 5. Keyboard-only navigation (edge case coverage)

1. From `contact.html`, press Tab repeatedly.
2. **Expected**: focus visibly reaches the "Send Me An Email" button (after
   the header nav links), and it activates with Enter, opening the mail
   client the same way a click does.

### 6. Console error check (SC-002)

1. Open browser dev tools → Console.
2. Repeat scenario 1 (nav-in) and scenario 3 (CTA click).
3. **Expected**: no console errors or warnings during navigation, image
   loads, or the CTA click.

### 7. Accessibility spot-check

1. Inspect the `<img>` for Shelley's photo.
2. **Expected**: non-empty, descriptive `alt` text identifying Shelley — no
   empty `alt=""` or generic `alt="image"` placeholder.

## Done

All 7 scenarios passing constitutes the feature working end-to-end per the
spec's Success Criteria (SC-001–SC-005).
