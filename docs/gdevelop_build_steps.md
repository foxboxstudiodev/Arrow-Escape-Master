# Arrow Escape Master — GDevelop Build Steps

This document defines the exact practical build steps for creating **Arrow Escape Master** in GDevelop.

The goal is to build the first playable prototype in the correct order.

---

## 1. Create the Project

Open GDevelop and create a new empty project.

Project settings:

```text
Project name: ArrowEscapeMaster
Game name: Arrow Escape Master
Orientation: Portrait
Base resolution: 720 x 1280
Platform target: Android
Package name: com.foxboxstudio.arrowescapemaster
```

Recommended window size:

```text
Width: 720
Height: 1280
```

---

## 2. Create Scenes

Create these scenes in this exact order:

```text
BootScene
MainMenu
LevelSelect
GameScene
Settings
```

For the first prototype, only these scenes are required:

```text
MainMenu
GameScene
```

Win and Lose screens should be created as layers inside `GameScene`, not as separate scenes.

---

## 3. Create Global Variables

In GDevelop, open project variables and create:

```text
CurrentLevel = 1
UnlockedLevel = 1
Coins = 0
SoundEnabled = 1
VibrationEnabled = 1
AdsRemoved = 0
```

Use numeric booleans:

```text
1 = true
0 = false
```

This is simpler in GDevelop events.

---

## 4. Create GameScene Variables

Inside `GameScene`, create scene variables:

```text
LevelID = 1
MistakeLimit = 3
Mistakes = 0
Moves = 0
ArrowsRemaining = 0
LevelCompleted = 0
LevelFailed = 0
InputLocked = 0
BoardStartX = 72
BoardStartY = 220
CellSize = 96
BoardWidth = 6
BoardHeight = 8
```

---

## 5. Create Layers in GameScene

Inside `GameScene`, create layers:

```text
BaseLayer
UILayer
WinLayer
LoseLayer
PauseLayer
```

Initial visibility:

```text
BaseLayer = visible
UILayer = visible
WinLayer = hidden
LoseLayer = hidden
PauseLayer = hidden
```

---

## 6. Create Main Objects

### 6.1 Arrow

Object type:

```text
Sprite
```

Object name:

```text
Arrow
```

Object size:

```text
96 x 96
```

Animations:

```text
0 = ArrowUp
1 = ArrowRight
2 = ArrowDown
3 = ArrowLeft
```

Object variables:

```text
ArrowID = 0
GridX = 0
GridY = 0
Direction = up
Color = none
Locked = 0
KeyID = 0
IsMoving = 0
IsRemoved = 0
```

Direction animation mapping:

```text
up    -> animation 0
right -> animation 1
down  -> animation 2
left  -> animation 3
```

---

### 6.2 Blocker

Object type:

```text
Sprite
```

Object name:

```text
Blocker
```

Object size:

```text
96 x 96
```

Object variables:

```text
BlockerID = 0
GridX = 0
GridY = 0
Type = stone
```

---

### 6.3 BoardCellDebug

Object type:

```text
Sprite or Shape Painter
```

Purpose:

Use only during development to visually see the board grid.

Final release:

```text
Delete or hide this object
```

---

### 6.4 UI Objects

Create these objects:

```text
LevelText
MistakeText
MoveText
CoinText
RestartButton
HintButton
UndoButton
MenuButton
```

Use Text objects for labels and Sprite/Button objects for buttons.

---

### 6.5 Win Layer Objects

Create on `WinLayer`:

```text
WinPanel
WinText
NextButton
ReplayButton
CoinRewardText
```

---

### 6.6 Lose Layer Objects

Create on `LoseLayer`:

```text
LosePanel
LoseText
RestartLoseButton
ExtraChanceButton
```

---

## 7. Position Formula

All grid objects must be placed with this formula:

```text
Object.X = BoardStartX + GridX * CellSize
Object.Y = BoardStartY + GridY * CellSize
```

Example:

```text
GridX = 2
GridY = 4
BoardStartX = 72
BoardStartY = 220
CellSize = 96

X = 72 + 2 * 96 = 264
Y = 220 + 4 * 96 = 604
```

---

## 8. First Manual Level

Before loading JSON, create Level 1 manually.

Spawn one arrow:

```text
ArrowID = 1
GridX = 2
GridY = 4
Direction = up
```

Position:

```text
X = 264
Y = 604
```

Scene variable:

```text
ArrowsRemaining = 1
```

This confirms that input and movement work before JSON loading is added.

---

## 9. Core Event Logic

### 9.1 Scene Start

GDevelop event:

```text
Condition:
  At the beginning of the scene

Actions:
  Set Mistakes = 0
  Set Moves = 0
  Set LevelCompleted = 0
  Set LevelFailed = 0
  Set InputLocked = 0
  Hide WinLayer
  Hide LoseLayer
  Spawn test level arrows
  Update UI text
```

---

### 9.2 Tap Arrow

GDevelop event:

