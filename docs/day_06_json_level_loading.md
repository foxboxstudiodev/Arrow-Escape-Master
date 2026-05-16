# Arrow Escape Master — Day 06 JSON Level Loading

This document defines Day 06 tasks for **Arrow Escape Master** in GDevelop.

Day 06 goal:

```text
Move from manual level creation toward structured level loading using the levels/levels.json format.
```

Important: GDevelop visual events can work with JSON, but the first implementation must stay simple and testable. Do not over-engineer this step.

---

## 1. Required Before Day 06

Day 05 must already be complete:

- [ ] LevelSelect scene exists
- [ ] CurrentLevel works
- [ ] UnlockedLevel works
- [ ] Progress saves locally
- [ ] Level buttons open selected levels
- [ ] NextButton opens the next level
- [ ] Manual levels 1–10 can be loaded or are planned
- [ ] Multi-arrow gameplay works
- [ ] PathChecker works
- [ ] Win/Lose logic works

Do not start JSON loading if manual levels are still unstable.

---

## 2. Day 06 Scope

Day 06 includes:

```text
Use levels/levels.json as the official level source
Define how level data maps to GDevelop objects
Create loading logic for arrows
Create loading logic for blockers
Set level variables from level data
Validate loaded level data
Keep fallback manual loading if needed
```

Day 06 does not include:

```text
AdMob
Coins final balancing
Hints final AI
Undo state history
Skins
Portals
Locks
Color gates
Store release
```

---

## 3. Current Level Data File

Official level file:

```text
levels/levels.json
```

It contains:

```text
version
game
boardDefaults
levels[]
```

Each level contains:

```text
id
name
difficulty
board
mistakeLimit
moveLimit
rewardCoins
arrows[]
blockers[]
gates[]
portals[]
```

---

## 4. Development Decision

Use this practical order:

```text
1. Keep manual level loading as fallback
2. Add level data parsing for one level first
3. Load arrows from data
4. Load blockers from data
5. Test Level 1 only
6. Test Levels 1–10
7. Remove or disable manual loading only after JSON loading is stable
```

Do not delete manual loading immediately.

---

## 5. Data Mapping — Level Fields

Map level data to scene variables:

| JSON Field | GDevelop Variable |
|---|---|
| `id` | `LevelID` |
| `mistakeLimit` | `MistakeLimit` |
| `rewardCoins` | `RewardCoins` |
| `board.width` | `BoardWidth` |
| `board.height` | `BoardHeight` |

Derived values:

```text
BoardRightEdge = BoardStartX + BoardWidth * CellSize
BoardBottomEdge = BoardStartY + BoardHeight * CellSize
ArrowsRemaining = number of arrows in selected level
```

---

## 6. Data Mapping — Arrow Fields

Each JSON arrow:

```json
{
  "id": 1,
  "x": 2,
  "y": 4,
  "direction": "up",
  "color": "none",
  "locked": false,
  "keyId": null
}
```

Maps to GDevelop object `Arrow`:

```text
Arrow.ArrowID = id
Arrow.GridX = x
Arrow.GridY = y
Arrow.Direction = direction
Arrow.Color = color
Arrow.Locked = locked
Arrow.KeyID = keyId
Arrow.IsMoving = 0
Arrow.IsRemoved = 0
```

Position formula:

```text
Arrow.X = BoardStartX + x * CellSize
Arrow.Y = BoardStartY + y * CellSize
```

Animation mapping:

```text
up    → animation 0
right → animation 1
down  → animation 2
left  → animation 3
```

---

## 7. Data Mapping — Blocker Fields

Each JSON blocker:

```json
{
  "id": 1,
  "x": 0,
  "y": 0,
  "type": "stone"
}
```

Maps to GDevelop object `Blocker`:

```text
Blocker.BlockerID = id
Blocker.GridX = x
Blocker.GridY = y
Blocker.Type = type
```

Position formula:

```text
Blocker.X = BoardStartX + x * CellSize
Blocker.Y = BoardStartY + y * CellSize
```

---

## 8. Recommended GDevelop Loading Approach

GDevelop can read JSON/text data, but the exact implementation depends on the project setup and available extensions.

Recommended implementation path:

```text
Option A — Start with manual level groups matching levels.json
Option B — Use GDevelop JSON extension to parse levels.json
Option C — Convert levels.json into GDevelop-friendly arrays/structures if needed
```

Most stable approach for first prototype:

```text
Start with Option A, then migrate to Option B.
```

Reason:

```text
Gameplay logic is more important than early automation.
```

---

## 9. Option A — Manual Groups Mirroring JSON

Create one event group per level:

```text
LoadLevel01
LoadLevel02
LoadLevel03
LoadLevel04
LoadLevel05
LoadLevel06
LoadLevel07
LoadLevel08
LoadLevel09
LoadLevel10
```

Each group must match the `levels/levels.json` data exactly.

Example:

```text
If CurrentLevel = 1:
  Delete all Arrow and Blocker objects
  Set LevelID = 1
  Set MistakeLimit = 3
  Set RewardCoins = 10
  Set ArrowsRemaining = 1
  Create Arrow at grid (2,4), direction up
```

This gives stable gameplay while JSON parsing is prepared.

---

## 10. Option B — Real JSON Loading Target

Final target:

```text
At scene start:
  Load levels/levels.json
  Find level where id = CurrentLevel
  Read board settings
  Loop through arrows[]
  Create Arrow objects
  Loop through blockers[]
  Create Blocker objects
  Set ArrowsRemaining
```

