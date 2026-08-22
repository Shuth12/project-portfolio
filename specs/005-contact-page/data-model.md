# Phase 1 Data Model: Contact Page

This feature has no database or runtime data — "data model" here means the
static content structure that `contact.html` is hand-authored from. There is
a single page with fixed content (no repeated/list entities, unlike the Work
Gallery Page's Project catalog).

## Entity: Contact Page

| Field | Type | Description |
|---|---|---|
| `heading` | string | The page's greeting, `"Say Hello!"`, styled like `index.html`'s `"Hi, I'm Shelley,"` hero heading |
| `bodyCopy` | string | The invitation paragraph shown left of the photo (see spec Input for exact copy) |
| `photo` | path | `assets/images/ShelleyCerny_Photo02.png`, overlapping the card's right edge with its own drop shadow |
| `backgroundPattern` | path | `assets/images/Shelleycerny-checkared.png`, tiled behind the card across the full-bleed teal content area |
| `ctaLabel` | string | `"Send Me An Email"` |
| `ctaHref` | string | `mailto:shelley.cerny@gmail.com` |

**Validation rules** (from spec FR-004–FR-009):

- The card MUST have exactly one heading, one body-copy block, one photo,
  and one CTA button.
- `ctaHref` MUST be a `mailto:` URI addressed to `shelley.cerny@gmail.com`
  (spec FR-009) — no other link target is valid for this control.
- `photo` MUST have accompanying `alt` text identifying Shelley (spec
  FR-011).

## Entity: Site Navigation ("Contact" link)

Not new data, but an existing field being updated: every page's header nav
currently has a `"Contact"` link pointing to the placeholder `#`. This
feature updates that link's target to `contact.html` (root-level pages) or
`../contact.html` (pages under `work/`) across all 12 existing pages, per
spec FR-002.
