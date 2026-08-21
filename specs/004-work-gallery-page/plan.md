# Implementation Plan: Work Gallery Page

**Branch**: `004-work-gallery-page` | **Date**: 2026-08-20 | **Spec**: [spec.md](./spec.md)

**Input**: Feature specification from `/specs/004-work-gallery-page/spec.md`

**Note**: This template is filled in by the `/speckit-plan` command; its definition describes the execution workflow.

## Summary

Add a `work.html` gallery page reusing the existing site header/footer that
displays a 10-project thumbnail grid matching
`assets/page_mockups/ShelleyCerny_WebsiteWork.jpg`, plus one static detail
page per project (under `work/`) showing that project's supporting images
from its existing `assets/images/<project>/` folder. Everything is
hand-authored static HTML/CSS reusing `assets/css/styles.css`'s existing
design tokens and layout patterns (no JavaScript, no build step), so a new
project can be added later as one new HTML file + one new grid entry
without touching shared layout/CSS, per constitution Principle V.

## Technical Context

**Language/Version**: HTML5, CSS3 (no JavaScript required by this feature)

**Primary Dependencies**: None (no framework/build tool); Google Fonts
"Barlow Condensed" already linked from `index.html`, reused as-is

**Storage**: N/A — content is static image files under `assets/images/`, no
database or CMS

**Testing**: Manual QA against `quickstart.md` (visual comparison to the
mockup, click-through of all links, breakpoint checks, browser dev tools
console check) — no automated test framework, consistent with the
constitution's static-only, no-build-step principle

**Target Platform**: Static web, deployed as-is to GitHub Pages; modern
evergreen browsers (Chrome, Firefox, Safari, Edge)

**Project Type**: Static multi-page website (single existing project, no
frontend/backend split)

**Performance Goals**: Fast initial load on standard broadband — no
render-blocking scripts, reasonably sized images (matching the already-
optimized landing page)

**Constraints**: No animations/motion (constitution Principle III, with the
existing Bouncy GIF exception), no server-side or client-side JavaScript
dependency for core navigation (constitution Principle IV), must remain
usable with JavaScript disabled

**Scale/Scope**: 1 gallery page + 10 project detail pages; ~10-45 images
total across existing `assets/images/<project>/` folders

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Principle | Check | Status |
|---|---|---|
| I. Static-Only, No Backend | Plain HTML/CSS files, no server/build step; output is directly served by GitHub Pages | PASS |
| II. Design Fidelity | Grid layout, palette, and typography match `ShelleyCerny_WebsiteWork.jpg`, reusing landing page's established tokens (`--color-*`, `--font-display`/`--font-body`) rather than introducing new ones | PASS |
| III. No Site-Implemented Motion (NON-NEGOTIABLE) | No hover/scroll animations on the grid; `Bouncy_Logo_Bounce.gif` used only as portfolio content on the Bouncy detail page, never as UI/chrome, per the existing constitutional exception (spec FR-010) | PASS |
| IV. CSS-First Interactivity, Minimal JS | All thumbnail links and back-links are plain `<a>` tags; no JS is introduced by this feature | PASS |
| V. Content Updatable Without Touching Layout | Each project is one self-contained detail page + its existing `assets/images/<project>/` folder; adding a project means one new HTML file + one new grid `<a>` entry, no CSS/layout file edits required | PASS |
| VI. Accessibility & Performance Baseline | All images get descriptive `alt` text; semantic sectioning (`<main>`, headings) reused from landing page pattern; existing image assets are already web-sized | PASS |

No violations — Complexity Tracking is not needed for this feature.

**Post-Phase 1 re-check**: Design artifacts (`research.md`, `data-model.md`,
`contracts/page-contract.md`, `quickstart.md`) introduce no new
dependencies, backend calls, motion, or JavaScript beyond what's assessed
above — all six principles remain PASS after design.

## Project Structure

### Documentation (this feature)

```text
specs/004-work-gallery-page/
├── plan.md              # This file (/speckit-plan command output)
├── research.md          # Phase 0 output (/speckit-plan command)
├── data-model.md        # Phase 1 output (/speckit-plan command)
├── quickstart.md        # Phase 1 output (/speckit-plan command)
├── contracts/           # Phase 1 output (/speckit-plan command)
└── tasks.md             # Phase 2 output (/speckit-tasks command - NOT created by /speckit-plan)
```

### Source Code (repository root)

```text
index.html                          # existing landing page (unchanged)
work.html                           # NEW: Work gallery — 10-project thumbnail grid

work/                                # NEW: one static detail page per project
├── the-yoga-space.html
├── red-cedar-coffee.html
├── bouncy.html
├── go-pint.html
├── boyd-consulting.html
├── invitations.html
├── fit4mom.html
├── book.html
├── wedding-signage.html
└── murals.html

assets/
├── css/
│   └── styles.css                  # EXTENDED: adds .work-grid / .work-tile /
│                                    #   .project-detail rules; existing rules
│                                    #   (tokens, header, footer) reused as-is
├── page_mockups/
│   └── ShelleyCerny_WebsiteWork.jpg  # existing reference mockup
└── images/
    ├── yoga_space/  red_cedar/  bouncy/  go_pints/  boyd/
    ├── invitations/  flower_baby/  fit_for_mom/  book/
    └── wedding_sign/  murals/       # existing per-project image folders,
                                     # each already containing a
                                     # *_MockUp_Thumbnail.* file (source for
                                     # the work.html grid) and supporting
                                     # images (source for that project's
                                     # detail page)
```

**Structure Decision**: Single static site (matches the existing landing
page project — no separate frontend/backend). This feature adds one new
root-level page (`work.html`) and one new `work/` subfolder holding ten
project detail pages, all built from the image assets already committed
under `assets/images/<project>/`. `assets/css/styles.css` is extended
in-place (new grid/detail-page rules alongside the existing header/hero/
footer rules) rather than adding a second stylesheet, so all pages keep
sharing one source of truth for the site's design tokens.

## Complexity Tracking

> No Constitution Check violations — this section is not applicable.