High-level pseudo-flow:

```text
LoadLevel(CurrentLevel)
↓
Find selected level
↓
Apply level variables
↓
Create arrows
↓
Create blockers
↓
Update UI
```

---

## 11. Level Loading Function Design

Even if GDevelop uses visual events, think of the logic like functions:

```text
ResetLevelState()
LoadLevelData(levelId)
CreateArrowFromData(arrowData)
CreateBlockerFromData(blockerData)
UpdateUI()
```

This keeps the event sheet clean.

---

## 12. ResetLevelState

Before loading any level:

```text
Delete all Arrow objects
Delete all Blocker objects
Delete or reset PathChecker
Set Mistakes = 0
Set Moves = 0
Set ArrowsRemaining = 0
Set LevelCompleted = 0
Set LevelFailed = 0
Set InputLocked = 0
Set PathBlocked = 0
Hide WinLayer
Hide LoseLayer
```

This prevents old level objects from staying on screen.

---

## 13. LoadLevelData

Load selected level using:

```text
CurrentLevel
```

Then set:

```text
LevelID
MistakeLimit
RewardCoins
BoardWidth
BoardHeight
BoardRightEdge
BoardBottomEdge
```

If selected level is missing:

```text
Go to LevelSelect
or show Coming Soon
```

Do not crash if a level is missing.

---

## 14. CreateArrowFromData

For every arrow in selected level:

```text
Create Arrow
Set ArrowID
Set GridX
Set GridY
Set Direction
Set Color
Set Locked
Set KeyID
Set IsMoving = 0
Set IsRemoved = 0
Set position by grid formula
Set animation by direction
Add 1 to ArrowsRemaining
```

---

## 15. CreateBlockerFromData

For every blocker in selected level:

```text
Create Blocker
Set BlockerID
Set GridX
Set GridY
Set Type
Set position by grid formula
Set animation/appearance by Type
```

---

## 16. Level Validation Before Spawn

Before creating objects, validate:

```text
Level exists
Board width > 0
Board height > 0
Arrows list is not empty
Every arrow has id, x, y, direction
Every direction is valid
Every object is inside board bounds
No duplicate ArrowID
No invalid blocker position
```

If invalid:

```text
Show error in debug build
Return to LevelSelect in production
```

---

## 17. Board Bounds Validation

Valid object coordinates:

```text
x >= 0
x < BoardWidth
y >= 0
y < BoardHeight
```

For default board:

```text
x = 0 to 5
y = 0 to 7
```

---

## 18. Direction Validation

Allowed values:

```text
up
right
down
left
```

Invalid values must not spawn broken arrows.

---

## 19. Duplicate Cell Validation

Two solid objects should not occupy the same grid cell.

Invalid example:

```text
Arrow at (2,4)
Blocker at (2,4)
```

Allowed later only if a mechanic specifically supports it.

For MVP:

```text
No duplicate cells.
```

---

## 20. JSON Level Test Plan

Test in this order:

```text
1. Load Level 1 only
2. Load Level 2 only
3. Load Level 3 with multiple arrows
4. Load Level 5 with blockers
5. Load Level 10 with more objects
6. Move through LevelSelect from 1 to 10
```

Do not test all levels at once first.

---

## 21. Fallback Rule

If JSON loading causes too many technical issues in GDevelop:

```text
Keep manual event-group loading for MVP
Use levels.json as design reference
Move JSON loading to post-MVP update
```

This is acceptable because the priority is shipping a stable game.

---

## 22. Common Problems

### Problem: Level loads but no arrows appear

Check:

```text
Selected level ID
Arrow array path
Create object action
BoardStartX / BoardStartY
Grid position formula
Layer placement
```

---

### Problem: Arrows appear in wrong positions

Check:

```text
GridX and GridY mapping
CellSize
BoardStartX
BoardStartY
Using x/y from JSON correctly
```

---

### Problem: Direction animation is wrong

Check:

```text
Direction string lowercase
Animation mapping
Arrow animation IDs
```

---

### Problem: Win appears immediately

Check:

```text
ArrowsRemaining is set after spawning arrows
ArrowsRemaining is not left at 0
Win condition does not run before loading finishes
Use InputLocked or LoadingLevel flag if needed
```

---

### Problem: Old arrows remain after next level

Check:

```text
Delete all Arrow objects before loading new level
Delete all Blocker objects before loading new level
Reset PathChecker
```

---

## 23. Day 06 Acceptance Test

Day 06 is complete only when all checks pass:

- [ ] Level loading flow is documented in project events
- [ ] Manual fallback remains available
- [ ] Level 1 can be loaded from structured data or mirrored event group
- [ ] Level 2 can be loaded correctly
- [ ] Level 3 multi-arrow layout works
- [ ] Level 5 blocker layout works
- [ ] ArrowsRemaining is correct after load
- [ ] MistakeLimit is correct after load
- [ ] RewardCoins is correct after load if used
- [ ] All spawned objects are inside board
- [ ] Direction animations match direction values
- [ ] Restart reloads the same level correctly
- [ ] NextButton loads the next level correctly
- [ ] No old objects remain after changing levels

---

## 24. After Day 06

Next file to follow:

```text
docs/day_07_coins_hints_rewards.md
```

Day 07 goal:

```text
Add coin rewards, hint placeholder, and reward balancing for the first playable MVP.
```

---

## 25. Critical Rule

Do not let JSON loading break the working prototype.

Stable manual loading is better than broken automated loading.
