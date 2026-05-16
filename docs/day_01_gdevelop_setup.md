# Arrow Escape Master — Day 01 GDevelop Setup

This document is the exact Day 01 setup plan for building **Arrow Escape Master** in GDevelop.

Day 01 goal:

```text
Create the GDevelop project, create MainMenu and GameScene, add the first manual arrow, and make the first basic scene structure ready.
```

Do not work on ads, skins, Play Store, or advanced mechanics on Day 01.

---

## 1. Before Starting

Required tools:

```text
GDevelop
GitHub repository: foxboxstudiodev/Arrow-Escape-Master
Project folder on computer
```

Recommended local folder:

```text
C:\Users\User\Desktop\Arrow-Escape-Master
```

or:

```text
C:\Users\Rovshan\Desktop\Arrow-Escape-Master
```

Use the correct one depending on the computer.

---

## 2. Clone Repository to Computer

Open PowerShell in Desktop and run:

```powershell
git clone https://github.com/foxboxstudiodev/Arrow-Escape-Master.git
cd Arrow-Escape-Master
```

Check files:

```powershell
dir
```

Expected files:

```text
README.md
ROADMAP.md
docs
levels
```

---

## 3. Create Required Folders If Missing

Run this in PowerShell inside the repo folder:

```powershell
mkdir gdevelop
mkdir assets
mkdir assets\arrows
mkdir assets\blockers
mkdir assets\backgrounds
mkdir assets\buttons
mkdir assets\icons
mkdir assets\ui
mkdir assets\sounds
mkdir exports
mkdir exports\android
```

If PowerShell says the folder already exists, that is fine.

---

## 4. Open GDevelop

In GDevelop:

```text
Create a new project
Choose Empty Game
Project name: ArrowEscapeMaster
```

Project settings:

```text
Game name: Arrow Escape Master
Orientation: Portrait
Window width: 720
Window height: 1280
Package name: com.foxboxstudio.arrowescapemaster
```

Save project as:

```text
gdevelop/ArrowEscapeMaster.json
```

Full path example:

```text
C:\Users\User\Desktop\Arrow-Escape-Master\gdevelop\ArrowEscapeMaster.json
```

---

## 5. Create Scenes

Create these scenes:

```text
MainMenu
GameScene
```

Optional later scenes:

```text
BootScene
LevelSelect
Settings
```

Day 01 only needs:

```text
MainMenu
GameScene
```

---

## 6. MainMenu Setup

Open `MainMenu`.

Create object:

```text
GameTitleText
```

Type:

```text
Text
```

Text:

```text
Arrow Escape Master
```

Position:

```text
X = 80
Y = 180
```

Create object:

```text
PlayButton
```

For Day 01, this can be a Text object or a simple button sprite.

Text:

```text
PLAY
```

Position:

```text
X = 280
Y = 500
```

Event:

```text
Condition:
  Cursor/touch is on PlayButton
  Left mouse button released or touch released

Action:
  Change scene to GameScene
```

Acceptance test:

```text
Pressing PLAY opens GameScene.
```

---

## 7. GameScene Layers

Open `GameScene`.

Create layers:

```text
BaseLayer
UILayer
WinLayer
LoseLayer
```

Layer visibility at start:

```text
BaseLayer visible
UILayer visible
WinLayer hidden
LoseLayer hidden
```

---

## 8. GameScene Variables

Create scene variables exactly:

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
SelectedArrowID = 0
```

Do not rename them.

---

## 9. Create Arrow Object

Create object:

```text
Arrow
```

Type:

```text
Sprite
```

For Day 01, use a temporary colored square if arrow art is not ready.

Object size:

```text
96 x 96
```

Object variables:

```text
ArrowID = 0
GridX = 0
GridY = 0
Direction = up
IsMoving = 0
IsRemoved = 0
```

Create 4 animations later:

```text
0 = ArrowUp
1 = ArrowRight
2 = ArrowDown
3 = ArrowLeft
```

Day 01 can start with only animation 0.

---

## 10. Create Blocker Object

Create object:

```text
Blocker
```

Type:

```text
Sprite
```

Temporary shape is acceptable for Day 01.

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

## 11. Create PathChecker Object

Create object:

```text
PathChecker
```

Type:

```text
Sprite or Shape Painter
```

Day 01 setting:

```text
Visible while debugging
Color: transparent red if possible
```

Later release setting:

```text
Hidden
```

Purpose:

```text
Checks whether selected arrow has a clear path.
```

---

## 12. Create BoardBackground

Create object:

```text
BoardBackground
```

Type:

```text
Sprite or Tiled Sprite
```

Temporary rectangle is acceptable.

Position:

```text
X = 72
Y = 220
```

Size:

```text
Width = 576
Height = 768
```

This matches:

```text
6 columns x 8 rows x 96 cell size
```

---

## 13. Create UI Text Objects

Create these on `UILayer`:

```text
LevelText
MistakeText
MoveText
RestartButton
```

Text values:

```text
LevelText = Level 1
MistakeText = Mistakes: 0/3
MoveText = Moves: 0
RestartButton = Restart
```

Positions:

```text
LevelText: X=40, Y=40
MistakeText: X=40, Y=100
MoveText: X=500, Y=100
RestartButton: X=40, Y=1120
```

---

## 14. Create WinLayer Objects

On `WinLayer`, create:

```text
WinText
NextButton
ReplayButton
```

Text values:

```text
WinText = LEVEL COMPLETE
NextButton = NEXT
ReplayButton = REPLAY
```

Set WinLayer hidden at scene start.

---

## 15. Create LoseLayer Objects

On `LoseLayer`, create:

```text
LoseText
RestartLoseButton
```

Text values:

```text
LoseText = LEVEL FAILED
RestartLoseButton = RESTART
```

Set LoseLayer hidden at scene start.

---

## 16. Scene Start Event

In `GameScene`, create this event:

```text
Condition:
  At the beginning of the scene

Actions:
  Set Mistakes = 0
  Set Moves = 0
  Set ArrowsRemaining = 1
  Set LevelCompleted = 0
  Set LevelFailed = 0
  Set InputLocked = 0
  Hide WinLayer
  Hide LoseLayer
  Create Arrow at X=264, Y=604
  Set Arrow.ArrowID = 1
  Set Arrow.GridX = 2
  Set Arrow.GridY = 4
  Set Arrow.Direction = up
  Set Arrow.IsMoving = 0
  Set Arrow.IsRemoved = 0
```

Expected result:

```text
When GameScene starts, one arrow appears in the board.
```

---

## 17. Day 01 Acceptance Test

Day 01 is complete only when:

- [ ] Repository exists locally
- [ ] GDevelop project is saved in `gdevelop/ArrowEscapeMaster.json`
- [ ] MainMenu exists
- [ ] GameScene exists
- [ ] PLAY button opens GameScene
- [ ] GameScene has required variables
- [ ] GameScene has required layers
- [ ] Arrow object exists
- [ ] Blocker object exists
- [ ] PathChecker object exists
- [ ] BoardBackground exists
- [ ] UI texts exist
- [ ] WinLayer exists and is hidden
- [ ] LoseLayer exists and is hidden
- [ ] One arrow appears at X=264, Y=604

---

## 18. After Day 01

Next file to follow:

```text
docs/day_02_arrow_movement.md
```

Day 02 goal:

```text
Make the arrow move out of the board when tapped.
```

---

## 19. Critical Rule

Do not continue to Day 02 until Day 01 acceptance test passes.

A broken base scene will create problems in every later phase.
