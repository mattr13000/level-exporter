# Map Baker (.glb to .json)

Extracts collision data and POIs (Points of Interest) from a `.glb` scene into a static JSON matrix for client-side A* pathfinding and server-side validation.

## GLB Data Contract (Blender Setup)

To parse any `.glb` file correctly, the 3D scene must strictly adhere to the following setup:

*   **Grid Tiles (Terrain/Obstacles):** 
    Every mesh acting as a grid node must contain a Custom Property named `walkable`.
    *   `walkable: 0` -> Floor / Path
    *   `walkable: 1` -> Wall / Obstacle
*   **Player Spawn:** 
    An Empty object named exactly `SPAWN_player`.
*   **Monster Spawns:** 
    Empty objects containing the string `SPAWN_monster`.
*   **Zone Triggers (Exits):** 
    Empty objects named `trigger_<target_name>` (e.g., an empty named `trigger_dungeon` exports the target value `"dungeon"`).

## Usage

1. Open `index.html` in a browser (no local server required).
2. Select your `.glb` file.
3. Verify the parsed grid preview (🟦 Player, 🟩 Trigger, 🟥 Monster, ⬛ Wall, ⬜ Floor).
4. Download the generated `map.json` and place it in your shared data folder.

## Output Structure
```json
{
  "name": "level_01",
  "width": 20,
  "height": 20,
  "offsetX": -10,
  "offsetZ": -10,
  "matrix": [
    [1, 1, 1, 1],
    [1, 0, 0, 1],
    [1, 0, 1, 1]
  ],
  "spawn_player": { "x": 0, "z": 0 },
  "spawn_monsters": [
    { "x": 5, "z": 2 },
    { "x": -3, "z": 4 }
  ],
  "triggers": [
    { "target": "dungeon", "x": 9, "z": 9 }
  ]
}