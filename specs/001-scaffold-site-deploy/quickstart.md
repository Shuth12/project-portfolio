# Quickstart: Site Scaffold & Deploy Pipeline

Validates the feature end-to-end against the spec's acceptance scenarios
and success criteria. No build tooling is required.

## Prerequisites

- Repository Settings → Pages → **Source** set to **"GitHub Actions"**
  (one-time manual setting; not part of any commit — see `research.md`).
- Local: any static file server or just opening the HTML file directly in a
  browser. No dependencies to install.

## 1. Verify the placeholder page locally

```bash
open index.html
# or: python3 -m http.server 8000   (then visit http://localhost:8000)
```

**Expected**: page loads with a real `<title>`, a visible "site under
construction" message, semantic HTML, no console errors, and no layout
breakage when the browser window is narrowed to a mobile width. Validates
User Story 2 / FR-002 / FR-007 / SC-003.

## 2. Verify non-`main` branches never deploy

```bash
git checkout development
git commit --allow-empty -m "chore: verify no deploy from development"
git push origin development
```

**Expected**: no new run appears under the repository's Actions tab for the
deploy workflow. Validates User Story 3 / FR-004 / SC-004.

## 3. Verify deploy on merge to `main`

```bash
git checkout main
git merge development
git push origin main
```

**Expected**: a new "Deploy to GitHub Pages" run starts automatically in the
Actions tab (no manual trigger), and completes successfully. Validates User
Story 1 / FR-003.

## 4. Verify the live site

Visit `https://shuth12.github.io/project-portfolio/`.

**Expected**: the same placeholder page verified in step 1 loads within ~2
seconds, within 5 minutes of the push in step 3, matching SC-001 and
SC-002.

## 5. Verify failure visibility and manual re-run

Temporarily break the workflow (e.g., push an invalid YAML change to
`main` on a throwaway commit), confirm the run shows as **failed** in the
Actions tab and the previously-deployed page is still live and unchanged,
then revert the break and use the Actions tab's **"Re-run jobs"** action to
confirm a manual re-run works without a new commit. Validates edge cases /
FR-005 / FR-006.
