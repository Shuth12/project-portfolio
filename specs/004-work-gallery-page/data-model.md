# Phase 1 Data Model: Work Gallery Page

This feature has no database or runtime data — "data model" here means the
static content structure: the fixed catalog of Projects that both
`work.html` and the `work/*.html` detail pages are hand-authored from.

## Entity: Project

| Field | Type | Description |
|---|---|---|
| `title` | string | Display name shown as the page `<h1>` on the detail page (and as `alt`-text context for the grid thumbnail) |
| `slug` | string | Kebab-case identifier used for the detail page filename (`work/<slug>.html`) |
| `assetFolder` | path | Existing folder under `assets/images/` this project's images live in |
| `thumbnail` | path | The `*_MockUp_Thumbnail.*` file from `assetFolder`, used only on the `work.html` grid |
| `detailImages` | path[] | The remaining images in `assetFolder`, shown on the project's own detail page |

**Validation rules** (from spec FR-002–FR-008):
- Every Project MUST have exactly one `thumbnail` and at least one
  `detailImages` entry.
- Every image reference (`thumbnail` and each `detailImages` entry) MUST
  have accompanying `alt` text naming the project and, where useful, the
  specific piece shown.
- `slug` MUST be unique across all Projects (enforces one detail page per
  project, FR-005).

## Entity: Work Grid

An ordered list of all ten Projects, rendered on `work.html` in the order
below (left-to-right, top-to-bottom, matching the reference mockup).

## Entity: Project Detail Page

One per Project (`work/<slug>.html`). Renders `title`, all `detailImages`,
and a link back to `work.html` (FR-006).

## Project Catalog (10 entries, mockup order)

| # | title | slug | assetFolder | thumbnail | detailImages |
|---|---|---|---|---|---|
| 1 | The Yoga Space | `the-yoga-space` | `yoga_space` | `YogaSpace_MockUp_Thumbnail.jpg` | `YogaSpace_Branding.jpg`, `YogaSpace_Website_Mockup.jpg`, `YogaSpace_Website_Mockup2.jpg` |
| 2 | Red Cedar Coffee | `red-cedar-coffee` | `red_cedar` | `RedCedar_MockUp_Thumbnail.jpg` | `RedCedar_MockUp.jpg`, `Red_Cedar_Branding.jpg` |
| 3 | Bouncy | `bouncy` | `bouncy` | `Bouncy_MockUp_Thumbnail.jpg` | `Bouncy_Branding.jpg`, `Bouncy_MockUp.jpg`, `Bouncy_Logo_Bounce.gif` (shown as-provided per constitution's portfolio-content motion exception, FR-010) |
| 4 | GoPint | `go-pint` | `go_pints` | `GoPint_MockUp_Thumbnail.jpg` | `GoPint_Mockup.jpg`, `GoPints_Branding.jpg` |
| 5 | Boyd Consulting | `boyd-consulting` | `boyd` | `Boyd_MockUp_Thumbnail.jpg` | `Boyd_Branding.jpg`, `Boyd_Logo_Ideas.jpg`, `Boyd_Business_Card.jpg`, `Boyd_Letterhead.jpg`, `Boyd_PowerPointMockUp.jpg` |
| 6 | Invitations | `invitations` | `invitations` | `Invitations_MockUp_Thumbnail.jpg` | `Invitation_ShelleyCerny-Invitation.jpg`, `Oh Baby - Baby Shower Invitation.jpg`, `Flower Baby Shower Invitation.jpg`, `Oil Painting - Wedding Invitation.jpg`, `Greenery - Wedding Invitation.jpg`, `Minimalist Image - Wedding Invitation.jpg` |
| 7 | Social Media Content | `fit4mom` | `fit_for_mom` | `Fit4Mom_MockUp_Thumbnail.jpg` | `Fit4Mom_Email_Mockup.jpg`, `Fit4Mom_Social_Post_Mockup.jpg`, `Fit4Mom_Social_Story_Mockup.jpg` |
| 8 | Herman Miller Book Design | `book` | `book` | `Book_MockUp_Thumbnail.jpg` | `Book_MockUp_01.jpg`, `Book_MockUp_02.jpg`, `Book_MockUp_03.jpg` |
| 9 | Wedding Signs | `wedding-signage` | `wedding_sign` | `WeddingSigns_MockUp_Thumbnail.jpg` | `WeddingSign_Seating_Chart_01.jpg`, `WeddingSign_Seating_Chart_White.PNG`, `WeddingSign_Social_Media_01.jpg`, `WeddingSign_Table_Numbers_White.jpg`, `WeddingSigns_Cannoli_01.jpg`, `WeddingSigns_Donuts_02.jpg`, `Welcome Sign_Katie.jpeg`, `Welcome_Sign_White.PNG` |
| 10 | Murals | `murals` | `murals` | `Murals_MockUp_Thumbnail.jpg` | `Murals_Custom Art CurvedBillboard.jpg`, `Murals_Graffito - Denim Mural Mockup.jpg`, `Murals_Lineup - Lava Window Sign.jpg` |

All filenames above are the actual, already-committed files under
`assets/images/<assetFolder>/` (verified during Phase 0/spec discovery) — no
new image processing is required for this feature (see research.md).
