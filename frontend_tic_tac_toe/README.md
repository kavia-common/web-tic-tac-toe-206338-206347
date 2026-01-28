# Tic Tac Toe (React) — Application Flow

This repository contains a React single-page application (SPA). The overall work item describes a Tic Tac Toe game, but the current implementation in this container is a lightweight React template that demonstrates theme toggling (light/dark) and a sample Create React App landing UI. This README documents the flow that is currently implemented in the code.

## What the app does right now

When you run the app, you will see:

A centered page with a theme toggle button in the top-right, a React logo, a short instruction to edit `src/App.js`, the current theme label, and a link to the React documentation. There is no Tic Tac Toe board, turn logic, winner/draw detection, or reset functionality implemented in the current code.

## Application flow (runtime)

### 1) Page load and bootstrapping

The application starts at:

- `src/index.js`, which creates the React root and renders `<App />` into the DOM element with id `root`.

The DOM root element is defined in:

- `public/index.html` (`<div id="root"></div>`)

### 2) Main component and state

The main UI is implemented in:

- `src/App.js`

`App` is a functional component that maintains a single piece of state:

- `theme` (string): defaults to `"light"` and can be toggled to `"dark"`.

### 3) Theme application side-effect

`App` uses a `useEffect` hook to apply the selected theme to the global document:

- On initial mount and whenever `theme` changes, the effect sets an attribute on the document root:
  - `document.documentElement.setAttribute('data-theme', theme)`

This is the core mechanism that drives theming throughout the page.

### 4) Styling and theming

The CSS theme variables and styles live in:

- `src/App.css`

The CSS defines:

- Light theme variables under `:root`
- Dark theme overrides under `[data-theme="dark"]`

Because the React effect sets `data-theme` on the `<html>` element, the CSS selector `[data-theme="dark"]` activates when the theme is dark, changing background and text colors accordingly.

### 5) User interaction: toggling the theme

In the UI, the user clicks the theme toggle button (`.theme-toggle`).

- Clicking the button calls `toggleTheme`, which flips `theme` from `"light"` to `"dark"` (or vice versa).
- Updating `theme` causes a re-render.
- The `useEffect` runs again and updates `data-theme` on the document.
- CSS variables switch, and the page transitions to the new theme.

The button uses an `aria-label` to improve accessibility by describing the action (switching to the opposite theme).

## How the Tic Tac Toe flow would be expected to work (not yet implemented)

The work item describes a Tic Tac Toe game with a centered 3x3 board, a status display above, and action buttons (such as Reset) below. At present, none of this behavior exists in `src/App.js`. Once implemented, a typical flow would include:

- Maintaining game state (board squares, current player, winner/draw state).
- Handling square clicks to place `X`/`O`.
- Preventing moves after a win/draw.
- Calculating and displaying status text (next player, winner, or draw).
- Resetting the game state on Reset.

If/when the game UI replaces the template UI, this README should be updated to reflect the actual implemented components and state transitions.

## Local development

From `web-tic-tac-toe-206338-206347/frontend_tic_tac_toe`:

### Start the dev server

```bash
npm start
```

Then open:

- http://localhost:3000

### Run tests

```bash
npm test
```

### Build

```bash
npm run build
```

## Key files

- `src/index.js`: React entry point; mounts `<App />`.
- `src/App.js`: Main component; holds `theme` state and toggle logic.
- `src/App.css`: Theme variables and component styles.
- `public/index.html`: HTML template with the `root` mounting element.
