# Arrow Escape Master — Objects and Variables

This document defines all required GDevelop objects, object variables, scene variables, and global variables for **Arrow Escape Master**.

Naming must stay consistent. GDevelop event logic depends on exact object and variable names.

---

## 1. Naming Rules

Use these naming rules everywhere:

```text
Object names: PascalCase
Object variables: PascalCase
Scene variables: PascalCase
Global variables: PascalCase
JSON fields: camelCase
```

Examples:

```text
Object: Arrow
Object variable: Direction
Scene variable: ArrowsRemaining
Global variable: CurrentLevel
JSON field: mistakeLimit
```

Do not mix names like:

```text
arrow_direction
arrowDirection
Arrowdirection
```

Use one strict standard.

---

## 2. Global Variables

Create these in GDevelop project variables.

| Variable | Type | Default | Purpose |
|---|---:|---:|---|
| `CurrentLevel` | Number | `1` | Current level selected/played |
| `UnlockedLevel` | Number | `1` | Highest unlocked level |
| `Coins` | Number | `0` | Player coin balance |
| `SoundEnabled` | Number | `1` | Sound on/off, 1=true, 0=false |
| `VibrationEnabled` | Number | `1` | Vibration on/off |
| `AdsRemoved` | Number | `0` | Remove ads purchase state placeholder |
| `TotalMoves` | Number | `0` | Lifetime moves counter |
| `TotalMistakes` | Number | `0` | Lifetime mistakes counter |
| `CompletedLevels` | Number | `0` | Number of completed levels |
| `LastPlayedLevel` | Number | `1` | Last opened level |

For MVP, the required variables are:

```text
CurrentLevel
UnlockedLevel
Coins
SoundEnabled
VibrationEnabled
AdsRemoved
```

---

## 3. GameScene Variables

Create these inside `GameScene`.

| Variable | Type | Default | Purpose |
|---|---:|---:|---|
| `LevelID` | Number | `1` | Loaded level ID |
| `MistakeLimit` | Number | `3` | Maximum allowed mistakes |
| `Mistakes` | Number | `0` | Current mistakes |
| `Moves` | Number | `0` | Current level move count |
| `ArrowsRemaining` | Number | `0` | Active arrows left on board |
| `LevelCompleted` | Number | `0` | Win state flag |
| `LevelFailed` | Number | `0` | Lose state flag |
| `InputLocked` | Number | `0` | Blocks input during animation or popup |
| `BoardStartX` | Number | `72` | Board left coordinate |
| `BoardStartY` | Number | `220` | Board top coordinate |
| `CellSize` | Number | `96` | Grid cell size in pixels |
| `BoardWidth` | Number | `6` | Board columns |
| `BoardHeight` | Number | `8` | Board rows |
| `BoardRightEdge` | Number | `648` | BoardStartX + BoardWidth * CellSize |
| `BoardBottomEdge` | Number | `988` | BoardStartY + BoardHeight * CellSize |
| `RewardCoins` | Number | `10` | Coins given after level win |
| `PathBlocked` | Number | `0` | Result of path check |
| `SelectedArrowID` | Number | `0` | Arrow selected by player |
| `MoveSpeed` | Number | `900` | Arrow escape movement speed |

---

## 4. Main Gameplay Objects

### 4.1 Arrow

Object type:

```text
Sprite
```

Purpose:

```text
Main playable arrow object.
```

Required animations:

| Animation ID | Name | Direction |
|---:|---|---|
| `0` | `ArrowUp` | up |
| `1` | `ArrowRight` | right |
| `2` | `ArrowDown` | down |
| `3` | `ArrowLeft` | left |

Required object variables:

| Variable | Type | Default | Purpose |
|---|---:|---:|---|
| `ArrowID` | Number | `0` | Unique arrow ID in level |
| `GridX` | Number | `0` | Grid column |
| `GridY` | Number | `0` | Grid row |
| `Direction` | String | `up` | Movement direction |
| `Color` | String | `none` | Arrow color for future gates |
| `Locked` | Number | `0` | 1 means locked |
| `KeyID` | Number | `0` | Required key ID if locked |
| `IsMoving` | Number | `0` | 1 while arrow is escaping |
| `IsRemoved` | Number | `0` | 1 after removed |
| `CanMove` | Number | `1` | 1 if currently allowed to move |

