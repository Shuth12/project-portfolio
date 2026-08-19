# Phase 1 Data Model: Landing Page (Home / About)

No persisted or dynamic data applies to this feature — the landing page is
static markup with no forms, database, or client-side state. The entities
below (from the spec's Key Entities section) are content structures baked
directly into `index.html`, documented here for completeness rather than as
a runtime data model.

## Bio Content

Inline text/markup in `index.html`. No separate content file or CMS.

| Field | Type | Notes |
|---|---|---|
| Name | Text | "Shelley" (heading: "Hi I'm Shelley,") |
| Bio paragraph | Text (rich text not required — plain paragraph) | Background, design focus, role sought; matches mockup tone (spec FR-003) |
| Headshot photo | Image reference | `assets/images/ShelleyCerny_Photo01.png` — real asset, supplied 2026-08-19 (supersedes the original placeholder path; spec FR-002) |

## Resume File

A single static asset linked from the CTA button, not an entity with
attributes beyond its file path.

| Field | Type | Notes |
|---|---|---|
| File path | Relative URL | Placeholder `assets/resume/ShelleyCerny-Resume.pdf`; expected to 404 until supplied (spec FR-013) |

## Navigation Menu

A fixed, hard-coded list of four links rendered in the page header. No
admin/editing mechanism — changing a link means editing `index.html`.

| Label | Target | State |
|---|---|---|
| About | In-page anchor to the bio section (e.g. `#bio` or `#top`) | Resolves within this page (spec FR-010) |
| Work | `work.html` | Placeholder — page not yet built (spec FR-011) |
| Contact | `#` | Placeholder, same treatment as Services (spec FR-014) |
| Services | Placeholder destination (e.g. `#` or `services.html`) | Scope undecided, deferred (spec FR-012) |

## Logo

| Field | Type | Notes |
|---|---|---|
| Logo image | Image reference | `assets/images/logo/ShelleyCerny-Logo.png` — real asset, supplied 2026-08-19 (supersedes the original placeholder path; spec FR-001) |

## Hero Backdrop

Added post-implementation; not part of the original spec's Key Entities.

| Field | Type | Notes |
|---|---|---|
| Backdrop pattern | Image reference | `assets/images/ShelleyCerny_Pattern01.png` — a wavy vertical-stripe pattern, supplied 2026-08-19, rendered as `.hero-visual-backdrop`'s `background-image`. Replaces the original solid `--color-accent-yellow` fill described in FR-006. |
