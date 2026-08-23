# Page Contract: Services Page

This static site has no API; the "contract" here is the fixed HTML
structure and linking convention that `services.html` must follow, so
navigation stays consistent (spec FR-001, FR-002) and the page matches the
reference mockup (spec FR-004–FR-009).

## `services.html`

**Required structure**:

```html
<header class="site-header">...</header>          <!-- identical to index.html's header, except the "Services" link now points to services.html itself -->
<div class="wave-divider" aria-hidden="true"></div> <!-- identical to index.html -->

<main class="services-main">                        <!-- full-bleed teal area, Shelleycerny-blobs background -->
  <div class="services-card">                        <!-- off-white card, rounded corners, strong drop shadow -->
    <h1>Services</h1>

    <div class="services-grid">
      <div class="service-item">
        <img src="assets/images/ShelleyCerny_UXIcon.png" alt="UX/UI design icon" />
        <h2 class="project-subtitle">UX/UI Design</h2>
        <p class="project-body">
          From wireframes to high fidelity designs, I create digital
          experiences that are intuitive, intentional, and beautiful.
        </p>
      </div>
      <div class="service-item">
        <img src="assets/images/ShelleyCerny_BrandIcon.png" alt="Brand identity icon" />
        <h2 class="project-subtitle">Brand Identity</h2>
        <p class="project-body">
          Logo design, color palettes, typography, and all the pieces that
          make a brand feel cohesive and memorable.
        </p>
      </div>
      <div class="service-item">
        <img src="assets/images/ShelleyCerny_PrintIcon.png" alt="Print design icon" />
        <h2 class="project-subtitle">Print Design</h2>
        <p class="project-body">
          Business cards, letterheads, event materials, and beyond.
          Designed with the same attention to detail as any digital
          project.
        </p>
      </div>
      <div class="service-item">
        <img src="assets/images/ShelleyCerny_SocialIcon.png" alt="Social media design icon" />
        <h2 class="project-subtitle">Social Media Design</h2>
        <p class="project-body">
          On brand, scroll stopping content that actually connects with
          your audience.
        </p>
      </div>
      <div class="service-item">
        <img src="assets/images/ShelleyCerny_WebIcon.png" alt="Web design icon" />
        <h2 class="project-subtitle">Web Design</h2>
        <p class="project-body">
          Clean, user centered website designs that look great and feel
          effortless to navigate.
        </p>
      </div>
      <div class="service-item">
        <img src="assets/images/ShelleyCerny_LetteringIcon.png" alt="Illustration and hand lettering icon" />
        <h2 class="project-subtitle">Illustration &amp; Hand Lettering</h2>
        <p class="project-body">
          Custom hand lettered signage, murals, and illustrated design
          elements with a personal touch.
        </p>
      </div>
    </div>
  </div>
</main>

<footer class="site-footer">...</footer>          <!-- identical to index.html's footer -->
```

**Contract guarantees**:

- Header/footer markup is byte-for-byte consistent with the equivalent
  markup on `index.html`/`work.html`/`contact.html` (same nav links, same
  logo, same footer text), except every page's "Services" nav link now
  targets this page.
- The card contains exactly one heading (`"Services"`) and exactly six
  `.service-item` blocks, each with exactly one icon, one subtitle, and one
  description, in the fixed order defined in `data-model.md`.
- Every icon has non-empty, descriptive `alt` text.
- No `.service-item` contains a link or button — the grid is informational
  only (per spec Assumptions).

## Nav link update (all 13 existing pages)

**Contract guarantee**: On `index.html`, `work.html`, `contact.html`, and
every `work/<slug>.html` detail page, the header's `"Services"` link's
`href` changes from the placeholder `#` to:

- `services.html` — for `index.html`, `work.html`, and `contact.html` (repo
  root)
- `../services.html` — for every page under `work/`

No other nav link, and no other part of the header/footer, changes.

## Linking convention

- Any existing page → Services: relative path `services.html` (from repo
  root) or `../services.html` (from inside `work/`).
- Services → About/logo: relative path `index.html#bio`, matching the
  existing convention already used by `work.html` and `contact.html`.
- Services → Work: relative path `work.html`, matching the existing
  convention.
- Services → Contact: relative path `contact.html`, matching the existing
  convention.
- The Services page itself has no outbound content links — it is
  informational only.
