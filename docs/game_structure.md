# Arrow Escape Master — Game Structure

This document defines the practical GDevelop structure for **Arrow Escape Master**.

The goal is to build a clean first version without unnecessary complexity. The first playable build must prove the core gameplay: tap arrows, move them in the correct direction, detect blocked paths, remove arrows, and complete the level.

---

## 1. Project Setup

### Project Name

```text
ArrowEscapeMaster
```

### Game Name

```text
Arrow Escape Master
```

### Package Name

```text
com.foxboxstudio.arrowescapemaster
```

### Target Platform

```text
Android first
```

### Orientation

```text
Portrait
```

### Recommended Base Resolution

```text
720 x 1280
```

### Game Type

```text
2D puzzle / offline / mobile casual
```

---

## 2. Scene List

### 2.1 BootScene

Purpose:

- Initialize global variables.
- Load player progress.
- Prepare first launch state.
- Go to MainMenu.

Objects:

- `LoadingText`
- `Logo`

Main logic:

```text
At scene start:
  Load progress from storage
  Load coin count
  Load sound/vibration settings
  Change scene to MainMenu
```

---

### 2.2 MainMenu

Purpose:

- Entry screen.
- Player can start game, open level select, settings, or remove ads placeholder.

Objects:

- `GameTitleText`
- `PlayButton`
- `LevelSelectButton`
- `SettingsButton`
- `RemoveAdsButton`
- `CoinText`
- `Background`

Main logic:

```text
Tap PlayButton:
  Load latest unlocked level
  Change scene to GameScene

Tap LevelSelectButton:
  Change scene to LevelSelect

Tap SettingsButton:
  Change scene to Settings
```

---

### 2.3 LevelSelect

Purpose:

- Show levels.
- Let player replay completed levels.
- Lock levels not yet unlocked.

Objects:

- `LevelButton`
- `BackButton`
- `LevelStarIcon`
- `LockedIcon`

Main logic:

```text
For each level button:
  If level <= unlocked level:
    enable button
  Else:
    show locked state

Tap unlocked level:
  Set GlobalVariable(CurrentLevel)
  Change scene to GameScene
```

---

### 2.4 GameScene

Purpose:

Main gameplay scene.

Objects:

- `Arrow`
- `Wall`
- `Blocker`
- `ExitArea`
- `KeyArrow`
- `LockGate`
- `ColorGate`
- `PortalIn`
- `PortalOut`
- `LevelText`
- `MistakeText`
- `MoveText`
- `HintButton`
- `UndoButton`
- `RestartButton`
- `PauseButton`
- `CoinText`
- `BoardBackground`

Main logic:

```text
At scene start:
  Load current level data
  Spawn arrows and blockers
  Reset moves
  Reset mistakes
  Reset level state

Tap Arrow:
  Check if arrow is allowed to move
  Check if path is clear
  If path is clear:
    Move arrow out
    Remove arrow
    Add move count
    Check win condition
  Else:
    Add mistake count
    Play fail feedback
    Check lose condition
```

---

### 2.5 WinPopup

In GDevelop this can be either a separate scene or a layer inside GameScene. For MVP, use a layer.

Objects:

- `WinPanel`
- `WinText`
- `NextButton`
- `ReplayButton`
- `CoinRewardText`

Main logic:

```text
When all arrows are removed:
  Show WinLayer
  Add coins
  Save progress
  Unlock next level
```

---

### 2.6 LosePopup

Use a layer inside GameScene for MVP.

Objects:

- `LosePanel`
- `LoseText`
- `RestartButton`
- `ExtraChanceButton`

Main logic:

```text
When mistake limit is reached:
  Show LoseLayer
  Stop arrow input

Tap RestartButton:
  Reload current level

Tap ExtraChanceButton:
  Show rewarded ad placeholder
  Add one extra mistake chance
```

---

### 2.7 Settings

Purpose:

- Sound on/off.
- Vibration on/off.
- Privacy policy button.
- Back button.

Objects:

- `SoundToggle`
- `VibrationToggle`
- `PrivacyPolicyButton`
- `BackButton`

---

## 3. Core Object Definitions

### 3.1 Arrow

Main gameplay object.

Object type:

```text
Sprite
```

Required object variables:

```text
Direction = "Up" | "Down" | "Left" | "Right"
ArrowID = number
Color = "None" | "Red" | "Blue" | "Green" | "Yellow"
IsLocked = false
NeedsKey = false
IsMoving = false
IsRemoved = false
```

Required animations:

