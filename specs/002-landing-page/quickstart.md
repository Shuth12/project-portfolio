# Quickstart: Landing Page (Home / About)

Validates the feature end-to-end against the spec's acceptance scenarios
and success criteria. No build tooling is required.

## Prerequisites

- Local: any static file server, or just opening the HTML file directly in
  a browser. No dependencies to install.
- Have `assets/page_mockups/ShelleyCerny_WebsiteAbout.jpg` open side-by-side
  for visual comparison.

## 1. Verify the page loads with real content

```bash
open index.html
# or: python3 -m http.server 8000   (then visit http://localhost:8000)
```

**Expected**: the header shows the logo placeholder and nav (About, Work,
Contact, Services); the hero section shows the headshot placeholder, the
heading "Hi I'm Shelley,", the full bio paragraph, and the "Download My
Resume" button; the footer shows "Designed by: Shelley Cerny". No console
errors. Validates User Story 1 / FR-001–FR-005.

## 2. Compare visually against the mockup

Place the browser window and `ShelleyCerny_WebsiteAbout.jpg` side by side.

**Expected**: layout, color palette, and typography closely match —
cream background, teal hero panel, mustard-yellow accent shapes, green
headings/nav/logo text, purple CTA button. Confirm the two known,
spec-approved contrast exceptions (footer white-on-mustard, nav
green-on-cream — see `research.md`) are present as designed, not
accidental. Validates FR-006 / SC-004.

## 3. Verify links and placeholders behave as specified

- Click **About** → page scrolls/jumps to the bio section (same page).
- Click **Work** → navigates to `work.html` (expected 404 — not yet built).
- Click **Services** → navigates to its placeholder destination (expected
  404 or no-op — not yet built).
- Click **Download My Resume** → attempts to open
  `assets/resume/ShelleyCerny-Resume.pdf` (expected 404 — file not yet
  supplied).

**Expected**: no JavaScript console errors from any of these clicks, even
though several are expected 404s. Validates User Story 2 / User Story 3 /
FR-009–FR-013 / SC-002.

## 4. Verify responsive behavior

Resize the browser (or use dev tools device emulation) to ~375px, ~768px,
and ~1440px widths.

**Expected**: no overlapping or cut-off content at any width; the nav wraps
or stacks cleanly at narrow widths with no JavaScript-driven menu; the hero
photo/bio panel reflows without breaking. Validates SC-003 / edge cases
(narrow/wide viewports).

## 5. Verify accessibility baseline

- View page source / inspect each `<img>` and confirm meaningful `alt`
  text (logo, headshot, any decorative shapes marked `alt=""` if purely
  decorative).
- Confirm heading structure is logical (single `<h1>` for "Hi I'm
  Shelley,", no skipped levels).

**Expected**: all images have appropriate `alt` text; no other console
errors. Validates FR-008.

## 6. Verify no JavaScript is required

Disable JavaScript in the browser (or use a text-only browser/curl) and
reload the page.

**Expected**: all content and nav links still render and are clickable —
nothing on the page depends on JavaScript to function. Validates edge case
"JavaScript disabled" / constitution Principle IV.