MVP required variables:

```text
ArrowID
GridX
GridY
Direction
IsMoving
IsRemoved
```

---

### 4.2 Blocker

Object type:

```text
Sprite
```

Purpose:

```text
Static obstacle that blocks arrows.
```

Required object variables:

| Variable | Type | Default | Purpose |
|---|---:|---:|---|
| `BlockerID` | Number | `0` | Unique blocker ID |
| `GridX` | Number | `0` | Grid column |
| `GridY` | Number | `0` | Grid row |
| `Type` | String | `stone` | stone / wood / metal |

---

### 4.3 PathChecker

Object type:

```text
Sprite or Shape Painter
```

Purpose:

```text
Hidden rectangle used to check whether an arrow path is blocked.
```

Required object variables:

| Variable | Type | Default | Purpose |
|---|---:|---:|---|
| `Active` | Number | `0` | 1 only during path check |
| `Direction` | String | `none` | Direction being checked |
| `OwnerArrowID` | Number | `0` | Arrow being checked |

Visibility:

```text
Hidden in final gameplay
```

Recommended color during debug:

```text
Transparent red with 30% opacity
```

Remove or hide before release.

---

### 4.4 BoardBackground

Object type:

```text
Sprite or Tiled Sprite
```

Purpose:

```text
Visual background for the puzzle grid.
```

Recommended size:

```text
576 x 768
```

Position:

```text
X = 72
Y = 220
```

---

### 4.5 BoardCellDebug

Object type:

```text
Shape Painter or Sprite
```

Purpose:

```text
Temporary debug object to show grid cells.
```

Release rule:

```text
Do not show in final release.
```

---

## 5. Future Gameplay Objects

These are not required for the first prototype, but names are reserved.

### 5.1 KeyArrow

Object type:

```text
Sprite
```

Purpose:

```text
Special arrow that unlocks locked gates or arrows.
```

Variables:

```text
KeyID = 0
KeyColor = red
Used = 0
```

---

### 5.2 LockGate

Object type:

```text
Sprite
```

Purpose:

```text
Gate that blocks movement until unlocked.
```

Variables:

```text
LockID = 0
RequiredKeyID = 0
LockColor = red
Unlocked = 0
GridX = 0
GridY = 0
```

---

### 5.3 ColorGate

Object type:

```text
Sprite
```

Purpose:

```text
Gate that allows only matching color arrows.
```

Variables:

```text
GateID = 0
GateColor = red
GridX = 0
GridY = 0
```

---

### 5.4 PortalIn

Object type:

```text
Sprite
```

Variables:

```text
PortalID = 0
PairID = 0
GridX = 0
GridY = 0
```

---

### 5.5 PortalOut

Object type:

```text
Sprite
```

Variables:

```text
PortalID = 0
PairID = 0
GridX = 0
GridY = 0
```

---

## 6. UI Objects — GameScene

Create these objects on `UILayer`.

| Object | Type | Purpose |
|---|---|---|
| `LevelText` | Text | Shows current level |
| `MistakeText` | Text | Shows mistakes/mistake limit |
| `MoveText` | Text | Shows move count |
| `CoinText` | Text | Shows coins |
| `RestartButton` | Sprite/Button | Restarts level |
| `HintButton` | Sprite/Button | Hint action placeholder |
| `UndoButton` | Sprite/Button | Undo action placeholder |
| `MenuButton` | Sprite/Button | Back to menu |
| `PauseButton` | Sprite/Button | Opens pause layer |

Recommended UI positions:

```text
LevelText:      x=40,  y=40
CoinText:       x=500, y=40
MistakeText:    x=40,  y=100
MoveText:       x=500, y=100
RestartButton:  x=40,  y=1120
HintButton:     x=260, y=1120
UndoButton:     x=480, y=1120
```

