# Implementation Plan: Site Scaffold & Deploy Pipeline

**Branch**: `001-scaffold-site-deploy` | **Date**: 2026-08-18 | **Spec**: [spec.md](./spec.md)

**Input**: Feature specification from `/specs/001-scaffold-site-deploy/spec.md`

**Note**: This template is filled in by the `/speckit-plan` command; its definition describes the execution workflow.

## Summary

Stand up the minimal static site (a single placeholder home page) and a
GitHub Actions workflow that automatically publishes the current contents of
`main` to GitHub Pages on every push/merge to `main`, and never on
`development` or feature branches. No build tooling, framework, or backend
is introduced — the placeholder ships as plain HTML/CSS and the workflow
uses GitHub's official Pages actions (`configure-pages`,
`upload-pages-artifact`, `deploy-pages`) to publish the repository's static
files as-is.

## Technical Context

**Language/Version**: HTML5, CSS3 (no JavaScript needed for a placeholder page)

**Primary Dependencies**: None for the site itself. Deploy workflow uses
GitHub's official Actions: `actions/checkout`, `actions/configure-pages`,
`actions/upload-pages-artifact`, `actions/deploy-pages`.

**Storage**: N/A (no data, no database)

**Testing**: Manual verification via `quickstart.md` (load the page locally,
check GitHub Actions run status/logs, load the deployed URL). No automated
test framework is warranted for one static HTML page.

**Target Platform**: GitHub Pages (static hosting), modern evergreen
browsers (Chrome, Firefox, Safari, Edge)

**Project Type**: Static website — no backend, no build step, single
repository (no frontend/backend split)

**Performance Goals**: Placeholder page fully rendered within 2s on a
standard broadband connection (spec SC-001)

**Constraints**: Fully static (constitution I); no build step required to
publish; deploy MUST fire only on `main` (spec FR-003/FR-004); deploy MUST
be manually re-runnable without a new commit (spec FR-005); failures MUST
surface as a failed Actions run (spec FR-006)

**Scale/Scope**: One placeholder page, one GitHub Actions workflow file —
this feature intentionally excludes real portfolio content

## Constitution Check

*GATE: Must pass before Phase 0 research. Re-check after Phase 1 design.*

| Principle | Status | Notes |
|---|---|---|
| I. Static-Only, No Backend | PASS | Plain HTML/CSS, no build step required to publish; the GitHub Actions workflow is CI/CD tooling that publishes existing static files, not a runtime backend. |
| II. Design Fidelity | N/A (deferred) | This feature ships an explicit, temporary placeholder per the user's own request — it does not implement any of the provided mockups. Design fidelity applies once real Home/Work/Contact pages are built in later features. |
| III. No Site-Implemented Motion or Animation | PASS | Placeholder has no motion, transitions, or animated assets. |
| IV. CSS-First Interactivity, Minimal JavaScript | PASS | No JavaScript is used at all — even more minimal than the floor the principle requires. Navigation (none yet) will use plain `<a>` tags when added. |
| V. Content Updatable Without Touching Layout | N/A (deferred) | A single placeholder page has no content/layout separation to make yet; applies once real per-project content is added in a later feature. |
| VI. Accessibility and Performance Baseline | PASS | Placeholder uses semantic HTML, a real `<title>`, logical heading structure, and no images requiring `alt` text; performance target captured in SC-001. |

No violations requiring justification — Complexity Tracking is not needed.

**Post-design re-check** (after Phase 1): design artifacts (research.md,
data-model.md, contracts/, quickstart.md) introduce no new dependencies,
build steps, JavaScript, motion, or backend components. All gate statuses
above are unchanged.

## Project Structure

### Documentation (this feature)

```text
specs/001-scaffold-site-deploy/
├── plan.md              # This file (/speckit-plan command output)
├── research.md          # Phase 0 output (/speckit-plan command)
├── data-model.md        # Phase 1 output (/speckit-plan command)
├── quickstart.md        # Phase 1 output (/speckit-plan command)
├── contracts/           # Phase 1 output (/speckit-plan command)
└── tasks.md             # Phase 2 output (/speckit-tasks command - NOT created by /speckit-plan)
```

### Source Code (repository root)

```text
index.html                     # Placeholder home page (semantic HTML, page title)
assets/
├── css/
│   └── styles.css              # Minimal placeholder styling only
├── images/                     # Existing design assets (already in repo)
└── page_mockups/                # Existing design reference mockups (already in repo)

.github/
└── workflows/
    └── deploy.yml               # Auto-deploy to GitHub Pages on push to main
```

**Structure Decision**: Single static website at the repository root — no
`src/`, no frontend/backend split, no build output directory. This matches
constitution principle I (no build step required) and the PRD's requirement
that GitHub Pages can serve the repository as-is. `assets/` already exists
from prior work; this feature adds only `index.html`,
`assets/css/styles.css`, and `.github/workflows/deploy.yml`.

## Complexity Tracking

> **Fill ONLY if Constitution Check has violations that must be justified**

No violations — table intentionally omitted.
