# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A GitHub Pages static site at gutoceolin.github.io — a study hub for Brazilian law school notes (3rd semester, UFN 2026/1). Pure HTML/CSS/vanilla JS with no build tooling, package manager, or dependencies.

## Development

**No build step.** Edit HTML files directly and open them in a browser. The site is published automatically by GitHub Pages from the `main` branch.

To preview: open any `.html` file directly in a browser, or use a simple local server:
```
python -m http.server
```

## Architecture

**[index.html](index.html)** is the main hub. It renders a filterable card grid linking to all content pages. Cards are filtered by discipline using vanilla JS (~40 lines). Adding a new topic requires adding a card `<div>` in the grid section.

**Content pages** (e.g., [civil-pessoa-natural-nascituro-capacidade.html](civil-pessoa-natural-nascituro-capacidade.html)) are fully self-contained — each embeds its own `<style>` and `<script>` tags. Pages use a tabbed module system with a search input that highlights matching content.

All CSS and JS is inline inside each HTML file. There are no separate `.css` or `.js` source files.

## Design System

**Dark theme** using CSS custom properties. Discipline colors defined at the top of each file:

| Discipline | CSS Variable | Color |
|---|---|---|
| Civil | `--civil` | `#e06e8c` (pink) |
| Constitutional | `--const` | `#7b8fe8` (blue) |
| Procedural | `--proc` | `#5cb8e0` (cyan) |
| Penal | `--penal` | `#e07a5c` (orange) |
| ECA | `--eca` | `#5cc98a` (green) |
| Accent | `--gold` | `#d4a843` |

Fonts loaded from Google Fonts: Cormorant Garamond (headings), Outfit (body), JetBrains Mono (code/labels).

## Adding New Content

1. Create a new HTML file following the naming pattern `{discipline}-{topic}.html`
2. Copy the structure from an existing content page — the full template (header, module tabs, search, footer) is embedded in each file
3. Add a card entry to the grid in [index.html](index.html) with the correct `data-discipline` attribute for filtering

## Language

All content is in Brazilian Portuguese (`lang="pt-BR"`). UI text, comments, and commit messages are in Portuguese.
