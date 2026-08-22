# Implementation Plan: Contact Page

**Branch**: `005-contact-page` | **Date**: 2026-08-22 | **Spec**: [spec.md](./spec.md)

**Input**: Feature specification from `/specs/005-contact-page/spec.md`

**Note**: This template is filled in by the `/speckit-plan` command; its definition describes the execution workflow.

## Summary

Add a `contact.html` page reusing the existing site header/footer that
presents a "Say Hello!" greeting, invitation copy, and a single
`mailto:shelley.cerny@gmail.com` call-to-action button, laid out as an
off-white card (with Shelley's photo overlapping its right edge) sitting on
a full-bleed tiled checkerboard-pattern background, matching
`assets/page_mockups/ShelleyCerny_Website_Contact.png`. The existing
placeholder "Contact" nav link (`href="#"`) is wired to this new page across
all 12 existing pages (`index.html`, `work.html`, and the 10 `work/*.html`
detail pages). Everything is hand-authored static HTML/CSS reusing
`assets/css/styles.css`'s existing design tokens (no JavaScript, no build
step, no form), consistent with the constitution's static-only,
`mailto:`-only contact principle.

## Technical Context

**Language/Version**: HTML5, CSS3 (no JavaScript required by this feature)

**Primary Dependencies**: None (no framework/build tool); Google Fonts
"Barlow Condensed" already linked from `index.html`, reused as-is

**Storage**: N/A — no form, no submitted data, no database or CMS

**Testing**: Manual QA against `quickstart.md` (visual comparison to the
mockup, click-through of the mailto button, nav-link check from every
existing page, breakpoint checks, browser dev tools console check) — no
automated test framework, consistent with the constitution's static-only,
no-build-step principle

**Target Platform**: Static web, deployed as-is to GitHub Pages; modern
evergreen browsers (Chrome, Firefox, Safari, Edge)

**Project Type**: Static multi-page website (single existing project, no
frontend/backend split)

**Performance Goals**: Fast initial load on standard broadband — no
render-blocking scripts, reasonably sized images (matching the
already-optimized landing page and Work gallery)

**Constraints**: No animations/motion (constitution Principle III), no
server-side or client-side JavaScript dependency (the CTA is a plain
`mailto:` `<a>` tag), must remain usable with JavaScript disabled

**Scale/Scope**: 1 new page (`contact.html`); 12 existing pages get their
"Contact" nav link updated from a `#` placeholder to `contact.html`

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Principle | Check | Status |
|---|---|---|
| I. Static-Only, No Backend | Plain HTML/CSS file, no server/build step; the single interactive element is a `mailto:` link, not a form | PASS |
| II. Design Fidelity | Card layout, checkerboard background, photo overlap, palette, and typography match `ShelleyCerny_Website_Contact.png`, reusing the landing page's established tokens and hero-card overlap technique rather than inventing new patterns | PASS |
| III. No Site-Implemented Motion (NON-NEGOTIABLE) | Drop shadows are static `box-shadow` values (no transition/animation); button `:hover`/`:focus-visible` reuses the existing instant-change `.button--resume` treatment | PASS |
| IV. CSS-First Interactivity, Minimal JS | The "Send Me An Email" CTA is a plain `<a href="mailto:...">` styled as a button; no JS is introduced by this feature | PASS |
| V. Content Updatable Without Touching Layout | The page's heading/body copy/email address live in one self-contained HTML file; updating the message or address later requires no CSS/layout changes | PASS |
| VI. Accessibility & Performance Baseline | Photo gets descriptive `alt` text; semantic `<main>`/heading structure reused from established landing-page pattern; existing image assets are already web-sized | PASS |

No violations — Complexity Tracking is not needed for this feature.

**Post-Phase 1 re-check**: Design artifacts (`research.md`, `data-model.md`,
`contracts/page-contract.md`, `quickstart.md`) introduce no new dependencies,
backend calls, motion, or JavaScript beyond what's assessed above — all six
principles remain PASS after design.

## Project Structure

### Documentation (this feature)

```text
specs/005-contact-page/
├── plan.md              # This file (/speckit-plan command output)
├── research.md          # Phase 0 output (/speckit-plan command)
├── data-model.md        # Phase 1 output (/speckit-plan command)
├── quickstart.md        # Phase 1 output (/speckit-plan command)
├── contracts/           # Phase 1 output (/speckit-plan command)
└── tasks.md             # Phase 2 output (/speckit-tasks command - NOT created by /speckit-plan)
```

### Source Code (repository root)

```text
index.html                          # EXISTING: "Contact" nav link updated to point to contact.html
work.html                           # EXISTING: "Contact" nav link updated to point to contact.html
work/                                # EXISTING: all 10 detail pages get "Contact" nav link updated
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

contact.html                        # NEW: Contact page ("Say Hello!" card + mailto CTA)

assets/
├── css/
│   └── styles.css                  # EXTENDED: adds .contact-main / .contact-card /
│                                    #   .contact-photo rules; existing rules
│                                    #   (tokens, header, footer, .button) reused as-is
├── page_mockups/
│   └── ShelleyCerny_Website_Contact.png  # existing reference mockup
└── images/
    ├── Shelleycerny-checkared.png  # existing tiled background pattern asset
    └── ShelleyCerny_Photo02.png    # existing photo of Shelley used in the card
```

**Structure Decision**: Single static site (matches the existing landing
page and Work gallery). This feature adds one new root-level page
(`contact.html`) built from image assets already committed under
`assets/images/`, and updates the "Contact" nav link across all 12 existing
pages. `assets/css/styles.css` is extended in-place (new contact-page rules
alongside the existing header/hero/footer/work rules) rather than adding a
second stylesheet, so all pages keep sharing one source of truth for the
site's design tokens.

## Complexity Tracking

> No Constitution Check violations — this section is not applicable.
