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

### Beta 2.6 (patch) — 2026-04-13
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
