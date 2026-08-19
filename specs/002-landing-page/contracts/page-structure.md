# Contract: Landing Page Structure & Shared Assets

This feature's "interface" is the markup structure and asset paths that
future features (Work gallery, Contact) are expected to reuse or fulfill.
This documents that contract at the structural level — actual HTML/CSS
belongs to the implementation phase, not this document.

## Header / navigation contract

The header markup and its four nav links are expected to be copied
verbatim into future pages (`work.html`, a contact page) so navigation is
consistent site-wide, per constitution Principle IV (plain `<a>` tags,
site-wide).

| Nav label | `href` | Contract |
|---|---|---|
| About | `#bio` (or equivalent in-page anchor id) | MUST resolve on every page — either by scrolling to a bio section (on the landing page) or by linking back to `index.html#bio` (on other pages) |
| Work | `work.html` | MUST become a real page when the Work gallery feature ships; until then, 404 is an accepted temporary state |
| Contact | `#` | Placeholder, same treatment as Services, until the Contact feature is speced (spec FR-014) |
| Services | `#` or `services.html` | Scope undecided; future spec MUST either wire this to a real destination or the nav item MUST be removed — it MUST NOT ship indefinitely as a dead link once other pages exist |

## Placeholder asset path contract

Future work that supplies real files MUST use these exact paths so
`index.html` requires no changes beyond removing the "expected 404" caveat:

| Asset | Path | Fulfilled by |
|---|---|---|
| Headshot photo | ~~`assets/images/profile/ShelleyCerny-Headshot.jpg`~~ → `assets/images/ShelleyCerny_Photo01.png` | Fulfilled 2026-08-19 |
| Logo | ~~`assets/images/logo/ShelleyCerny-Logo.svg`~~ → `assets/images/logo/ShelleyCerny-Logo.png` | Fulfilled 2026-08-19 |
| Resume PDF | `assets/resume/ShelleyCerny-Resume.pdf` | Still outstanding — designer supplies file; no code change needed once added |
| Hero backdrop pattern | `assets/images/ShelleyCerny_Pattern01.png` | New asset added 2026-08-19, not in the original placeholder set — replaces the solid `--color-accent-yellow` fill |

## Shared design tokens contract

Colors and fonts established in `research.md` are expected to be reused
(not re-derived) by future pages built from the same design system:

| Token | Value |
|---|---|
| `--color-background` | `#F9F8F3` |
| `--color-panel-teal` | `#1F7A8C` |
| `--color-accent-yellow` | `#E8B601` |
| `--color-text-green` | `#5D8C6A` |
| `--color-text-body` | `#0C0B09` |
| `--color-cta-purple` | `#9C8BBF` |
| `--color-text-on-dark` | `#FFFFFF` |
| Display font | ~~Space Mono, 700~~ → Barlow Condensed, 700 (superseded 2026-08-19) |
| Body font | ~~Inter, 400/500~~ → Barlow Condensed, 400/500 (superseded 2026-08-19; site now uses one family site-wide) |

Future specs SHOULD define these as CSS custom properties in
`assets/css/styles.css` (rather than repeating raw hex values) the first
time a second page is added, so the palette has one source of truth.
