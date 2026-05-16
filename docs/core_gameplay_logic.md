# Arrow Escape Master — Core Gameplay Logic

This document defines the core gameplay logic for **Arrow Escape Master**.

This is the most important technical document for the first playable prototype. The game must feel simple, deterministic, and fair.

---

## 1. Core Game Loop

The entire gameplay loop is:

```text
Player taps an arrow
↓
Game checks the arrow direction
↓
Game checks whether the path is clear
↓
If clear: arrow escapes
↓
If blocked: mistake is counted
↓
Game checks win or lose condition
```

---

## 2. Main Gameplay Rule

An arrow can move only in its own direction.

Allowed directions:

```text
up
right
down
left
```

An arrow does not turn, rotate, or choose a different path.

---

## 3. Object State

Each `Arrow` object must have these variables:

```text
ArrowID
GridX
GridY
Direction
Color
Locked
KeyID
IsMoving
IsRemoved
```

For the MVP, the critical variables are:

```text
GridX
GridY
Direction
IsMoving
IsRemoved
```

---

## 4. Scene State

`GameScene` must control the level state with these scene variables:

```text
MistakeLimit = 3
Mistakes = 0
Moves = 0
ArrowsRemaining = 0
LevelCompleted = 0
LevelFailed = 0
InputLocked = 0
```

Meaning:

```text
InputLocked = 0 → player can tap arrows
InputLocked = 1 → player input is disabled
LevelCompleted = 1 → win state active
LevelFailed = 1 → lose state active
```

---

## 5. Tap Input Logic

The player can interact with an arrow only when all conditions are true:

```text
InputLocked = 0
Arrow.IsMoving = 0
Arrow.IsRemoved = 0
LevelCompleted = 0
LevelFailed = 0
```

GDevelop event logic:

```text
Condition:
  Cursor/touch is on Arrow
  Touch released or left mouse button released
  Scene variable InputLocked = 0
  Arrow variable IsMoving = 0
  Arrow variable IsRemoved = 0

Action:
  Start path check for selected Arrow
```

---

## 6. Path Checking — Design Choice

For the MVP, use a hidden `PathChecker` object.

This is easier in GDevelop than building a full loop-based grid parser from the first day.

`PathChecker` is a hidden rectangle that is temporarily placed in front of the selected arrow.

Purpose:

```text
Detect whether another Arrow or Blocker exists in the selected arrow's forward path.
```

---

## 7. PathChecker Object

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
Hidden during gameplay
```

Size is dynamic and changes depending on arrow direction.

---

## 8. PathChecker Placement Logic

### 8.1 Up Direction

If selected arrow direction is `up`:

```text
PathChecker.X = Arrow.X
PathChecker.Y = BoardStartY
PathChecker.Width = CellSize
PathChecker.Height = Arrow.Y - BoardStartY
```

Meaning:

```text
Check all space from top board edge to the arrow.
```

---

### 8.2 Right Direction

If selected arrow direction is `right`:

```text
PathChecker.X = Arrow.X + CellSize
PathChecker.Y = Arrow.Y
PathChecker.Width = BoardRightEdge - (Arrow.X + CellSize)
PathChecker.Height = CellSize
```

Where:

```text
BoardRightEdge = BoardStartX + BoardWidth * CellSize
```

---

### 8.3 Down Direction

If selected arrow direction is `down`:

```text
PathChecker.X = Arrow.X
PathChecker.Y = Arrow.Y + CellSize
PathChecker.Width = CellSize
PathChecker.Height = BoardBottomEdge - (Arrow.Y + CellSize)
```

Where:

```text
BoardBottomEdge = BoardStartY + BoardHeight * CellSize
```

---

### 8.4 Left Direction

If selected arrow direction is `left`:

```text
PathChecker.X = BoardStartX
PathChecker.Y = Arrow.Y
PathChecker.Width = Arrow.X - BoardStartX
PathChecker.Height = CellSize
```

---

## 9. Important Collision Rule

When checking path collision, the selected arrow itself must not count as a blocker.

Correct logic:

```text
PathChecker collides with another Arrow OR Blocker → path blocked
PathChecker does not collide with another Arrow or Blocker → path clear
```

Wrong logic:

```text
PathChecker collides with selected Arrow → fail
```

To avoid false collision:

```text
Place PathChecker only in front of Arrow, not on top of Arrow.
```

---

## 10. Clear Path Result

If the path is clear:

```text
Move is successful
Arrow starts escaping
Moves += 1
Arrow.IsMoving = 1
```

Do not delete the arrow instantly. Animate it first.

---

## 11. Blocked Path Result

If the path is blocked:

```text
Move fails
Mistakes += 1
Moves += 1
Arrow shakes
UI updates
Lose condition is checked
```

The arrow must stay in the same grid cell.

---

## 12. Arrow Escape Movement

Recommended movement speed:

```text
900 px/sec
```

Escape targets:

```text
up    → Y = -150
right → X = 870
down  → Y = 1430
left  → X = -150
```

When arrow goes outside screen:

```text
Delete Arrow
ArrowsRemaining -= 1
Check win condition
```

---

## 13. Direction Movement Rules

### Up

```text
If Arrow.Direction = up and Arrow.IsMoving = 1:
  Arrow.Y -= 900 * TimeDelta()
