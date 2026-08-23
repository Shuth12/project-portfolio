# Phase 1 Data Model: Services Page

This feature has no database or runtime data — "data model" here means the
static content structure that `services.html` is hand-authored from. There
is a single page with a fixed heading and a fixed, ordered list of six
Service Item entities (unlike the Work Gallery Page's dynamic-feeling
project catalog, this list's size and content are fixed by the spec).

## Entity: Services Page

| Field | Type | Description |
|---|---|---|
| `heading` | string | The page's title, `"Services"`, styled like `index.html`'s `"Hi I'm Shelley,"` hero heading |
| `backgroundPattern` | path | `assets/images/Shelleycerny-blobs.png`, sized and positioned like the Contact page's `Shelleycerny-checkared.png` background |
| `services` | Service Item[6] | The six service offerings, rendered in the fixed order below |

## Entity: Service Item

| Field | Type | Description |
|---|---|---|
| `icon` | path | The service's icon image (see table below) |
| `iconAlt` | string | Descriptive alt text identifying the service (spec FR-009) |
| `subtitle` | string | The service's name, styled like `.project-subtitle` on Work detail pages |
| `description` | string | Centered body copy, styled like `.project-body` on Work detail pages |

**Fixed instances** (spec FR-008, in display order):

| # | `icon` | `subtitle` | `description` |
|---|---|---|---|
| 1 | `assets/images/ShelleyCerny_UXIcon.png` | UX/UI Design | From wireframes to high fidelity designs, I create digital experiences that are intuitive, intentional, and beautiful. |
| 2 | `assets/images/ShelleyCerny_BrandIcon.png` | Brand Identity | Logo design, color palettes, typography, and all the pieces that make a brand feel cohesive and memorable. |
| 3 | `assets/images/ShelleyCerny_PrintIcon.png` | Print Design | Business cards, letterheads, event materials, and beyond. Designed with the same attention to detail as any digital project. |
| 4 | `assets/images/ShelleyCerny_SocialIcon.png` | Social Media Design | On brand, scroll stopping content that actually connects with your audience. |
| 5 | `assets/images/ShelleyCerny_WebIcon.png` | Web Design | Clean, user centered website designs that look great and feel effortless to navigate. |
| 6 | `assets/images/ShelleyCerny_LetteringIcon.png` | Illustration & Hand Lettering | Custom hand lettered signage, murals, and illustrated design elements with a personal touch. |

**Validation rules** (from spec FR-005–FR-009):

- The card MUST have exactly one heading and exactly six Service Items, in
  the fixed order above.
- Each Service Item MUST render icon-then-subtitle-then-description,
  top to bottom, center-aligned.
- Each `icon` MUST have accompanying, non-empty `alt` text identifying the
  service it represents (spec FR-009).

## Entity: Site Navigation ("Services" link)

Not new data, but an existing field being updated: every page's header nav
currently has a `"Services"` link pointing to the placeholder `#`. This
feature updates that link's target to `services.html` (root-level pages) or
`../services.html` (pages under `work/`) across all 13 existing pages, per
spec FR-002.