```text
Conditions:
  Cursor/touch is on Arrow
  Mouse button released OR touch released
  Scene variable InputLocked = 0
  Arrow variable IsMoving = 0
  Arrow variable IsRemoved = 0

Actions:
  Check arrow path
```

In the first prototype, use separate events for each direction:

```text
If Arrow.Direction = up
If Arrow.Direction = right
If Arrow.Direction = down
If Arrow.Direction = left
```

---

## 10. Path Checking Logic

For MVP, use grid logic.

An arrow can escape if there is no arrow or blocker in front of it before the board edge.

### 10.1 Up Direction

For an arrow at:

```text
GridX = x
GridY = y
Direction = up
```

Check every cell:

```text
(x, y - 1)
(x, y - 2)
...
(x, 0)
```

If no blocker or arrow exists in those cells:

```text
Path is clear
```

If at least one object exists:

```text
Path is blocked
```

---

### 10.2 Right Direction

Check:

```text
(x + 1, y)
(x + 2, y)
...
(BoardWidth - 1, y)
```

---

### 10.3 Down Direction

Check:

```text
(x, y + 1)
(x, y + 2)
...
(x, BoardHeight - 1)
```

---

### 10.4 Left Direction

Check:

```text
(x - 1, y)
(x - 2, y)
...
(0, y)
```

---

## 11. Practical First Version Path Check

Because GDevelop visual events do not work like a normal programming loop, the first version should use a simple collision ray object.

Create object:

```text
PathChecker
```

Type:

```text
Sprite or Shape Painter
```

Visibility:

```text
Hidden
```

When an arrow is tapped:

1. Place `PathChecker` in front of the arrow.
2. Stretch it until the board edge in the arrow direction.
3. Check collision between `PathChecker` and `Arrow` / `Blocker`.
4. If collision exists, fail move.
5. If no collision exists, move arrow out.

This is faster to build in GDevelop than a full JSON grid parser.

---

## 12. Successful Move Events

If path is clear:

```text
Set Arrow.IsMoving = 1
Add 1 to Moves
Move Arrow in Direction
```

Movement target:

```text
up    -> Y = -150
right -> X = 870
down  -> Y = 1430
left  -> X = -150
```

When arrow is outside screen:

```text
Delete Arrow
Subtract 1 from ArrowsRemaining
Set Arrow.IsRemoved = 1
Check win condition
```

Recommended movement speed:

```text
900 pixels per second
```

---

## 13. Failed Move Events

If path is blocked:

```text
Add 1 to Moves
Add 1 to Mistakes
Shake arrow slightly
Play fail sound later
Update UI
Check lose condition
```

Shake effect for prototype:

```text
Move Arrow 8 px left
Wait 0.05 sec
Move Arrow 16 px right
Wait 0.05 sec
Move Arrow 8 px left
```

Later this can be replaced with a Tween behavior.

---

## 14. Win Condition

GDevelop event:

```text
Conditions:
  ArrowsRemaining <= 0
  LevelCompleted = 0

Actions:
  Set LevelCompleted = 1
  Set InputLocked = 1
  Add reward coins
  Unlock next level
  Save progress
  Show WinLayer
```

---

## 15. Lose Condition

GDevelop event:

```text
Conditions:
  Mistakes >= MistakeLimit
  LevelFailed = 0
  LevelCompleted = 0

Actions:
  Set LevelFailed = 1
  Set InputLocked = 1
  Show LoseLayer
```

---

## 16. Restart Button

GDevelop event:

```text
Condition:
  Cursor/touch is on RestartButton
  Mouse button released OR touch released

Action:
  Restart scene
```

Same logic applies to:

```text
RestartLoseButton
ReplayButton
```

---

## 17. Next Button

GDevelop event:

```text
Condition:
  Cursor/touch is on NextButton
  Mouse button released OR touch released

Actions:
  Add 1 to GlobalVariable(CurrentLevel)
  Change scene to GameScene
```

For MVP:

```text
If CurrentLevel > 10:
  Go to MainMenu or show ComingSoon
```

---

## 18. Save Progress

Use GDevelop storage.

On level win:

```text
If CurrentLevel >= UnlockedLevel:
  Set UnlockedLevel = CurrentLevel + 1

Write UnlockedLevel to storage
Write Coins to storage
```

At game start:

```text
Read UnlockedLevel from storage
Read Coins from storage
```

---

## 19. Development Order

Build in this strict order:

```text
1. MainMenu scene
2. GameScene scene
3. One arrow manual test
4. Tap arrow detection
5. Direction-based movement
6. PathChecker object
7. Blocked-path fail logic
8. Win condition
9. Lose condition
10. Restart and next buttons
11. Add 10 levels manually or through JSON
12. Add level select
13. Add coin/hint placeholders
14. Add ads later
```

---

## 20. Important Rule

Do not start with ads, skins, store screenshots, or advanced gates.

First objective:

```text
One playable level that works perfectly.
```

Only after that, expand to levels and UI.
