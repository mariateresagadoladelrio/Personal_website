# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A single-page personal portfolio website for Teresa Gadola (marketing professional). The entire site lives in one file: `index.html`, which contains all CSS, HTML, and JavaScript inline — no build step, no package manager, no external dependencies beyond Google Fonts.

To preview: open `index.html` directly in a browser. There is no dev server or build process.

## Architecture

Everything is in `index.html`, structured in this order:
1. `<head>` — Google Fonts imports + all CSS in a single `<style>` block
2. `<body>` — Six sections (`#hero`, `#about`, `#experience`, `#education`, `#skills`, `#contact`) + `<footer>`
3. `<script>` — Three behaviours: scroll-reveal via IntersectionObserver, smooth anchor scroll, parallax on hero emoji-nav items, and contact form fake success state (no backend — form submission is purely visual)

## Design System

All visual tokens are CSS custom properties defined in `:root`:

- **Colors:** `--blush`, `--blush-light`, `--blush-deep`, `--cream`, `--cream-warm`, `--taupe`, `--taupe-dark`, `--charcoal`, `--charcoal-mid`, `--gold`, `--gold-light`, `--white`
- **Fonts:** `--serif` (Playfair Display), `--sans` (DM Sans), `--script` (Dancing Script)
- **Shadows:** `--s1` (subtle), `--s2` (medium), `--s3` (strong)

Always use these tokens rather than raw values when adding new styles.

## Reveal Animation Pattern

Elements animate in on scroll via the `.reveal` class + IntersectionObserver. Add `.d1`–`.d4` for staggered delays (0.1s–0.4s each step). The observer adds `.visible` when the element enters the viewport.

```html
<div class="reveal d2">...</div>
```

## Responsive Breakpoints

- `920px` — collapses `about-grid` and `contact-grid` from two-column to single-column; hides `.obj-camera`
- `640px` — hides `.obj-ring` and `.obj-flower`; reduces hero font size; collapses timeline `.t-head` to column layout; reduces section padding

## Hero Navigation

Six floating emoji anchors (`.nav-obj`) are absolutely positioned inside `.nav-float` and link to page sections via `href="#section-id"`. They use CSS `@keyframes drift` for idle floating and get parallax offset applied via the scroll listener in JS. Each object class (`.obj-bag`, `.obj-ring`, `.obj-flower`, `.obj-sunnies`, `.obj-camera`, `.obj-env`) sets its own position and animation timing.

## Section Backgrounds

- `#hero` — `var(--blush)` with radial glows and SVG paper grain texture
- `#about` — `var(--cream)`
- `#experience` — `var(--cream-warm)` with a top gradient stripe
- `#education` — `var(--cream)`
- `#skills` — `var(--cream-warm)`
- `#contact` — `var(--blush)` with radial glow
- `footer` — `var(--charcoal)`

## Local Assets

Images and files in the project root (referenced directly by filename in `index.html`):

- `self_image.jpeg` — profile photo used in `#about`
- `red_cross.jpg`, `rec_cross_image.jpg`, `red_cross_logo.png` — Red Cross experience assets
- `logo_friesland.png`, `Inditex_logo_black.svg` — company logos
- `magazine_debic.png`, `website_debic.png`, `inspiration_debic.png`, `debic_main.png` — Debic project visuals
- `graduation_picture.jpeg`, `graduation_picture_with_friend.JPG`, `thesis.png` — education section assets
- `CV_TeresaGadola.pdf` — downloadable CV linked in the contact/hero section

`index copy.html` is a backup of the main file — do not edit it; only modify `index.html`.
