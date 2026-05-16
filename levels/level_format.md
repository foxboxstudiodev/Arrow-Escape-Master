# Arrow Escape Master — Level Format

This document defines the level data structure for **Arrow Escape Master**.

The level system must be simple enough for GDevelop but structured enough to support many levels later.

---

## 1. Design Decision

The game uses a **grid-based level system**.

This is the correct approach because Arrow Escape Master is a puzzle game. Physics-based logic can create unstable results, while grid-based logic gives deterministic and testable levels.

---

## 2. Board Settings

Default MVP board:

```text
BoardWidth = 6
BoardHeight = 8
CellSize = 96
```

Grid coordinates start from the top-left cell.

```text
X = 0 to 5
Y = 0 to 7
```

Example:

```text
Top-left cell:     x=0, y=0
Top-right cell:    x=5, y=0
Bottom-left cell:  x=0, y=7
Bottom-right cell: x=5, y=7
```

---

## 3. Coordinate Rules

Every gameplay object uses grid coordinates.

```json
{
  "x": 2,
  "y": 4
}
```

This means:

```text
Column 2
Row 4
```

GDevelop position formula:

```text
ObjectX = BoardStartX + x * CellSize
ObjectY = BoardStartY + y * CellSize
```

Recommended values:

```text
BoardStartX = 72
BoardStartY = 220
CellSize = 96
```

---

## 4. Direction Values

Allowed arrow directions:

```text
up
right
 down
left
```

Important: use lowercase in JSON.

Correct:

```json
"direction": "up"
```

Wrong:

```json
"direction": "UP"
```

---

## 5. Basic Level Object

Each level must contain:

```json
{
  "id": 1,
  "name": "Level 1",
  "difficulty": "easy",
  "board": {
    "width": 6,
    "height": 8
  },
  "mistakeLimit": 3,
  "moveLimit": null,
  "rewardCoins": 10,
  "arrows": [],
  "blockers": [],
  "gates": [],
  "portals": []
}
```

---

## 6. Arrow Format

Normal arrow:

```json
{
  "id": 1,
  "x": 2,
  "y": 3,
  "direction": "up",
  "color": "none",
  "locked": false,
  "keyId": null
}
```

Fields:

```text
id        = unique arrow ID inside level
x         = grid column
y         = grid row
direction = up / right / down / left
color     = none / red / blue / green / yellow
locked    = true / false
keyId     = required key ID if locked, otherwise null
```

---

## 7. Blocker Format

Blockers are static obstacles.

```json
{
  "id": 1,
  "x": 3,
  "y": 3,
  "type": "stone"
}
```

Allowed blocker types:

```text
stone
wood
metal
```

---

## 8. Gate Format

Gates are used in later phases.

```json
{
  "id": 1,
  "x": 4,
  "y": 2,
  "type": "lock",
  "color": "red",
  "locked": true,
  "keyId": 1
}
```

Allowed gate types:

```text
lock
color
```

---

## 9. Portal Format

Portals are later-phase mechanics.

```json
{
  "id": 1,
  "x": 1,
  "y": 2,
  "pairId": 2
}
```

Each portal must have a pair.

---

## 10. Full Example Level

```json
{
  "id": 1,
  "name": "First Escape",
  "difficulty": "easy",
  "board": {
    "width": 6,
    "height": 8
  },
  "mistakeLimit": 3,
  "moveLimit": null,
  "rewardCoins": 10,
  "arrows": [
    {
      "id": 1,
      "x": 2,
      "y": 3,
      "direction": "up",
      "color": "none",
      "locked": false,
      "keyId": null
    },
    {
      "id": 2,
      "x": 3,
      "y": 3,
      "direction": "right",
      "color": "none",
      "locked": false,
      "keyId": null
    }
  ],
  "blockers": [],
  "gates": [],
  "portals": []
}
```

---

## 11. Solvability Rule

Every level must have at least one valid solution path.

Bad level design:

```text
All arrows block each other permanently.
No first legal move exists.
```

Good level design:

```text
At least one arrow can escape immediately.
Each escaped arrow opens a path for another arrow.
The level can be completed with logical ordering.
```

---

## 12. Difficulty Rules

### Easy

```text
2–8 arrows
0–2 blockers
No gates
No portals
Mistake limit: 3
```

### Normal

```text
8–16 arrows
2–5 blockers
Simple locks allowed
Mistake limit: 3
```

### Hard

```text
16–28 arrows
5+ blockers
Locks, color gates, and portals allowed
Mistake limit: 2 or 3
```

---

## 13. MVP Level Requirement

First MVP requires 50 levels:

```text
Level 1–10: tutorial/easy
Level 11–30: normal
Level 31–50: hard but fair
```

---

## 14. Level Validation Checklist

Before adding a level to the game, check:

- [ ] Level has valid ID
- [ ] All arrows have unique IDs
- [ ] All objects are inside board bounds
- [ ] No two objects occupy the same cell unless intentionally allowed
- [ ] Direction values are valid
- [ ] At least one first move is possible
- [ ] Level can be solved fully
- [ ] Mistake limit is not too harsh
- [ ] Level difficulty matches its position

---

## 15. Implementation Note for GDevelop

GDevelop can load JSON data, but for the first MVP, levels may also be created manually inside the scene if JSON loading becomes too slow to implement.

Final target remains JSON-driven levels.

Correct development order:

1. Manually create 1 playable level.
2. Confirm movement and collision logic.
3. Add simple level data format.
4. Load levels from JSON.
5. Build 50 levels.
