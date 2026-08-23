# Implementation Plan: Services Page

**Branch**: `006-services-page` | **Date**: 2026-08-22 | **Spec**: [spec.md](./spec.md)

**Input**: Feature specification from `/specs/006-services-page/spec.md`

**Note**: This template is filled in by the `/speckit-plan` command; its definition describes the execution workflow.

## Summary

Add a `services.html` page reusing the existing site header/footer that
presents a "Services" heading over a 3-column-by-2-row grid of six service
offerings (icon, subtitle, centered description each: UX/UI Design, Brand
Identity, Print Design, Social Media Design, Web Design, Illustration & Hand
Lettering), laid out as an off-white, rounded-corner card with a strong drop
shadow sitting on a full-bleed tiled `Shelleycerny-blobs` pattern background,
matching `assets/page_mockups/ShelleyCerny_Website_Services.png`. The
approach mirrors the Contact page's `.contact-pattern`/`.contact-card`
pattern almost exactly (same box footprint, corner radius, and background
sizing technique, swapping `Shelleycerny-checkared.png` for
`Shelleycerny-blobs.png`), and reuses the existing `.hero-card h1` heading
style and `.project-subtitle`/`.project-body` text styles rather than
inventing new typography. The existing placeholder "Services" nav link
(`href="#"`) is wired to this new page across all 13 existing pages
(`index.html`, `work.html`, `contact.html`, and the 10 `work/*.html` detail
pages). Everything is hand-authored static HTML/CSS reusing
`assets/css/styles.css`'s existing design tokens (no JavaScript, no build
step, no per-item links), consistent with the constitution's static-only
principle.

## Technical Context

**Language/Version**: HTML5, CSS3 (no JavaScript required by this feature)

**Primary Dependencies**: None (no framework/build tool); Google Fonts
"Barlow Condensed" already linked from `index.html`, reused as-is

**Storage**: N/A — no form, no submitted data, no database or CMS

**Testing**: Manual QA against `quickstart.md` (visual comparison to the
mockup, nav-link check from every existing page, breakpoint checks, browser
dev tools console check) — no automated test framework, consistent with the
constitution's static-only, no-build-step principle

**Target Platform**: Static web, deployed as-is to GitHub Pages; modern
evergreen browsers (Chrome, Firefox, Safari, Edge)

**Project Type**: Static multi-page website (single existing project, no
frontend/backend split)

**Performance Goals**: Fast initial load on standard broadband — no
render-blocking scripts, reasonably sized images (matching the
already-optimized landing page, Work gallery, and Contact page)

**Constraints**: No animations/motion (constitution Principle III), no
server-side or client-side JavaScript dependency (grid items are static
content, not interactive controls), must remain usable with JavaScript
disabled

**Scale/Scope**: 1 new page (`services.html`) with 6 fixed grid items; 13
existing pages get their "Services" nav link updated from a `#` placeholder
to `services.html`

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Principle | Check | Status |
|---|---|---|
| I. Static-Only, No Backend | Plain HTML/CSS file, no server/build step, no form, no interactive JS | PASS |
| II. Design Fidelity | Card layout, blob background, 3x2 icon grid, palette, and typography match `ShelleyCerny_Website_Services.png`, reusing the Contact page's established pattern/card technique and the landing/Work pages' heading/subtitle/body tokens rather than inventing new patterns | PASS |
| III. No Site-Implemented Motion (NON-NEGOTIABLE) | Drop shadow is a static `box-shadow` value (no transition/animation); grid items have no hover/focus interactive states since they are non-interactive content, not controls | PASS |
| IV. CSS-First Interactivity, Minimal JS | No interactive elements beyond standard `<a>` nav links reused from the shared header; no JS introduced by this feature | PASS |
| V. Content Updatable Without Touching Layout | The six services' icon/subtitle/description live as repeated markup in one self-contained HTML file; adding/editing a service later requires no CSS/layout changes | PASS |
| VI. Accessibility & Performance Baseline | Each icon gets descriptive `alt` text; semantic `<main>`/heading structure reused from established landing/Contact-page pattern; existing icon image assets are already web-sized | PASS |

No violations — Complexity Tracking is not needed for this feature.

**Post-Phase 1 re-check**: Design artifacts (`research.md`, `data-model.md`,
`contracts/page-contract.md`, `quickstart.md`) introduce no new dependencies,
backend calls, motion, or JavaScript beyond what's assessed above — all six
principles remain PASS after design.

## Project Structure

### Documentation (this feature)

```text
specs/006-services-page/
├── plan.md              # This file (/speckit-plan command output)
├── research.md          # Phase 0 output (/speckit-plan command)
├── data-model.md        # Phase 1 output (/speckit-plan command)
├── quickstart.md        # Phase 1 output (/speckit-plan command)
├── contracts/           # Phase 1 output (/speckit-plan command)
└── tasks.md             # Phase 2 output (/speckit-tasks command - NOT created by /speckit-plan)
```

### Source Code (repository root)

```text
index.html                          # EXISTING: "Services" nav link updated to point to services.html
work.html                           # EXISTING: "Services" nav link updated to point to services.html
contact.html                        # EXISTING: "Services" nav link updated to point to services.html
work/                                # EXISTING: all 10 detail pages get "Services" nav link updated
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

services.html                       # NEW: Services page ("Services" card + 6-item grid)

assets/
├── css/
│   └── styles.css                  # EXTENDED: adds .services-pattern / .services-card /
│                                    #   .services-grid / .service-item rules; existing rules
│                                    #   (tokens, header, footer, .hero-card h1,
│                                    #   .project-subtitle, .project-body) reused as-is
├── page_mockups/
│   └── ShelleyCerny_Website_Services.png  # existing reference mockup
└── images/
    ├── Shelleycerny-blobs.png      # existing tiled background pattern asset
    ├── ShelleyCerny_UXIcon.png     # existing service icon assets
    ├── ShelleyCerny_BrandIcon.png
    ├── ShelleyCerny_PrintIcon.png
    ├── ShelleyCerny_SocialIcon.png
    ├── ShelleyCerny_WebIcon.png
    └── ShelleyCerny_LetteringIcon.png
```

**Structure Decision**: Single static site (matches the existing landing
page, Work gallery, and Contact page). This feature adds one new root-level
page (`services.html`) built from image assets already committed under
`assets/images/`, and updates the "Services" nav link across all 13 existing
pages. `assets/css/styles.css` is extended in-place (new services-page rules
alongside the existing header/hero/footer/work/contact rules) rather than
adding a second stylesheet, so all pages keep sharing one source of truth
for the site's design tokens.

## Complexity Tracking

> No Constitution Check violations — this section is not applicable.
