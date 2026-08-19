# Phase 0 Research: Site Scaffold & Deploy Pipeline

No `NEEDS CLARIFICATION` markers remained in the Technical Context, so
research here consolidates the deploy-mechanism decisions needed to satisfy
the spec's functional requirements and the constitution's static-only
constraint.

## Decision: Deploy via GitHub's official Pages Actions, not a branch push

**Decision**: Use `actions/configure-pages`, `actions/upload-pages-artifact`,
and `actions/deploy-pages` in a workflow triggered on `push: branches:
[main]` plus `workflow_dispatch`, with Pages source set to "GitHub Actions"
in repository settings.

**Rationale**:
- Satisfies FR-003 (auto-publish on merge to `main`) and FR-004 (never
  auto-publish from other branches) directly via the trigger's branch filter.
- `workflow_dispatch` satisfies FR-005 (re-run on demand without a new
  commit).
- A failed run shows as a failed run in the Actions tab by default,
  satisfying FR-006 with no extra configuration.
- No third-party action or extra `gh-pages` branch to keep in sync — the
  published artifact is built directly from what's already in `main`,
  matching constitution I (no build step required, static files served
  as-is).
- This exact pattern (`configure-pages` → `upload-pages-artifact` →
  `deploy-pages`, same trigger shape) was already used successfully by this
  repository's prior Hugo-based deploy workflow (see `git show
  73fe6b2:.github/workflows/deploy.yml`), minus the Hugo build step this
  project no longer needs.

**Alternatives considered**:
- **`peaceiris/actions-gh-pages` (push to a `gh-pages` branch)** — rejected:
  adds a third-party action dependency and a second branch to reason about,
  with no benefit for a project with no build step.
- **Manual `git subtree push` to a `gh-pages` branch or `/docs` folder** —
  rejected: reintroduces a manual publish step, violating FR-003's "no
  manual publish step" requirement outright.

## Decision: No CSS framework or JS for the placeholder

**Decision**: Ship one plain `index.html` with a single linked
`assets/css/styles.css` file; no JavaScript.

**Rationale**: A placeholder page has no interactive behavior to implement,
so constitution IV's "CSS-first, minimal JS" floor is trivially met by using
no JS at all. Introducing a CSS framework would add a dependency with zero
payoff for one page and cuts against constitution I's minimal-footprint
intent.

**Alternatives considered**:
- **A CSS framework/reset library** — rejected as unnecessary weight for a
  single placeholder page; can be reconsidered once real page layouts (from
  the provided mockups) are being implemented.

## Decision: GitHub Pages source = default `github.io` project URL

**Decision**: Repository Pages settings will be configured with source
"GitHub Actions" (not a branch), and no `CNAME`/custom domain is added in
this feature. The live URL will be `https://shuth12.github.io/project-portfolio/`.

**Rationale**: Resolves the PRD's open question about Pages source/branch —
"GitHub Actions" as the source is required for the `deploy-pages` action
approach and needs no branch/folder convention decision. Matches spec
Assumption that custom domain work is deferred.

**Alternatives considered**:
- **`main` branch `/root` or `/docs` as Pages source** — rejected: requires
  either committing published output at repo root (fine here, but still a
  branch-based source) or a `/docs` copy step; "GitHub Actions" as source is
  the simpler, currently-recommended mechanism and needs no extra folder.
