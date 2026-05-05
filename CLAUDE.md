# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository shape

Single-file static marketing site for **volta.codes**, a German-language custom-software/AI consultancy based in Berlin. The entire site lives in [index.html](index.html) — HTML, CSS (inline `<style>`), and JavaScript (inline `<script>`) in one document. No build step, no package manager, no tests, not a git repository.

To preview: open `index.html` directly in a browser, or serve the directory with `python3 -m http.server`.

## Page sections

The page consists of five sections in order: `.hero`, `.warum`, `.pakete`, `.team`, `.kontakt`. Each (except hero) uses the `.split` layout.

## Architecture notes

- **Layout primitive: `.split`** — a two-column grid (`var(--left-col) 1fr`) used by every content section. The left column holds a sticky `.s-head` section heading; the right column (`.col` or similar) holds body copy. On mobile (`max-width: 768px`) it collapses to one column and the heading un-stickies. When adding a section, follow this pattern rather than inventing a new one.
- **Dark sections drive nav color.** `.pakete` and `.kontakt` have dark backgrounds; an `IntersectionObserver` toggles `nav.nav-dark` when either is in view. The selector is `const darkSections = document.querySelectorAll('.pakete, .kontakt')` — if you add another dark section, add it there.
- **Scroll-triggered effects.** Three observers at the bottom of the file: (1) `fade` (threshold 0.15) → adds `.visible` for the fade-in-up entry animation; (2) `mark` (threshold 0.8) → adds `.lit` to animate the blue highlight sweep across `<mark>` elements; (3) the nav-dark observer above. The hero `.fade` is pre-activated via `document.querySelector('.hero .fade').classList.add('visible')` so it shows on load without waiting for scroll. Any new animated element must use one of these existing classes — don't add parallel observer logic.
- **Nav scroll state.** `nav.scrolled` is toggled when `scrollY > 40`, applying a frosted-glass background. On dark sections, `nav.scrolled.nav-dark` switches it to a dark variant.
- **Design tokens live in `:root`** — colors, `--left-col` (240px desktop / 0px mobile), `--col-gap` (4rem desktop / 0rem mobile). Change tokens there rather than hard-coding values in rules.

## Design tokens

Key values from `:root`:

| Token | Value |
|---|---|
| `--white` | `#fafaf8` |
| `--dark` | `#14141a` |
| `--text` | `#3a3a3e` |
| `--text-mid` | `#48484c` |
| `--text-light` | `#70706e` |
| `--blue` | `#2b5ae0` |
| `--blue-bg` | `#2350c8` (`.pakete` background) |

Font: **Space Grotesk** (Google Fonts), weights 300/400/500/600.

## Content conventions

- All user-facing copy is **German**. Preserve umlauts (ä/ö/ü/ß) and match the existing tone: sober, confident, no marketing fluff.
- Contact email: `hallo@volta.codes`. Address: Emserstr. 125, 12051 Berlin. Footer year: 2026.
