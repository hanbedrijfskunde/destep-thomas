# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Static website presenting a strategic DESTEP (Demografisch, Economisch, Sociaal, Technologisch, Ecologisch, Politiek) and OT (Opportunities/Threats) analysis for **Kegro Deuren B.V.**, a Dutch door manufacturer. Content is in Dutch.

## Architecture

- **No build system, package manager, or test framework** — pure static HTML
- Single page (`index.html`) with two switchable views and all CSS/JS inline:
  - **"Huidige Analyse"** — Current-state DESTEP analysis (6 dimensions: D, E, S, T, Eco, P) with SWOT/OT summary
  - **"Toekomst 2031"** — Forward-looking horizon analysis (4 dimensions: D, E, S, T) with Evidence section and LKI dashboard
- CDN dependencies loaded via `<script>`/`<link>` tags:
  - **Tailwind CSS** (CDN runtime) with custom `kegro` color theme inline
  - **Chart.js** for data visualizations (bar, line, radar, doughnut charts)
  - **Google Fonts** (Inter)

## Development

Open `index.html` directly in a browser — no server required.

## Key Patterns

- **View switching**: A `switchView('current'|'future')` JS function toggles between `#view-current` and `#view-future` containers, updates the header subtitle, footer text, and toggle button states
- **Chart lifecycle**: Charts use a factory pattern (`chartFactories.current.*` / `chartFactories.future.*`). On view switch, all active charts are destroyed and new ones created via `requestAnimationFrame` to ensure correct canvas sizing
- `splitLabel()` helper wraps long chart labels at 16 characters
- Custom CSS classes (`opportunity-box`, `threat-box`, `lki-card`, `probability-bar`, `chart-container`) are defined in a `<style>` block
- Each DESTEP dimension follows a consistent layout: letter indicator, heading, chart/visual, and opportunity/threat cards
