# Implementation Plan: Landing Page Design Polish

**Branch**: `003-landing-page-design-polish` | **Date**: 2026-08-19 | **Spec**: [spec.md](./spec.md)

**Input**: Feature specification from `/specs/003-landing-page-design-polish/spec.md`

**Note**: This template is filled in by the `/speckit-plan` command; its definition describes the execution workflow.

## Summary

Apply four designer-requested visual refinements to the existing static
landing page (`index.html` / `assets/css/styles.css`, delivered in
`002-landing-page`): reveal more of the patterned backdrop behind the hero
photo, increase padding/spacing and make the bio text card more square,
remove all em dash characters sitewide while opening up body letter
spacing, and increase nav link letter spacing (subtly). The approach is a
targeted CSS/markup adjustment pass with no new dependencies, files, or
structural changes — only edits to the two existing site files plus a
visual QA/designer sign-off step.

## Technical Context

**Language/Version**: HTML5, CSS3 (no preprocessor, no build step)

**Primary Dependencies**: None added; existing Google Fonts `Barlow
Condensed` webfont link in `index.html` is unchanged

**Storage**: N/A (static site, no data layer)

**Testing**: Manual visual QA in-browser across breakpoints + designer
review sign-off (no automated test framework exists in this repo, matching
`002-landing-page`'s validated approach)

**Target Platform**: Static site served via GitHub Pages; modern desktop
and mobile browsers

**Project Type**: Static website (single project, no frontend/backend split)

**Performance Goals**: No regression to current page weight/load time — this
feature changes only CSS values and a handful of text characters, no new
assets or requests

**Constraints**: No animation/motion (Constitution III); no JavaScript
required (Constitution IV); no backend (Constitution I); must not require
touching layout/CSS to update unrelated content (Constitution V)

**Scale/Scope**: One page (`index.html`) and one stylesheet
(`assets/css/styles.css`); ~4 scoped visual/typographic adjustments, no new
sections or content

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Principle | Gate | Status |
|---|---|---|
| I. Static-Only, No Backend | No server/backend/database introduced | **PASS** — edits are HTML/CSS only |
| II. Design Fidelity | Deviations from designer intent must be flagged and resolved with the designer, not assumed | **PASS w/ condition** — designer notes are qualitative ("a little more," "a lot more, nothing drastic"); this plan proposes concrete candidate values in `research.md`, but per spec FR-010/SC-001 the designer MUST confirm the final rendered result before this feature is considered done |
| III. No Site-Implemented Motion (NON-NEGOTIABLE) | No animation/transition introduced | **PASS** — spacing, sizing, and letter-spacing changes only; no transitions added |
| IV. CSS-First Interactivity, Minimal JavaScript | Prefer CSS; no JS unless CSS can't do it | **PASS** — entirely achievable via CSS property changes and text edits; no JavaScript touched |
| V. Content Updatable Without Touching Layout | Content changes shouldn't require layout/CSS edits | **N/A** — this feature *is* a layout/CSS/typography change, not a content addition; does not weaken the principle for future content edits |
| VI. Accessibility and Performance Baseline | Alt text, semantic HTML, contrast, no console errors, no breakpoint breakage | **PASS w/ verification** — no `alt` text or semantics change; contrast is unaffected (no color changes); increased letter-spacing/padding must be checked at all breakpoints per FR-009 to confirm no wrapping/overflow regressions (see `quickstart.md`) |

No unjustified violations. Complexity Tracking table below is not needed.

## Project Structure

### Documentation (this feature)

```text
specs/003-landing-page-design-polish/
├── plan.md              # This file (/speckit-plan command output)
├── research.md          # Phase 0 output (/speckit-plan command)
├── data-model.md        # Phase 1 output (/speckit-plan command)
├── quickstart.md        # Phase 1 output (/speckit-plan command)
├── contracts/           # Phase 1 output (/speckit-plan command)
└── tasks.md             # Phase 2 output (/speckit-tasks command - NOT created by /speckit-plan)
```

### Source Code (repository root)

```text
index.html                  # Hero section markup: nav link text, title/meta
                             # (em dash removal), hero-visual/hero-card structure
assets/
└── css/
    └── styles.css           # .site-nav a, .hero, .hero-visual, .hero-visual-backdrop,
                              # .hero-card, .hero-card p letter-spacing/padding rules,
                              # including the three responsive breakpoint blocks
```

**Structure Decision**: Single static site project (matches `002-landing-page`
and the repo's existing flat structure — no `src/`, no frontend/backend
split). This feature only edits the two files above; no new files,
directories, or build tooling are introduced.

## Complexity Tracking

*No constitution violations — table not applicable.*
