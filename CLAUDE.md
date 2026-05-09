# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal portfolio website for Bertin Balouki SIMYELI (Quant Developer · Systems Engineer · AI Engineer). Single-page static site — no build system, no package manager, no dependencies.

## Development

To preview locally, open `portfolio.html` directly in a browser. No server or build step is required. For live-reload development, any static file server works:

```powershell
# Python (if available)
python -m http.server 8080

# Or open directly
start portfolio.html
```

Deployment is any static host (GitHub Pages, Netlify, Vercel, etc.). See `DEPLOYMENT.md` for step-by-step instructions.

## Architecture: Single-File SPA

`portfolio.html` is the entire codebase (~115KB, 3194 lines). All CSS and JS are inline:

- **`<style>` (~2137 lines, lines 17–2154)** — CSS custom properties for theming at `:root`, then section-by-section styles. Responsive breakpoints at `<900px` and `<600px`.
- **`<body>`** — Eight `<section>` elements by ID: `hero`, `about`, `ai`, `experience`, `education`, `projects`, `writing`, `contact`, plus a fixed `<nav id="nav">`, a `<footer>`, and a floating `.chat-widget` (WhatsApp + Telegram buttons).
- **`<script>` (~30 lines)** — Four behaviors: Intersection Observer for scroll-reveal animations (`.reveal` class), smooth anchor scroll for nav links, a `mailto:` handler (`sendMsg()`) for the contact form, and a scroll listener that darkens the nav border on scroll.

## Key Patterns

- **Scroll animations**: Elements get class `reveal` in HTML; the Intersection Observer adds `in` (not `visible`) on entry. New animated elements need the `reveal` class; staggered timing uses the `--delay` CSS variable.
- **Dark theme tokens**: Colors are defined as CSS variables at `:root` — always use variables rather than hardcoded hex values. Current palette:
  - Backgrounds: `--bg`, `--bg-subtle`, `--bg-inset`, `--bg-overlay`
  - Borders: `--border`, `--border-subtle`
  - Text: `--text`, `--text-2`, `--text-3`
  - Accent: `--blue`, `--blue-l`, `--blue-d`, `--red`, `--red-d`, `--green`, `--orange`, `--purple`, `--pink`, `--white`
  - Misc: `--r` (border-radius base, 4px)
- **Typography variables**: `--sans` (Bricolage Grotesque), `--serif` (Instrument Serif), `--mono` (JetBrains Mono) — all loaded from Google Fonts in `<head>`. Always reference via variable, not font name directly.
- **Grid layouts**: Project cards use `minmax(350px, 1fr)`, education cards use `minmax(290px, 1fr)` — adjust the `minmax` minimum to control card width.
- **Featured project card**: `.rc.feat` spans `grid-column: 1/-1` with a two-column internal layout and a blue→red gradient top border.
- **Chat widget**: The `.chat-widget` div (WhatsApp + Telegram) lives outside `<footer>`, fixed-positioned. Phone number: `+1 773 345 3491`, Telegram: `@bbalouki`.
