---

description: "Task list template for feature implementation"
---

# Tasks: Site Scaffold & Deploy Pipeline

**Input**: Design documents from `/specs/001-scaffold-site-deploy/`

**Prerequisites**: plan.md, spec.md, research.md, data-model.md, contracts/deploy-workflow.md, quickstart.md

**Tests**: Not requested in the feature spec — this feature is validated via the manual steps in `quickstart.md` instead of an automated test suite (no framework is warranted for one static page and one workflow file).

**Organization**: Tasks are grouped by user story to enable independent implementation and testing of each story.

## Format: `[ID] [P?] [Story] Description`

- **[P]**: Can run in parallel (different files, no dependencies)
- **[Story]**: Which user story this task belongs to (e.g., US1, US2, US3)
- Include exact file paths in descriptions

## Path Conventions

Single static site at the repository root (see `plan.md` Project Structure): `index.html`, `assets/css/styles.css`, `.github/workflows/deploy.yml`. No `src/`/`tests/` split — this is not a code library.

---

## Phase 1: Setup (Shared Infrastructure)

**Purpose**: Create the directories the feature's files will live in

- [X] T001 Create the `.github/workflows/` directory in the repository root for the deploy workflow
- [X] T002 [P] Create the `assets/css/` directory in the repository root for placeholder styling

---

## Phase 2: Foundational (Blocking Prerequisites)

**Purpose**: Prerequisites that MUST be in place before any user story can be verified end-to-end

**⚠️ CRITICAL**: No user story work can be verified live until this phase is complete

- [X] T003 Enable GitHub Pages with **Source = "GitHub Actions"** in the repository's Settings → Pages (manual, one-time repository setting; steps in `specs/001-scaffold-site-deploy/quickstart.md` Prerequisites) — already configured from the repo's prior Hugo-based Pages deployment; confirmed by user
- [X] T004 [P] Create a minimal `index.html` scaffold at the repository root with `<!DOCTYPE html>`, `<html lang="en">`, and a `<head>` containing a real `<title>` (empty `<body>` for now) — gives US1 something deployable and gives US2 a file to fill in

**Checkpoint**: Foundation ready — user story implementation can now begin

---

## Phase 3: User Story 1 - Automatic publish on merge to main (Priority: P1) 🎯 MVP

**Goal**: Any change merged into `main` is automatically published to the site's public URL with no manual step.

**Independent Test**: Merge this feature's changes into `main` and confirm a deploy workflow run starts automatically and the live URL serves the current `index.html`, without running any manual publish command.

### Implementation for User Story 1

- [X] T005 [US1] Add the trigger, permissions, and concurrency configuration (`push: branches: [main]`, `workflow_dispatch`, `permissions: contents: read / pages: write / id-token: write`, `concurrency: group: pages, cancel-in-progress: false`) to `.github/workflows/deploy.yml`, per `specs/001-scaffold-site-deploy/contracts/deploy-workflow.md`
- [X] T006 [US1] Add a build job to `.github/workflows/deploy.yml` using `actions/checkout@v4` followed by `actions/configure-pages@v5`
- [X] T007 [US1] Add an `actions/upload-pages-artifact@v3` step to the build job in `.github/workflows/deploy.yml` uploading the repository root (`.`) as the Pages artifact
- [X] T008 [US1] Add a deploy job to `.github/workflows/deploy.yml` using `actions/deploy-pages@v4`, with `needs: build` and `environment: name: github-pages`
- [ ] T009 [US1] Run `specs/001-scaffold-site-deploy/quickstart.md` steps 3–4 to verify a merge to `main` triggers an automatic deploy and the live URL serves the current page within the expected time — **PENDING: requires pushing to `main` on GitHub, needs user go-ahead**

**Checkpoint**: At this point, User Story 1 should be fully functional — merges to `main` deploy automatically.

---

## Phase 4: User Story 2 - Clear "under construction" placeholder (Priority: P2)

**Goal**: A visitor who loads the site sees an intentional placeholder page, not a blank or broken one.

**Independent Test**: Load `index.html` locally (or the deployed URL) with no other context and confirm a page renders with a clear "under construction" message, a real page title, semantic HTML, and no console errors or mobile-width layout breakage.

### Implementation for User Story 2

- [X] T010 [US2] In `index.html`, add placeholder body content inside a `<main>` landmark: a single `<h1>` identifying the site and a paragraph stating it's under construction, plus a `<link rel="stylesheet" href="assets/css/styles.css">` in `<head>`
- [X] T011 [P] [US2] Create `assets/css/styles.css` with minimal responsive styling (single-column layout, legible type size, no animation/transition properties) so the page reads cleanly at both mobile and desktop widths
- [X] T012 [US2] Run `specs/001-scaffold-site-deploy/quickstart.md` step 1 to verify the page loads with no console errors and no layout breakage at a narrowed (mobile-width) browser window