```

Delete when:

```text
Arrow.Y < -120
```

---

### Right

```text
If Arrow.Direction = right and Arrow.IsMoving = 1:
  Arrow.X += 900 * TimeDelta()
```

Delete when:

```text
Arrow.X > 840
```

---

### Down

```text
If Arrow.Direction = down and Arrow.IsMoving = 1:
  Arrow.Y += 900 * TimeDelta()
```

Delete when:

```text
Arrow.Y > 1400
```

---

### Left

```text
If Arrow.Direction = left and Arrow.IsMoving = 1:
  Arrow.X -= 900 * TimeDelta()
```

Delete when:

```text
Arrow.X < -120
```

---

## 14. Win Logic

Win condition:

```text
ArrowsRemaining <= 0
LevelCompleted = 0
LevelFailed = 0
```

Actions:

```text
LevelCompleted = 1
InputLocked = 1
Add reward coins
Unlock next level
Save progress
Show WinLayer
```

Reward logic:

```text
Coins += rewardCoins
```

Perfect bonus later:

```text
If Mistakes = 0:
  Coins += bonusCoins
```

---

## 15. Lose Logic

Lose condition:

```text
Mistakes >= MistakeLimit
LevelCompleted = 0
LevelFailed = 0
```

Actions:

```text
LevelFailed = 1
InputLocked = 1
Show LoseLayer
```

---

## 16. Restart Logic

Restart button action:

```text
Restart GameScene
```

On restart, reset:

```text
Mistakes = 0
Moves = 0
LevelCompleted = 0
LevelFailed = 0
InputLocked = 0
Reload level arrows
Hide WinLayer
Hide LoseLayer
```

---

## 17. Next Level Logic

When player presses `NextButton`:

```text
CurrentLevel += 1
Restart GameScene
```

If no next level exists:

```text
Go to LevelSelect or MainMenu
```

For the first prototype with 10 levels:

```text
If CurrentLevel > 10:
  CurrentLevel = 10
  Show Coming Soon message
```

---

## 18. UI Update Logic

After every move, update:

```text
LevelText = "Level " + CurrentLevel
MoveText = "Moves: " + Moves
MistakeText = "Mistakes: " + Mistakes + "/" + MistakeLimit
CoinText = Coins
```

UI should update after:

```text
Scene start
Successful move
Failed move
Win reward
Restart
Next level
```

---

## 19. Fail Feedback

A failed move must be visible to the player.

Minimum MVP feedback:

```text
Arrow shakes
MistakeText updates
Short fail sound later
Small red flash later
```

Without feedback, players will think the game is broken.

---

## 20. Input Locking Rule

Input must be locked during animations.

When arrow begins escaping:

```text
InputLocked = 1
```

When arrow is deleted and win is not triggered:

```text
InputLocked = 0
```

Why:

```text
Prevents player from tapping multiple arrows while one arrow is moving.
```

Later, if we want faster gameplay, we can allow multiple arrow movement. For MVP, keep one move at a time.

---

## 21. Required First Playable Prototype

The first working prototype is complete only when this test passes:

```text
1. Open GameScene
2. Tap a clear arrow
3. Arrow moves out of screen
4. Arrow is deleted
5. ArrowsRemaining decreases
6. WinLayer appears when no arrows remain
7. Restart works
8. Blocked arrow gives mistake
9. LoseLayer appears after 3 mistakes
```

---

## 22. Do Not Add Yet

Do not add these before the core logic is stable:

```text
AdMob
Skins
Portals
Locks
Daily rewards
Store screenshots
In-app purchases
Complex animations
```

The correct order is:

```text
Core gameplay first
Level system second
Monetization third
Polish fourth
```

---

## 23. Quality Standard

The core gameplay must be deterministic.

That means:

```text
Same level + same tap order = same result every time
```

No random physics. No unclear collisions. No hidden rules.
