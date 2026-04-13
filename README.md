# Standards In Smoke

A browser-based hex tile strategy game inspired by Civilization. Build cities, train units, research technologies, and expand your empire across a procedurally generated map.

## How to Play

Open `index.html` in a browser. No build step or server required.

- **Pan**: Click and drag, or WASD / arrow keys
- **Zoom**: Mouse wheel
- **Select**: Click on units or cities
- **Move units**: Select a unit, click the Move button, then click a destination
- **Found cities**: Move a Settler unit and use the Found City action
- **Build improvements**: Use a Worker unit on owned tiles
- **Buy tiles**: Expand city borders by purchasing adjacent tiles

## Features

- Procedurally generated hex maps with terrain types: plains, forest, mountain, swamp, ocean, and more
- City management with production queues
- Unit combat, movement, and fog of war
- Tech tree for unlocking new units and improvements
- AI opponents with diplomacy
- Resource system: gold, food, wood, stone, steel, science
- Save/load support via local storage
- Background music and sound effects

## Tech Stack

Single-file HTML/JS/CSS application using Canvas 2D rendering. Hex tile sprites from a flat-top isometric tile pack.

## Changelog

### Beta 2.9 — 2026-04-13
- **Feature**: 7 additional playable nations — Ottoman Empire, United States, Bavaria, Duchy of Nassau, Swiss Confederation, Denmark-Norway, Westphalia; total roster now 21 nations, up to 20 AI opponents
- **Feature**: All newly founded cities use historically accurate names drawn from each nation's real territory — each nation has a deep pool of 12–24 period-appropriate city names; AI settlers also use historical names; falls back to procedural generation only when all names are exhausted
- **Fix**: Renamed Britain → Great Britain, Holland → Kingdom of Holland, Italy → Kingdom of Italy

### Beta 2.8 — 2026-04-13
- **Feature**: 14 preset historical Napoleonic nations replace random kingdoms — Great Britain, Austria, France, Russia, Belgium, Kingdom of Holland, Spain, Sweden, Portugal, Kingdom of Italy, Duchy of Warsaw, Kingdom of Naples, Kingdom of Saxony, Prussia; each with assigned banner colour
- **Feature**: Nation selection screen — pick which nation to play from an illustrated card grid before starting a campaign; up to 13 AI opponents from the same roster
- **Feature**: Each nation starts with historically accurate capital and 1–2 secondary cities pre-founded at geographically proportional positions on the map
- **Feature**: Civilization borders are now rounded — territory edges use quadratic bezier curves at corners where adjacent border edges meet, plus a soft semi-transparent territory colour fill on all owned tiles

### Beta 2.7 — 2026-04-13
- **Feature**: Tech tree is now a full-screen visual graph — nodes arranged by prereq depth with bezier arrows, section colour-coding, click to research, hover tooltips, ESC to close
- **Feature**: Lancer unit (8 ATK, 10 HP, 7 moves) — ZOC Pierce hits the primary target for 100% damage and the unit directly behind it for 25%
- **Feature**: Heavy Cavalry unit (13 ATK, 14 HP, 5 moves) — highest ATK of any cavalry
- **Feature**: Upgrade path: cavalry → hussar → lancer → heavy cavalry; new techs Lancer Tactics and Heavy Cavalry
- **Fix**: City ambient SFX volume reduced to near-inaudible background level

### Beta 2.6 (patch 2) — 2026-04-13
- **Feature**: Tech unlock now plays a 14-second bang sound effect with a 16-beam golden god-ray animation bursting from the banner for the first 4 seconds

### Beta 2.6 (patch 1) — 2026-04-13
- **Fix**: Black screen flash when issuing a go-to order — unit now animates from its original tile instead of snapping to destination on the first frame
- **Fix**: Unit invisible/unselectable after go-to — camera now follows the unit each turn it advances along its route
- **Fix**: Go-to movement cost ignored terrain penalties (forest, mountain, river etc.) — now uses the same cost function as manual moves
- **Fix**: Camera jolted when cycling to next unit — now pans smoothly instead of snapping

### Beta 2.6 — prior
- Lakes and mountains added to map generation; improved rivers
- Bug fixes, balance tweaks, faster season progression

### Beta 2.5
- Napoleonic warfare overhaul: morale, formations, generals, seasons, dynasty system
- Swordsman Charge ability: move and attack in the same turn (disabled in Square formation)