**Checkpoint**: At this point, User Stories 1 AND 2 both work — the pipeline deploys a real placeholder page.

---

## Phase 5: User Story 3 - Deploy only from `main` (Priority: P3)

**Goal**: Pushes to `development` or any other branch never affect the live site.

**Independent Test**: Push a change to `development` and confirm no deploy run fires; then merge the same change to `main` and confirm a deploy run does fire.

### Implementation for User Story 3

- [X] T013 [US3] Confirm the `push:` trigger added in `.github/workflows/deploy.yml` (T005) lists only `main` under `branches:`, with no other branch names present
- [ ] T014 [US3] Run `specs/001-scaffold-site-deploy/quickstart.md` step 2 to verify a push to `development` triggers no workflow run — **PENDING: requires pushing to `development` on GitHub, needs user go-ahead**

**Checkpoint**: All three user stories are now independently verified.

---

## Phase 6: Polish & Cross-Cutting Concerns

**Purpose**: Validate the edge cases that span all user stories

- [ ] T015 Run `specs/001-scaffold-site-deploy/quickstart.md` step 5 to verify a failed deploy run is visible as a failed run in the Actions tab, the previously-deployed page stays live and unchanged, and a manual re-run succeeds without a new commit — **PENDING: requires pushing to `main` on GitHub, needs user go-ahead**

---

## Dependencies & Execution Order

### Phase Dependencies

- **Setup (Phase 1)**: No dependencies — start immediately
- **Foundational (Phase 2)**: Depends on Setup completion — BLOCKS all user stories
- **User Stories (Phase 3–5)**: All depend on Foundational phase completion
  - US1, US2, and US3 can proceed in parallel if staffed; sequentially they follow priority order (P1 → P2 → P3)
- **Polish (Phase 6)**: Depends on US1 and US3 being complete (needs a working, correctly-triggered deploy to validate failure/re-run behavior)

### User Story Dependencies

- **User Story 1 (P1)**: Depends only on Foundational — no dependency on US2/US3
- **User Story 2 (P2)**: Depends only on Foundational (specifically T004's `index.html` scaffold) — independently testable locally without US1's live deploy
- **User Story 3 (P3)**: Depends on US1's T005 (the trigger this story validates) — this is the one place priority order matters, since US3 verifies behavior US1 implements

### Parallel Opportunities

- T001 and T002 (Setup) can run in parallel
- T003 and T004 (Foundational) can run in parallel
- T010 and T011 (US2) can run in parallel — different files
- Once Foundational is complete, a second contributor could start US2 (T010–T012) while US1 (T005–T009) is still in progress, since US2 only needs `index.html` to exist

---

## Parallel Example: Foundational + User Story 2

```bash
# Foundational, launched together:
Task: "Enable GitHub Pages Source = GitHub Actions in repository settings"
Task: "Create minimal index.html scaffold at repository root"

# User Story 2 implementation, launched together (after T004):
Task: "Add placeholder body content + stylesheet link to index.html"
Task: "Create assets/css/styles.css with minimal responsive styling"
```

---

## Implementation Strategy

### MVP First (User Story 1 Only)

1. Complete Phase 1: Setup
2. Complete Phase 2: Foundational (CRITICAL — blocks all stories)
3. Complete Phase 3: User Story 1
4. **STOP and VALIDATE**: run `quickstart.md` steps 3–4 to confirm the pipeline auto-deploys
5. At this point the site is live (with the bare scaffold from T004) — a working MVP deploy pipeline

### Incremental Delivery

1. Setup + Foundational → foundation ready
2. Add User Story 1 → validate independently → pipeline proven (MVP)
3. Add User Story 2 → validate independently → real placeholder content live
4. Add User Story 3 → validate independently → branch isolation confirmed
5. Polish → validate failure/re-run edge cases

## Notes

- [P] tasks touch different files and have no ordering dependency on each other
- [Story] label maps each task to its user story for traceability
- This feature has no automated tests per `plan.md`'s Technical Context — validation is via `quickstart.md`
- Commit after each phase checkpoint, per the constitution's "commit often at logical checkpoints" workflow rule
- Avoid: editing `.github/workflows/deploy.yml` and `index.html` in parallel across tasks that touch the same file (T005–T008 and T010 are intentionally sequential for this reason)
