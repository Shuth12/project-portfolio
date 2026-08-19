# Implementation Plan: Landing Page (Home / About)

**Branch**: `002-landing-page` | **Date**: 2026-08-18 | **Spec**: [spec.md](./spec.md)

**Input**: Feature specification from `/specs/002-landing-page/spec.md`

**Note**: This template is filled in by the `/speckit-plan` command; its definition describes the execution workflow.

## Summary

Replace the placeholder `index.html` shipped in `001-scaffold-site-deploy`
with the real landing page, which doubles as the site's "About" content per
the PRD. The page is a single static HTML file (header/nav, hero bio
section, footer) styled via the existing `assets/css/styles.css`, matching
the `ShelleyCerny_WebsiteAbout.jpg` mockup's layout, color palette (sampled
directly from the mockup image), and typography (approximated with free
Google Fonts). The headshot photo, hand-lettered logo, and resume PDF are
not yet available, so the page references placeholder asset paths per the
spec's clarifications; "Work," "Services," and "Contact" nav links point to
pages built in future specs. No JavaScript is introduced — the four-item
nav is handled with pure CSS responsive layout.

## Technical Context

**Language/Version**: HTML5, CSS3 (no JavaScript — nav is plain `<a>` tags,
responsive behavior handled entirely with CSS flex-wrap)

**Primary Dependencies**: None for markup/logic. Two Google Fonts loaded via
a CDN `<link>` (no build step, no npm dependency) — see research.md for the
specific families chosen to approximate the mockup's bold block headings
and hand-lettered feel.

**Storage**: N/A (no data, no database)

**Testing**: Manual verification via `quickstart.md` (load the page
locally, compare against the mockup, check responsive breakpoints, verify
links/alt text). Consistent with `001-scaffold-site-deploy` — no automated
test framework is warranted for a single static content page.

**Target Platform**: GitHub Pages (static hosting), modern evergreen
browsers (Chrome, Firefox, Safari, Edge)

**Project Type**: Static website — extends the existing single-page
scaffold at the repository root; no frontend/backend split, no build step

**Performance Goals**: Page fully rendered without layout shift on a
standard broadband connection; resume download <2s once the real file is
supplied (spec SC-005)

**Constraints**: Fully static (constitution I); no build step; no
JavaScript (constitution IV — a pure-CSS nav is sufficient here); no
animation/motion (constitution III); design fidelity takes precedence over
accessibility contrast where the mockup's exact colors are borderline, per
the spec's resolved clarification (constitution II vs. VI tradeoff,
explicitly justified below)

**Scale/Scope**: One page (`index.html`), extending one stylesheet
(`assets/css/styles.css`) — no new pages, no content model beyond the
static bio text

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Principle | Status | Notes |
|---|---|---|
| I. Static-Only, No Backend | PASS | Plain HTML/CSS plus a Google Fonts CDN `<link>` (a static asset request, not a backend/build dependency). No server, database, or build step introduced. |
| II. Design Fidelity | PASS (documented exception, see below) | Layout, palette, and typography follow the mockup closely; exact colors were sampled from the mockup image's pixels rather than estimated. One explicit, spec-approved exception: where a mockup color pairing has low contrast, the mockup's exact color is kept as-is (see VI). |
| III. No Site-Implemented Motion or Animation | PASS | No transitions/animations; hover/focus states (if any) use plain CSS pseudo-classes with instant state changes. |
| IV. CSS-First Interactivity, Minimal JavaScript | PASS | Nav is four `<a>` tags; responsive stacking/wrapping is handled with CSS flexbox — no JavaScript is used at all. |
| V. Content Updatable Without Touching Layout | PASS | The bio is one-off prose text (not a repeating content list), so it lives inline in `index.html`; editing it is a text change, not a layout/CSS change. This principle's main target (repeatable project content) applies once the Work gallery feature is built. |
| VI. Accessibility and Performance Baseline | PASS (documented exception) | Semantic HTML, alt text on all images (FR-008), and layout stability at common breakpoints (SC-003) are all met. One exception: the footer's white text on the mustard-yellow band measures ~1.89:1 contrast (below WCAG AA's 4.5:1), and the nav's green-on-cream text measures ~3.64:1 (below AA for normal-size text). Per the spec's resolved clarification, design fidelity to the mockup takes precedence over adjusting these specific colors — see Complexity Tracking. |

**Post-design re-check** (after Phase 1): design artifacts (research.md,
data-model.md, contracts/, quickstart.md) introduce no new dependencies,
build steps, JavaScript, motion, or backend components beyond the Google
Fonts CDN link already captured above. All gate statuses are unchanged.

## Project Structure

### Documentation (this feature)

```text
specs/002-landing-page/
├── plan.md              # This file (/speckit-plan command output)
├── research.md          # Phase 0 output (/speckit-plan command)
├── data-model.md         # Phase 1 output (/speckit-plan command)
├── quickstart.md         # Phase 1 output (/speckit-plan command)
├── contracts/            # Phase 1 output (/speckit-plan command)
└── tasks.md              # Phase 2 output (/speckit-tasks command - NOT created by /speckit-plan)
```

### Source Code (repository root)

```text
index.html                     # Replaced: real landing page (header/nav, hero bio, footer)
assets/
├── css/
│   └── styles.css              # Extended: header/nav, hero/bio, button, footer, responsive rules
├── images/                     # Existing project mockup assets (unchanged by this feature)
│   ├── profile/                # NEW (referenced, not populated): headshot placeholder path
│   └── logo/                   # NEW (referenced, not populated): logo placeholder path
├── resume/                     # NEW (referenced, not populated): resume PDF placeholder path
└── page_mockups/                # Existing design reference mockups (unchanged)

.github/
└── workflows/
    └── deploy.yml               # Unchanged (from 001-scaffold-site-deploy)
```

**Structure Decision**: Continue the single static site at the repository
root established in `001-scaffold-site-deploy` — no `src/`, no
frontend/backend split, no build output directory. `index.html` is edited
in place (replacing the placeholder content) and `assets/css/styles.css` is
extended rather than split into multiple stylesheets, since this feature
adds exactly one page. The `assets/images/profile/`, `assets/images/logo/`,
and `assets/resume/` paths are referenced by `index.html`'s `<img>`/`<a>`
tags per the spec's placeholder-asset clarifications, but the actual files
are out of scope for this feature and are intentionally not created.

## Complexity Tracking

> **Fill ONLY if Constitution Check has violations that must be justified**

| Violation | Why Needed | Simpler Alternative Rejected Because |
|---|---|---|
| Principle VI (contrast): footer white-on-mustard (~1.89:1) and nav green-on-cream (~3.64:1) fall below WCAG AA | The spec's design-fidelity clarification (resolved 2026-08-18) explicitly requires matching the mockup's exact colors even where contrast is borderline, since the designer (Shelley) owns the visual language per Principle II | Substituting a higher-contrast shade of yellow/green was rejected by the spec owner — it would deviate from the approved mockup, which Principle II treats as authoritative over ad hoc accessibility tweaks unless the designer amends the design |
