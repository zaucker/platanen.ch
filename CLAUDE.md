# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Hugo static site for **platanen.ch** — a neighborhood gallery website for "Platanen @ 4600" in Olten, Switzerland. German-language site showcasing photo galleries of neighborhood events and surroundings.

## Development Environment

Tools are managed via `mise.toml`:
- **Hugo Extended** (latest) — static site generator
- **Node.js** 24.9.0 — for Tailwind CSS
- **Dart Sass** 1.89.1

Run `mise install` to set up the toolchain.

## Common Commands

```bash
# Install Node dependencies (Tailwind CSS)
npm install

# Start Hugo dev server with live reload
hugo server

# Build Tailwind CSS from assets/css/main.css → static/css/main.css
npx @tailwindcss/cli -i assets/css/main.css -o static/css/main.css

# Production build
hugo --minify
```

## Architecture

**No external theme** — all layouts are custom-built in `layouts/`.

### Key Layout Files

- `layouts/_default/baseof.html` — base template (head, header, footer partials, mobile menu JS)
- `layouts/index.html` — homepage with hero section and gallery album preview grid
- `layouts/galerie/list.html` — gallery index showing album cards in responsive grid
- `layouts/galerie/single.html` — individual album page with photo grid and GLightbox lightbox
- `layouts/partials/` — head.html (meta/CSS/fonts), header.html (sticky nav), footer.html

### Content Structure

- `content/_index.md` — homepage
- `content/galerie/` — gallery albums, each as a page bundle (`index.md` + `images/` subdirectory)
- `content/kontakt/` — contact page

Gallery albums use `weight` in front matter for ordering.

### Styling

- **Tailwind CSS v4** configured in `assets/css/main.css` with custom theme colors:
  - `--color-platane` (#4a7c59), `--color-platane-dark`, `--color-platane-light`
  - Font: Inter (Google Fonts)
- Compiled CSS lives at `static/css/main.css` — rebuild after changing `assets/css/main.css`

### Image Processing

Hugo's built-in image pipeline:
- Thumbnails: `Fill "600x400 q85 Lanczos"`
- Full-size gallery: `Fit "1600x1200 q90 Lanczos"`
- All images use lazy loading

### External Dependencies (CDN)

- GLightbox CSS/JS for photo lightbox galleries
- Google Fonts (Inter)
