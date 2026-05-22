# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

A static web application for playing "Расписной покер" (Raspishnoy Poker) — a Russian card game variant. No build step, no backend, no package manager.

## Running Locally

```powershell
# From the public_html directory
python -m http.server 8000
# Then open http://localhost:8000
```

Alternatively use any static file server (Node's `http-server`, PHP's built-in server, etc.).

## Tech Stack

- **Vue.js 3** — loaded via CDN (`https://unpkg.com/vue@3`), no npm build
- **Bootstrap 5.3.3** — local copy in `public_html/assets/css/` and `public_html/assets/js/`
- **Font Awesome 4.7.0** — local copy in `public_html/assets/font-awesome-4.7.0/`
- **vuedraggable / Sortable.js** — loaded via CDN for drag-and-drop

All dependencies are either CDN-loaded or bundled locally. There is no `package.json` or build toolchain.

## Architecture

The entire application lives in `public_html/index.html` as a single-file Vue 3 app using the Options API with `Vue.createApp({...})`. There are no `.vue` single-file components, no router, and no state management library.

Game flow is controlled by a `phase` variable:
- `phase === 'setup'` — configure players, rules, and game blocks
- `phase === 'game'` — active play (bid entry → trick reporting → score calculation)
- `phase === 'results'` — final scores and winner

Drag-and-drop block reordering uses `vuedraggable` wrapping `v-model` on the blocks array.

## Deployment

The project deploys to `poker.it-cosmos.ru` via PhpStorm's built-in deployment sync. The `public_html/` directory maps directly to the server web root. No CI/CD pipeline exists.