---

## 7. MainMenu Objects

Create these inside `MainMenu`.

| Object | Type | Purpose |
|---|---|---|
| `Background` | Sprite | Main menu background |
| `GameTitleText` | Text | Game title |
| `PlayButton` | Sprite/Button | Continue/start game |
| `LevelSelectButton` | Sprite/Button | Opens level select |
| `SettingsButton` | Sprite/Button | Opens settings |
| `RemoveAdsButton` | Sprite/Button | Remove ads placeholder |
| `MenuCoinText` | Text | Shows coins |

Recommended positions:

```text
GameTitleText:       x=80,  y=180
PlayButton:          x=210, y=430
LevelSelectButton:   x=210, y=550
SettingsButton:      x=210, y=670
RemoveAdsButton:     x=210, y=790
MenuCoinText:        x=500, y=50
```

---

## 8. LevelSelect Objects

Create these inside `LevelSelect`.

| Object | Type | Purpose |
|---|---|---|
| `LevelButton` | Sprite/Button | Reused level button object |
| `LevelNumberText` | Text | Level number label |
| `LockedIcon` | Sprite | Lock icon |
| `CompletedIcon` | Sprite | Completed marker |
| `BackButton` | Sprite/Button | Return to MainMenu |

For MVP, create 10 buttons manually first.

Later, generate buttons dynamically.

---

## 9. WinLayer Objects

Create on `WinLayer`.

| Object | Type | Purpose |
|---|---|---|
| `WinPanel` | Sprite | Background panel |
| `WinText` | Text | Level complete text |
| `CoinRewardText` | Text | Coins earned |
| `NextButton` | Sprite/Button | Loads next level |
| `ReplayButton` | Sprite/Button | Replays level |
| `HomeButton` | Sprite/Button | Back to menu |

Initial layer state:

```text
Hidden
```

---

## 10. LoseLayer Objects

Create on `LoseLayer`.

| Object | Type | Purpose |
|---|---|---|
| `LosePanel` | Sprite | Background panel |
| `LoseText` | Text | Level failed text |
| `RestartLoseButton` | Sprite/Button | Restarts level |
| `ExtraChanceButton` | Sprite/Button | Rewarded ad placeholder |
| `LoseHomeButton` | Sprite/Button | Back to menu |

Initial layer state:

```text
Hidden
```

---

## 11. Settings Objects

Create inside `Settings` scene.

| Object | Type | Purpose |
|---|---|---|
| `SettingsTitleText` | Text | Title |
| `SoundToggle` | Sprite/Button | Sound on/off |
| `VibrationToggle` | Sprite/Button | Vibration on/off |
| `PrivacyPolicyButton` | Sprite/Button | Opens policy link later |
| `SettingsBackButton` | Sprite/Button | Back to MainMenu |

---

## 12. Storage Keys

Use these exact storage keys in GDevelop.

```text
UnlockedLevel
CurrentLevel
Coins
SoundEnabled
VibrationEnabled
AdsRemoved
CompletedLevels
```

Do not rename them after release unless migration logic is added.

---

## 13. Object Creation Order in GDevelop

Build objects in this order:

```text
1. Arrow
2. Blocker
3. PathChecker
4. BoardBackground
5. LevelText
6. MistakeText
7. MoveText
8. CoinText
9. RestartButton
10. WinLayer objects
11. LoseLayer objects
12. MainMenu objects
13. LevelSelect objects
14. Settings objects
```

---

## 14. MVP Required Objects Only

For the first working prototype, only these are mandatory:

```text
Arrow
Blocker
PathChecker
BoardBackground
LevelText
MistakeText
MoveText
RestartButton
WinPanel
WinText
NextButton
LosePanel
LoseText
RestartLoseButton
```

Everything else can be added after the core prototype works.

---

## 15. Critical Rule

Do not change object names after event logic is created.

Changing object names later will break GDevelop events.

Approved names are the ones in this document.
