# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Pickup Queue is a mobile-first web app for managing fair basketball pickup game rotations (5v5, 10 players per game). It's a zero-dependency, single-file app — all HTML, CSS, and JavaScript live in `index.html`.

## Development

No build tools, package manager, or dev server required. Open `index.html` directly in a browser. There are no tests, linters, or CI pipelines.

## Architecture

Everything is in **`index.html`** — a single self-contained file with inline `<style>` and `<script>` blocks:

- **State management**: A global `state` object holds all app state (players, game status, timer, history). State persists via `localStorage` under the key `pickup-queue-state`. The `saveState()` function serializes a subset of state (excluding timer runtime) to localStorage.
- **Rendering**: The `render()` function rebuilds the entire DOM by constructing an HTML string and setting `innerHTML` on `#app`. There is no virtual DOM or framework — call `render()` after any state mutation.
- **Timer**: Uses `setInterval` with a 1-second tick. `renderTimer()` is a targeted update that only touches the timer display element (avoids full re-render every second).
- **Player priority**: `getPriority(p)` computes queue position using a weighted formula: `gamesSatOut * 1000000 - gamesPlayed * 1000 - arrivalOrder`. Manual reordering overrides this via `queueOrder`.
- **Transfer system**: Export/import uses base64-encoded JSON (`btoa`/`atob`) with compressed property names (`n`, `a`, `s`, `g` for name, arrivalOrder, gamesSatOut, gamesPlayed).

## Key Constants

```javascript
const PLAYERS_PER_GAME = 10;
const GAME_DURATION = 16 * 60; // seconds
```

## Conventions

- HTML escaping uses `esc()` which creates a temporary DOM element — use it for all user-supplied text in rendered HTML.
- Player IDs are `Date.now()` timestamps — not guaranteed unique if adding players in rapid succession.
- "Remove" sets `player.active = false` (soft delete); "Return" reactivates with reset stats.
- Swap/reorder modes use `assignManualOrder()` to snapshot current priority order into explicit `queueOrder` values before modifying positions.
- `queueOrder` is reset to `null` for all players when a game ends, restoring automatic priority sorting.