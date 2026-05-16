# Arrow Escape Master — First Prototype Tasks

This document defines the exact task list for building the first playable prototype of **Arrow Escape Master** in GDevelop.

The first prototype has one goal:

```text
One playable level where the player can tap arrows, clear paths, make mistakes, win, lose, restart, and continue.
```

Do not add ads, skins, store screenshots, or advanced mechanics before this prototype works.

---

## 1. Prototype Scope

The first prototype includes:

```text
MainMenu
GameScene
One manual test level
Arrow object
Blocker object
PathChecker object
Tap input
Arrow movement
Blocked path detection
Mistake counter
Win condition
Lose condition
Restart button
Next button placeholder
```

The first prototype does not include:

```text
AdMob
Real level JSON loading
Store build
Skins
Portals
Locks
Color gates
Daily rewards
In-app purchases
```

---

## 2. Task Group A — Create GDevelop Project

- [ ] Open GDevelop
- [ ] Create new empty project
- [ ] Set project name to `ArrowEscapeMaster`
- [ ] Set game name to `Arrow Escape Master`
- [ ] Set orientation to portrait
- [ ] Set base resolution to `720 x 1280`
- [ ] Set package name to `com.foxboxstudio.arrowescapemaster`
- [ ] Save project file as `gdevelop/ArrowEscapeMaster.json`

Result:

```text
A clean GDevelop project exists and is saved inside the repository structure.
```

---

## 3. Task Group B — Create Scenes

Create these scenes:

- [ ] `MainMenu`
- [ ] `GameScene`

Optional later:

- [ ] `BootScene`
- [ ] `LevelSelect`
- [ ] `Settings`

For the first prototype, only `MainMenu` and `GameScene` are mandatory.

---

## 4. Task Group C — MainMenu Prototype

Create objects in `MainMenu`:

- [ ] `GameTitleText`
- [ ] `PlayButton`
- [ ] `Background`

Required behavior:

- [ ] Tapping `PlayButton` changes scene to `GameScene`

Text:

```text
GameTitleText = Arrow Escape Master
PlayButton = PLAY
```

Result:

```text
Player can open the game and press Play to enter GameScene.
```

---

## 5. Task Group D — GameScene Variables

Create these scene variables inside `GameScene`:

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
BoardRightEdge = 648
BoardBottomEdge = 988
MoveSpeed = 900
PathBlocked = 0
```

Checklist:

- [ ] All variables are created
- [ ] Numeric values are entered correctly
- [ ] Variable names exactly match this document

---

## 6. Task Group E — Create GameScene Layers

Create layers:

- [ ] `BaseLayer`
- [ ] `UILayer`
- [ ] `WinLayer`
- [ ] `LoseLayer`

Initial state:

```text
BaseLayer = visible
UILayer = visible
WinLayer = hidden
LoseLayer = hidden
```

---

## 7. Task Group F — Create Core Objects

Create these objects:

### Arrow

- [ ] Object type: Sprite
- [ ] Object name: `Arrow`
- [ ] Size: `96 x 96`
- [ ] Animation 0: ArrowUp
- [ ] Animation 1: ArrowRight
- [ ] Animation 2: ArrowDown
- [ ] Animation 3: ArrowLeft

Object variables:

```text
ArrowID = 0
GridX = 0
GridY = 0
Direction = up
IsMoving = 0
IsRemoved = 0
```

### Blocker

- [ ] Object type: Sprite
- [ ] Object name: `Blocker`
- [ ] Size: `96 x 96`

Object variables:

```text
BlockerID = 0
GridX = 0
GridY = 0
Type = stone
```

### PathChecker

- [ ] Object type: Sprite or Shape Painter
- [ ] Object name: `PathChecker`
- [ ] Hidden during gameplay
- [ ] Used only for path collision checks

### BoardBackground

- [ ] Object type: Sprite or Tiled Sprite
- [ ] Object name: `BoardBackground`
- [ ] Position: `X=72`, `Y=220`
- [ ] Size: `576 x 768`

---

## 8. Task Group G — Create UI Objects

Create these objects on `UILayer`:

- [ ] `LevelText`
- [ ] `MistakeText`
- [ ] `MoveText`
- [ ] `RestartButton`

Optional for first prototype:

- [ ] `CoinText`
- [ ] `HintButton`
- [ ] `UndoButton`

Recommended text positions:

```text
LevelText:   x=40,  y=40
MistakeText: x=40,  y=100
MoveText:    x=500, y=100
RestartButton: x=40, y=1120
```

---

## 9. Task Group H — Create WinLayer Objects

Create on `WinLayer`:

- [ ] `WinPanel`
- [ ] `WinText`
- [ ] `NextButton`
- [ ] `ReplayButton`

Text:

```text
WinText = LEVEL COMPLETE
NextButton = NEXT
ReplayButton = REPLAY
```

Initial state:

```text
WinLayer hidden
```

---

## 10. Task Group I — Create LoseLayer Objects

Create on `LoseLayer`:

- [ ] `LosePanel`
- [ ] `LoseText`
- [ ] `RestartLoseButton`

Text:

```text
LoseText = LEVEL FAILED
RestartLoseButton = RESTART
```

Initial state:

```text
LoseLayer hidden
```

---

## 11. Task Group J — Manual Test Level

Create the first test level manually in `GameScene`.

At scene start:

```text
Set Mistakes = 0
Set Moves = 0
Set ArrowsRemaining = 1
Set LevelCompleted = 0
Set LevelFailed = 0
Set InputLocked = 0
Hide WinLayer
Hide LoseLayer
Create Arrow at x=264, y=604
Set Arrow.GridX = 2
Set Arrow.GridY = 4
Set Arrow.Direction = up
Set Arrow.ArrowID = 1
Set Arrow.IsMoving = 0
Set Arrow.IsRemoved = 0
Set Arrow animation = 0
```

Position formula:

```text
X = BoardStartX + GridX * CellSize = 72 + 2 * 96 = 264
Y = BoardStartY + GridY * CellSize = 220 + 4 * 96 = 604
```

Result:

```text
One up arrow appears on the board.
```

---

## 12. Task Group K — Arrow Tap Event

Create event:

Conditions:

```text
Cursor/touch is on Arrow
Mouse button released or touch released
InputLocked = 0
Arrow.IsMoving = 0
Arrow.IsRemoved = 0
LevelCompleted = 0
LevelFailed = 0
```

Actions:

```text
Set SelectedArrowID = Arrow.ArrowID
Run path check based on Arrow.Direction
```

For first prototype, create separate sub-events for:

```text
Direction = up
Direction = right
Direction = down
Direction = left
```

---

## 13. Task Group L — PathChecker Setup

Create path check for each direction.

### Up

```text
PathChecker.X = Arrow.X
PathChecker.Y = BoardStartY
PathChecker.Width = CellSize
PathChecker.Height = Arrow.Y - BoardStartY
```

### Right

```text
PathChecker.X = Arrow.X + CellSize
PathChecker.Y = Arrow.Y
PathChecker.Width = BoardRightEdge - (Arrow.X + CellSize)
PathChecker.Height = CellSize
```

### Down

```text
PathChecker.X = Arrow.X
PathChecker.Y = Arrow.Y + CellSize
PathChecker.Width = CellSize
PathChecker.Height = BoardBottomEdge - (Arrow.Y + CellSize)
```

### Left

```text
PathChecker.X = BoardStartX
PathChecker.Y = Arrow.Y
PathChecker.Width = Arrow.X - BoardStartX
PathChecker.Height = CellSize
```

After placing PathChecker:

```text
If PathChecker collides with another Arrow or Blocker:
  PathBlocked = 1