```text
0 = ArrowUp
1 = ArrowDown
2 = ArrowLeft
3 = ArrowRight
```

Recommended size:

```text
96 x 96 px
```

---

### 3.2 Wall

Static object that blocks arrows.

Object type:

```text
Sprite or Tiled Sprite
```

Behavior:

```text
Obstacle
```

---

### 3.3 Blocker

A normal static obstacle used inside levels.

Object variables:

```text
BlockerID = number
Type = "Stone" | "Wood" | "Metal"
```

---

### 3.4 ExitArea

Invisible boundary or escape zone.

Object type:

```text
Sprite
```

Visibility:

```text
Hidden during gameplay
```

Purpose:

- Detect when an arrow has escaped the board.

---

### 3.5 KeyArrow

Special arrow that unlocks gates or locked arrows.

Object variables:

```text
KeyColor = "Red" | "Blue" | "Green" | "Yellow"
UnlockTargetID = number
```

---

### 3.6 LockGate

Locked obstacle that disappears after key activation.

Object variables:

```text
LockID = number
LockColor = "Red" | "Blue" | "Green" | "Yellow"
IsUnlocked = false
```

---

### 3.7 ColorGate

Gate that only lets matching arrows pass.

Object variables:

```text
GateColor = "Red" | "Blue" | "Green" | "Yellow"
```

---

### 3.8 PortalIn / PortalOut

Advanced mechanic for later phases.

Object variables:

```text
PortalID = number
PairID = number
```

---

## 4. Global Variables

```text
CurrentLevel = 1
UnlockedLevel = 1
Coins = 0
TotalMoves = 0
TotalMistakes = 0
SoundEnabled = true
VibrationEnabled = true
AdsRemoved = false
```

---

## 5. Scene Variables for GameScene

```text
LevelID = 1
MistakeLimit = 3
Mistakes = 0
Moves = 0
ArrowsRemaining = 0
LevelCompleted = false
LevelFailed = false
InputLocked = false
```

---

## 6. Core Gameplay Logic

### 6.1 Tap Arrow

```text
Condition:
  Cursor/touch is on Arrow
  Left mouse button released / touch ended
  InputLocked = false
  Arrow.IsRemoved = false
  Arrow.IsMoving = false

Action:
  Call CheckArrowPath
```

---

### 6.2 Check Arrow Path

For MVP, path checking should be grid-based, not physics-based. This is cleaner for puzzle logic.

Each arrow has a grid position:

```text
GridX
GridY
Direction
```

Check cells in front of the arrow until board edge:

```text
If no object blocks the path:
  Move arrow out
Else:
  Register failed move
```

---

### 6.3 Successful Move

```text
Set Arrow.IsMoving = true
Move Arrow in its Direction
When Arrow reaches outside board:
  Delete Arrow
  ArrowsRemaining -= 1
  Moves += 1
  CheckWinCondition
```

---

### 6.4 Failed Move

```text
Mistakes += 1
Moves += 1
Play fail effect
Shake arrow slightly
CheckLoseCondition
```

---

### 6.5 Win Condition

```text
If ArrowsRemaining <= 0:
  LevelCompleted = true
  InputLocked = true
  Add coin reward
  Save progress
  Show WinLayer
```

---

### 6.6 Lose Condition

```text
If Mistakes >= MistakeLimit:
  LevelFailed = true
  InputLocked = true
  Show LoseLayer
```

---

## 7. Board System

### Recommended Board

```text
Grid width: 6
Grid height: 8
Cell size: 96 px
```

### Board Origin

```text
BoardStartX = 72
BoardStartY = 220
```

### Position Formula

```text
ObjectX = BoardStartX + GridX * CellSize
ObjectY = BoardStartY + GridY * CellSize
```

---

## 8. MVP Rules

First version must not include too many advanced systems.

MVP includes:

```text
Normal arrows
Walls/blockers
Mistake limit
Win/lose
Restart
Next level
50 levels
Coins
Hint placeholder
Ad placeholder
```

MVP does not include yet:

```text
Complex skins
Daily challenge
Leaderboard
Cloud save
In-app purchase final integration
Complex analytics
```

---

## 9. Development Priority

Correct order:

1. Build one playable level.
2. Make arrows move correctly.
3. Add path blocking logic.
4. Add win/lose condition.
5. Add level loading.
6. Add 10 levels.
7. Add UI.
8. Add 50 levels.
9. Add ads.
10. Prepare Play Store build.

---

## 10. Quality Rule

The first version must be simple, but it must not be broken. Every level must be solvable, input must feel responsive, and the player must understand why a move failed.
