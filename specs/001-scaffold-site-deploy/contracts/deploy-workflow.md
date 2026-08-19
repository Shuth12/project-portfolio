# Contract: Deploy Workflow (`.github/workflows/deploy.yml`)

This feature's only external interface is the GitHub Actions workflow that
publishes the site. This documents its contract at the trigger/interface
level — implementation (the actual YAML steps) belongs to the tasks/
implementation phase, not this document.

## Trigger contract

| Trigger | Behavior |
|---|---|
| `push` to `main` | MUST run the full build-and-deploy job (FR-003) |
| `push` to `development` or any other branch | MUST NOT run (FR-004) |
| `workflow_dispatch` (manual) | MUST be available so a failed run can be retried without a new commit (FR-005) |

## Permissions contract

The workflow's `GITHUB_TOKEN` MUST be scoped to only what Pages deployment
needs:

- `contents: read`
- `pages: write`
- `id-token: write`

No broader permissions (e.g., `contents: write`) are required or granted.

## Concurrency contract

Deploys MUST be serialized (a `pages` concurrency group) so two overlapping
runs cannot publish out of order. An in-flight deploy MUST be allowed to
finish rather than being cancelled by a newer push, so a run is never left
half-published.

## Output contract

| Output | Guarantee |
|---|---|
| Success | The site at `https://shuth12.github.io/project-portfolio/` serves the exact contents of `main` at the time of the run, within SC-002's 5-minute window. |
| Failure | The run is marked failed in the repository's Actions tab (FR-006); the previously-deployed version of the site remains live and unchanged. |

## Site output contract

The workflow publishes the repository's static files as-is (no build/
transform step), so what's committed at repo root (`index.html`,
`assets/`) is exactly what's served. Relative paths in `index.html` MUST
resolve correctly under the project subpath
(`/project-portfolio/...`) rather than assuming the site is served from a
domain root.