Else:
  PathBlocked = 0
```

---

## 14. Task Group M — Successful Move Logic

If `PathBlocked = 0`:

```text
Set Arrow.IsMoving = 1
Set InputLocked = 1
Add 1 to Moves
Update UI
```

Arrow movement events:

```text
If Arrow.Direction = up and Arrow.IsMoving = 1:
  Arrow.Y -= MoveSpeed * TimeDelta()

If Arrow.Direction = right and Arrow.IsMoving = 1:
  Arrow.X += MoveSpeed * TimeDelta()

If Arrow.Direction = down and Arrow.IsMoving = 1:
  Arrow.Y += MoveSpeed * TimeDelta()

If Arrow.Direction = left and Arrow.IsMoving = 1:
  Arrow.X -= MoveSpeed * TimeDelta()
```

Delete arrow when outside screen:

```text
up:    Arrow.Y < -120
right: Arrow.X > 840
down:  Arrow.Y > 1400
left:  Arrow.X < -120
```

Actions after delete:

```text
Delete Arrow
Subtract 1 from ArrowsRemaining
Set InputLocked = 0
Check win condition
```

---

## 15. Task Group N — Failed Move Logic

If `PathBlocked = 1`:

```text
Add 1 to Moves
Add 1 to Mistakes
Update UI
Play fail feedback later
Check lose condition
```

Fail feedback for first prototype:

```text
Temporarily change Arrow color/tint
or shake with Tween behavior
```

---

## 16. Task Group O — Win Condition

Create event:

Conditions:

```text
ArrowsRemaining <= 0
LevelCompleted = 0
LevelFailed = 0
```

Actions:

```text
Set LevelCompleted = 1
Set InputLocked = 1
Show WinLayer
```

Result:

```text
When the last arrow exits, LEVEL COMPLETE appears.
```

---

## 17. Task Group P — Lose Condition

Create event:

Conditions:

```text
Mistakes >= MistakeLimit
LevelCompleted = 0
LevelFailed = 0
```

Actions:

```text
Set LevelFailed = 1
Set InputLocked = 1
Show LoseLayer
```

Result:

```text
After 3 failed taps, LEVEL FAILED appears.
```

---

## 18. Task Group Q — Restart Logic

Events:

```text
Tap RestartButton → Restart GameScene
Tap RestartLoseButton → Restart GameScene
Tap ReplayButton → Restart GameScene
```

Result:

```text
Level resets cleanly.
```

---

## 19. Task Group R — Next Button Placeholder

For first prototype:

```text
Tap NextButton → Restart GameScene
```

Later:

```text
CurrentLevel += 1
Load next level
```

---

## 20. Task Group S — Prototype Acceptance Test

The first prototype is accepted only when all checks pass:

- [ ] MainMenu opens
- [ ] Play button opens GameScene
- [ ] One arrow appears on board
- [ ] Tapping clear arrow moves it upward
- [ ] Arrow leaves screen
- [ ] Arrow is deleted
- [ ] WinLayer appears
- [ ] Restart works
- [ ] Blocker can block arrow path
- [ ] Blocked move increases mistake count
- [ ] LoseLayer appears after 3 mistakes
- [ ] UI updates correctly
- [ ] No crash during restart

---

## 21. Development Rule

Do not continue to level loading or monetization until the first prototype passes the acceptance test.

Correct next step after acceptance:

```text
Build 10-level prototype using levels/levels.json structure.
```
