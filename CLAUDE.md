# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal portfolio website for Bertin Balouki SIMYELI (Quant Developer & Systems Engineer). Single-page static site — no build system, no package manager, no dependencies.

## Development

To preview locally, open `portfolio.html` directly in a browser. No server or build step is required. For live-reload development, any static file server works:

```powershell
# Python (if available)
python -m http.server 8080

# Or open directly
start portfolio.html
```

Deployment is any static host (GitHub Pages, Netlify, Vercel, etc.).

## Architecture: Single-File SPA

`portfolio.html` is the entire codebase (~66KB). All CSS and JS are inline:

- **`<style>` (~1365 lines)** — CSS custom properties for theming (`--bg`, `--text`, `--blue`, `--red`, `--surface`), then section-by-section styles. Responsive breakpoints at `<900px` and `<600px`.
- **`<body>`** — Six `<section>` elements by ID: `hero`, `about`, `experience`, `projects`, `writing`, `contact`, plus a fixed `<nav>` and `<footer>`.
- **`<script>` (~50 lines)** — Three behaviors: Intersection Observer for scroll-reveal animations (`.reveal` class), smooth anchor scroll for nav links, and a `mailto:` handler for the contact form.

## Key Patterns

- **Scroll animations**: Elements get class `reveal` in HTML; the Intersection Observer adds `visible` on entry, triggering a CSS `rise` keyframe. New animated elements need both classes and the `--delay` CSS variable for staggered timing.
- **Dark theme tokens**: Colors are defined as CSS variables at `:root` — always use variables rather than hardcoded hex values.
- **Grid layouts**: Project cards and article cards use `grid-template-columns: repeat(auto-fill, minmax(..., 1fr))` — adjust the `minmax` minimum to control minimum card width.
- **Typography**: Headings use `Bricolage Grotesque`, body uses `Instrument Serif`, code/terminal uses `JetBrains Mono` — all loaded from Google Fonts in `<head>`.
