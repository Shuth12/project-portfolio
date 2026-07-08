# Portfolio Site

A custom-built Hugo portfolio site for a graphic designer. Deployed via GitHub Actions to GitHub Pages.

## Stack
- **Generator:** Hugo extended `v0.164.0`
- **Hosting:** GitHub Pages (via GitHub Actions)
- **Editing:** Markdown + Git — no CMS

## Local development

```bash
# Install Hugo extended (Mac)
brew install hugo

# Serve with drafts
hugo server -D

# Production build
hugo --minify
```

## Adding a new project

```bash
hugo new work/my-project-name.md
```

Edit the generated file in `content/work/`. Fill in the front matter fields:
- Set `draft = false` when ready to publish
- Set `flagship = true` for projects that get a full case-study page
- Add image paths to `cover` and `gallery`

## Content structure

```
content/
  work/        # Portfolio projects (one .md per project)
  about.md     # About page
  contact.md   # Contact page
```

## Deploy

Push to `main` — GitHub Actions builds and deploys automatically.
Before first deploy, enable GitHub Pages in repo Settings → Pages → Source: GitHub Actions.
