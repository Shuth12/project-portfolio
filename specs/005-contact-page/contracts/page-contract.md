# Page Contract: Contact Page

This static site has no API; the "contract" here is the fixed HTML
structure and linking convention that `contact.html` must follow, so
navigation stays consistent (spec FR-001, FR-002) and the page matches the
reference mockup (spec FR-004–FR-009).

## `contact.html`

**Required structure**:

```html
<header class="site-header">...</header>          <!-- identical to index.html's header, except the "Contact" link now points to contact.html itself -->
<div class="wave-divider" aria-hidden="true"></div> <!-- identical to index.html -->

<main class="contact-main">                        <!-- full-bleed teal area, tiled checkerboard background -->
  <div class="contact-card">                        <!-- off-white card, drop shadow -->
    <div class="contact-card-content">
      <h1>Say Hello!</h1>
      <p>
        Whether you are looking for a UX/UI designer, need a brand identity
        refresh, or just want to talk design, I would love to hear from
        you. I am currently open to remote junior UX/UI design roles and
        freelance projects. Reach out and let's see what we can make
        together.
      </p>
      <a class="button button--resume" href="mailto:shelley.cerny@gmail.com">
        Send Me An Email
      </a>
    </div>
    <img
      class="contact-photo"
      src="assets/images/ShelleyCerny_Photo02.png"
      alt="Shelley Cerny smiling, sitting on a couch"
    />
  </div>
</main>

<footer class="site-footer">...</footer>          <!-- identical to index.html's footer -->
```

**Contract guarantees**:

- Header/footer markup is byte-for-byte consistent with the equivalent
  markup on `index.html`/`work.html` (same nav links, same logo, same
  footer text), except every page's "Contact" nav link now targets this
  page.
- The card contains exactly one heading (`"Say Hello!"`), one body-copy
  paragraph, one `mailto:` CTA button, and one photo — no additional
  content.
- The CTA's `href` is exactly `mailto:shelley.cerny@gmail.com`.
- The photo has non-empty, descriptive `alt` text.

## Nav link update (all 12 existing pages)

**Contract guarantee**: On `index.html`, `work.html`, and every
`work/<slug>.html` detail page, the header's `"Contact"` link's `href`
changes from the placeholder `#` to:

- `contact.html` — for `index.html` and `work.html` (repo root)
- `../contact.html` — for every page under `work/`

No other nav link, and no other part of the header/footer, changes.

## Linking convention

- Any existing page → Contact: relative path `contact.html` (from repo
  root) or `../contact.html` (from inside `work/`).
- Contact → About/logo: relative path `index.html#bio`, matching the
  existing convention already used by `work.html` and every detail page.
- Contact → Work: relative path `work.html`, matching the existing
  convention.
- Contact's own CTA: `mailto:shelley.cerny@gmail.com` — the only
  non-navigational link on the page.
