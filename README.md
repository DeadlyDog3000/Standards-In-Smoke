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

### Beta 3.9 — 2026-04-14
- **Balance**: Unit production costs and building costs now scale with city count — each additional city raises all production and event resource costs by 20% (2 cities = 1.2×, 3 = 1.4×, etc.), discouraging pure city-spam and resource hoarding
- **Balance**: Event gold/resource costs follow the same scaling — paying for events gets more expensive as your empire grows

### Beta 3.8 — 2026-04-14
- **Feature**: All 11 tile improvements now render as pixel art sprites instead of emoji icons: Farm, Market, Mine, Quarry, Steel Mill, Urban, Lumbermill, Barn, Port, Pasture, Science Lab, Treasury
- **Fix**: Grass tile variants updated — plains now use Grass and Grass_Plants sprites

### Beta 3.7 — 2026-04-13
- **Feature**: Idle city popup — appears at end of turn for any city not producing; click a unit/building to assign production, or open the full city panel
- **Feature**: No research popup — appears when no tech is being researched; browse available techs by section with cost and turn estimate, or open the full tech tree
- Both reminders chain (idle cities first, then research), dismiss with ESC or "Later", and reappear next turn if still unresolved

### Beta 3.6 — 2026-04-13
- **Feature**: New cities start with a free worker unit — no longer stranded with a bare capital
- **Feature**: Orders exhausted popup — a centred overlay appears when you use your last order, prompting you to end your turn
- **Fix**: Tech research sound now plays reliably on completion — was silently failing due to cloneNode not loading audio data

### Beta 3.5 — 2026-04-13
- **Feature**: Noble Families system — every nation now has 2–4 historic noble houses (Habsburgs, Bonapartes, Romanovs, Hohenzollerns, etc.) with individual opinion scores (0–100); families with low opinion become Restless → Angry and eventually spawn scaled rebellions near the capital
- **Feature**: Noble Families replace the old per-city discontent system entirely — `city.discontent` and `triggerRebellion` removed; rebellions now emerge from noble politics, not mob unhappiness
- **Feature**: Family opinion is affected by legitimacy, treasury gold, buildings (Granary, Fortifications, Grand Cathedral), events, and city capture; Court panel shows opinion bars, status labels, and an Appease button (30g → +15 opinion)
- **Feature**: Event system overhauled — 31 events expanded to 120 with conditional triggers; events now check game state before appearing (coastal city, mountain/forest/river tiles owned, at war, at peace, gold level, legitimacy, current season, tech researched, buildings, city count, turn number, family opinion, character existence)
- **Feature**: 89 new events across 15 categories — Coastal, Mountain, Forest, River, War, Peace, High/Low Gold, High/Low Legitimacy, Many Cities, Tech-gated, Building-gated, Season, Early/Late game, Family politics, Flavour
- **Feature**: Characters can now die from events — 4 events carry `charDeath` outcomes (Death of a General, Plague in the Palace, Assassination Attempt, Duel of Honour) killing heirs, spouses, or random courtiers; family opinion takes a hit on each death
- **Fix**: Rebel nation creation no longer calls `initNationFamilies` / `initNationCharacters`, stopping orphaned characters and families accumulating in memory after each rebellion

### Beta 3.3 — 2026-04-13
- **Scrapped**: Premade map ideas scrapped for now — nation selection screen, preset geographic city positions, world map terrain overrides, tribal nations system, and World (600×360) map size all removed
- Nations and their historical city name pools are retained; nations now spawn at random positions on procedurally generated maps (same as before Beta 2.8)
- Default map size changed back to Large (200×130)

### Beta 3.2 — 2026-04-13
- **Fix**: `tribeAI` combat was broken — `doAttack` was called with a unit object instead of coordinates; also used Manhattan distance instead of proper hex adjacency (`hexNeighbors`) matching all other combat code
- **Fix**: `checkElimination` now skips tribe nations (same as barbarians) — tribes with no cities were incorrectly triggering conqueror logic and resource transfers
- **Fix**: `getMaxOrders` now returns unlimited orders for tribes (same as barbarians) — tribes never use the order system
- **Fix**: Tribal capital names now deduplicate against existing city names before use — prevents duplicate city names if a preset nation already founded a same-named city

### Beta 3.1 — 2026-04-13
- **Fix**: Great Britain and Ireland now reliably spawn as islands fully separate from continental Europe — terrain override carves a wide ocean box (lon −12 to 2) then punches the islands back in; continental Europe is stamped starting at lon 2.5 guaranteeing a 4-tile ocean gap; Irish Sea carved between Ireland and Britain; `findLandNear` for French/Belgian cities always resolves to the continent before it can reach the British island

### Beta 3.0 — 2026-04-13
- **Feature**: World map — all 21 nations now placed at historically accurate world-scale coordinates (formula: xFrac = (lon+180)/360, yFrac = (80-lat)/140); new World (600×360) map size added and set as default
- **Feature**: 22 tribal/non-state peoples — Iroquois Confederacy, Cherokee Nation, Sioux Nation, Comanche, Maya, Andean Tribes, Mapuche, Guaraní, Ashanti Empire, Oyo Empire, Zulu Kingdom, Kingdom of Kongo, Ethiopian Empire, Tuareg Confederacy, Qing China, Japanese Shogunate, Maratha Confederacy, Qajar Persia, Kazakh Khanate, Hawaiian Kingdom, Maori Confederation, Aboriginal Australia — each spawned at a historically proportional world position with a settlement and 3 tribal warriors
- **Feature**: Tribal nation diplomacy — tribes start **neutral** (not at war); discover them by sight; open Kingdoms panel to **Send Envoy** (costs 20g, establishes peace) or **Declare War**; tribes defend their settlement but never expand; shown in a dedicated "Tribal Nations" section in the Kingdoms panel
- **Feature**: New `tribal_warrior` unit (5 ATK, 10 HP, 4 moves, 🏹) used by all tribal peoples
- **Feature**: Barbarians still spawn independently from tribes as before

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
