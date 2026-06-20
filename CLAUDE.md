# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What this project is

A Japanese-language static website for RAI, an HPB (Hot Pepper Beauty) consultant targeting beauty salon owners. It delivers free educational content and tools to improve salon listings on the HPB booking platform. There is no build system, no package manager, and no framework — everything is plain HTML/CSS/JavaScript opened directly in a browser.

## Previewing changes

Open any `.html` file directly in a browser, or serve the root directory over HTTP:

```sh
python3 -m http.server 8080
```

There are no build, lint, or test commands.

## Site structure and content groups

The repository contains two distinct brand contexts:

**RAI brand (10-gift series) — current main content**
- `index.html` — hub page listing all 10 gifts, links to `01.html`–`10.html`
- `01.html`–`10.html` — individual gift content pages
- `lp.html` — SEO landing page driving LINE registrations
- `line-lp.html` — LINE-specific landing page
- `minimo-guide.html` — standalone guide for the Minimo booking platform

**Salon Result Lab brand (older 7-gift series)**
- `7gifts.html` — hub page for the 7-gift bundle
- `gifts/01-hpb-checklist.html` – `gifts/07-counseling-sheet.html` — individual older gift pages
- `blog-auto.html` — service landing page for HPB blog/photo automation

**Tools (standalone, self-contained)**
- `hpb-report-analyzer/index.html` — drag-and-drop HPB report analyzer; embeds `marked.min.js` from CDN
- `threads-post-analyzer/index.html` — paste-in Threads post analyzer (see `threads-post-analyzer/README.md` for column spec and metric formulas)
- `threads-daily-posts/YYYY-MM-DD/index.html` — archived daily Threads post batches

## CSS themes and which files use them

| Stylesheet | Background | Accent | Used by |
|---|---|---|---|
| `style-light.css` | White/`#F8F9FA` | Gold `#C9932A` | `index.html`, `01–10.html`, `lp.html`, `line-lp.html` |
| `style.css` | Dark `#07090c` | Gold `#c9a84c` | `minimo-guide.html` (dark premium theme) |
| `gifts/gift-style.css` | Cream `#FFFAF5` | Orange `#FF8C42` | All files in `gifts/` |
| Embedded `<style>` | Varies | — | `7gifts.html`, `blog-auto.html`, `line-lp.html`, both tool pages, daily posts |

When adding a new page that belongs to the RAI 10-gift series, link `style-light.css` and follow the patterns in `01.html`–`10.html`. When adding a Salon Result Lab page, embed styles inline or link `gifts/gift-style.css`.

## Shared patterns across pages

**Fonts**: `Noto Sans JP` (body) + `Bebas Neue` (display/numbers). Both are loaded from Google Fonts. The `.bebas` utility class applies Bebas Neue.

**Layout container**: `.wrap` (max-width ~860–960 px, centered with `padding: 0 20px`). Some pages also use `.wrap--narrow` (max-width 680 px).

**Scroll-reveal animation**: Elements with class `.reveal` start hidden (`opacity:0; transform:translateY(20px)`) and animate in when they enter the viewport. Activate by attaching an `IntersectionObserver` and adding `.in-view` — see the inline `<script>` at the bottom of `index.html` for the canonical implementation.

**Gold gradient text**: `.g-text` applies a linear-gradient clip to text. In `style-light.css` this renders as a solid gold color; in `style.css` it renders as an animated gradient.

**Page header (content pages)**: Sticky, with a back-button (`.back-btn`) on the left and a breadcrumb/pager on the right. See `01.html` for the standard markup.

**CTA (call-to-action)**: All pages end with a LINE registration button (`.btn-line`). The LINE SVG logo inline is the standard icon pattern used across the site.

## Adding a new gift content page (01–10 pattern)

1. Copy an existing content page (e.g., `01.html`) as a starting point.
2. Update the `<title>`, page-hero text, and the `header-pager__num` (e.g., `11 / 11`).
3. Add a link card to `index.html`'s `.gifts-grid` following the existing `.gift-card` markup.
4. No CSS changes needed if content fits within existing component styles.

## Tool pages

Both tool pages (`hpb-report-analyzer/`, `threads-post-analyzer/`) are fully self-contained single-file apps with embedded CSS and JS. They do not share stylesheets or scripts with the rest of the site. The Threads analyzer README documents the expected TSV column order and how engagement metrics are computed.
