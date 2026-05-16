# Arrow Escape Master — Day 02 Arrow Movement

This document defines Day 02 tasks for **Arrow Escape Master** in GDevelop.

Day 02 goal:

```text
Make arrows move in their own direction when tapped and delete them after they leave the screen.
```

Day 02 does not include advanced path blocking yet. The first goal is movement reliability.

---

## 1. Required Before Day 02

Day 01 must already be complete:

- [ ] GDevelop project exists
- [ ] `MainMenu` exists
- [ ] `GameScene` exists
- [ ] `Arrow` object exists
- [ ] GameScene has one test arrow
- [ ] PLAY button opens GameScene
- [ ] Scene variables exist
- [ ] WinLayer and LoseLayer exist

Do not start Day 02 if Day 01 is broken.

---

## 2. Day 02 Scope

Day 02 includes:

```text
Tap Arrow
Set Arrow.IsMoving = 1
Lock input while arrow moves
Move arrow by direction
Delete arrow outside screen
Decrease ArrowsRemaining
Show WinLayer when no arrows remain
Restart level
```

Day 02 does not include:

```text
PathChecker collision logic
Blocked move mistake logic
JSON level loading
Coin system
Ads
Advanced gates
```

---

## 3. Confirm Required Variables

Inside `GameScene`, confirm these scene variables exist:

```text
InputLocked = 0
ArrowsRemaining = 1
MoveSpeed = 900
Moves = 0
LevelCompleted = 0
LevelFailed = 0
```

Inside `Arrow`, confirm these object variables exist:

```text
Direction = up
IsMoving = 0
IsRemoved = 0
ArrowID = 1
```

---

## 4. Update Scene Start Event

At the beginning of `GameScene`, make sure the test arrow is created with these values:

```text
Create Arrow at X=264, Y=604
Set Arrow.ArrowID = 1
Set Arrow.GridX = 2
Set Arrow.GridY = 4
Set Arrow.Direction = up
Set Arrow.IsMoving = 0
Set Arrow.IsRemoved = 0
Set ArrowsRemaining = 1
Set InputLocked = 0
Set Moves = 0
Set LevelCompleted = 0
Set LevelFailed = 0
Hide WinLayer
Hide LoseLayer
```

For this test, the arrow direction is:

```text
up
```

---

## 5. Tap Arrow Event

Create this event in `GameScene`.

Conditions:

```text
Cursor/touch is on Arrow
Left mouse button released OR touch released
Scene variable InputLocked = 0
Arrow variable IsMoving = 0
Arrow variable IsRemoved = 0
Scene variable LevelCompleted = 0
Scene variable LevelFailed = 0
```

Actions:

```text
Set Arrow.IsMoving = 1
Set Scene variable InputLocked = 1
Add 1 to Scene variable Moves
Update MoveText
```

For Day 02, do not check path blocking yet.

Expected result:

```text
When the player taps the arrow, the arrow starts moving.
```

---

## 6. Movement Events

Create four separate events for arrow movement.

---

### 6.1 Move Up

Conditions:

```text
Arrow variable IsMoving = 1
Arrow variable Direction = up
```

Action:

```text
Subtract MoveSpeed * TimeDelta() from Arrow.Y position
```

Meaning:

```text
Arrow.Y = Arrow.Y - MoveSpeed * TimeDelta()
```

---

### 6.2 Move Right

Conditions:

```text
Arrow variable IsMoving = 1
Arrow variable Direction = right
```

Action:

```text
Add MoveSpeed * TimeDelta() to Arrow.X position
```

Meaning:

```text
Arrow.X = Arrow.X + MoveSpeed * TimeDelta()
```

---

### 6.3 Move Down

Conditions:

```text
Arrow variable IsMoving = 1
Arrow variable Direction = down
```

Action:

```text
Add MoveSpeed * TimeDelta() to Arrow.Y position
```

Meaning:

```text
Arrow.Y = Arrow.Y + MoveSpeed * TimeDelta()
```

---

### 6.4 Move Left

Conditions:

```text
Arrow variable IsMoving = 1
Arrow variable Direction = left
```

Action:

```text
Subtract MoveSpeed * TimeDelta() from Arrow.X position
```

Meaning:

```text
Arrow.X = Arrow.X - MoveSpeed * TimeDelta()
```

---

## 7. Delete Arrow Outside Screen

Create separate events to delete arrows after they leave the screen.

---

### 7.1 Delete Up Arrow

Conditions:

```text
Arrow variable IsMoving = 1
Arrow variable Direction = up
Arrow.Y < -120
```

Actions:

```text
Delete Arrow
Subtract 1 from ArrowsRemaining
Set InputLocked = 0
```

---

### 7.2 Delete Right Arrow

Conditions:

```text
Arrow variable IsMoving = 1
Arrow variable Direction = right
Arrow.X > 840
```

Actions:

```text
Delete Arrow
Subtract 1 from ArrowsRemaining
Set InputLocked = 0
```

---

### 7.3 Delete Down Arrow

Conditions:

```text
Arrow variable IsMoving = 1
Arrow variable Direction = down
Arrow.Y > 1400
```

Actions:

```text
Delete Arrow
Subtract 1 from ArrowsRemaining
Set InputLocked = 0
```

---

### 7.4 Delete Left Arrow

Conditions:

```text
Arrow variable IsMoving = 1
Arrow variable Direction = left
Arrow.X < -120
```

Actions:

```text
Delete Arrow
Subtract 1 from ArrowsRemaining
Set InputLocked = 0
```

---

## 8. Win Condition Event

Create event:

Conditions:

```text
Scene variable ArrowsRemaining <= 0
Scene variable LevelCompleted = 0
Scene variable LevelFailed = 0
```

Actions:

```text
Set LevelCompleted = 1
Set InputLocked = 1
Show WinLayer
```

Expected result:

```text
When the only arrow exits the screen, WinLayer appears.
```

---

## 9. Restart Events

Create restart events for all restart-type buttons.

### RestartButton

Conditions:

```text
Cursor/touch is on RestartButton
Left mouse button released OR touch released
```

Action:

```text
Restart GameScene
```

### ReplayButton

Conditions:

```text
Cursor/touch is on ReplayButton
Left mouse button released OR touch released
```

Action:

```text
Restart GameScene
```

---

## 10. NextButton Temporary Event

For Day 02, `NextButton` can restart the same scene.

Conditions:

```text
Cursor/touch is on NextButton
Left mouse button released OR touch released
```

Action:

```text
Restart GameScene
```

Later, this will become:

```text
CurrentLevel += 1
Load next level
```

---

## 11. UI Update

At scene start:

```text
LevelText = Level 1
MistakeText = Mistakes: 0/3
MoveText = Moves: 0
```

After tap:

```text
MoveText = Moves: [Moves]
```

For Day 02, the important UI is:

```text
MoveText updates after tapping arrow
WinLayer appears after arrow exits
```

---

## 12. Direction Testing

After up direction works, test other directions manually.

Change the test arrow direction and animation.

### Test Right

Scene start:

```text
Arrow position: X=264, Y=604
Direction = right
Animation = ArrowRight
```

Expected:

```text
Arrow moves right and exits screen.
```

### Test Down

```text
Direction = down
Animation = ArrowDown
```

Expected:

```text
Arrow moves down and exits screen.
```

### Test Left

```text
Direction = left
Animation = ArrowLeft
```

Expected:

```text
Arrow moves left and exits screen.
```

Return test level to:

```text
Direction = up
```

when all tests pass.

---

## 13. Common Problems

### Problem: Arrow does not move

Check:

```text
IsMoving becomes 1 after tap
InputLocked is 0 before tap
Direction text exactly equals up/right/down/left
MoveSpeed is greater than 0
Movement event is not disabled
```

---

### Problem: Arrow moves but never deletes

Check:

```text
Delete condition threshold
Arrow direction value
Arrow position value
Delete event order
```

---

### Problem: WinLayer does not appear

Check:

```text
ArrowsRemaining decreases after delete
WinLayer visibility action exists
LevelCompleted starts as 0
LevelFailed starts as 0
```

---

### Problem: Arrow moves multiple times or input breaks

Check:

```text
InputLocked is set to 1 after tap
InputLocked is set back to 0 only after arrow deletion
Arrow.IsMoving is checked before tap
```

---

## 14. Day 02 Acceptance Test

Day 02 is complete only when all checks pass:

- [ ] Arrow starts moving after tap
- [ ] Input locks while arrow moves
- [ ] Up arrow exits through top side
- [ ] Right arrow exits through right side
- [ ] Down arrow exits through bottom side
- [ ] Left arrow exits through left side
- [ ] Arrow deletes after leaving screen
- [ ] ArrowsRemaining decreases
- [ ] WinLayer appears after last arrow exits
- [ ] RestartButton works
- [ ] ReplayButton works
- [ ] NextButton placeholder works
- [ ] MoveText updates after tap
- [ ] No crash after restart

---

## 15. After Day 02

Next file to follow:

```text
docs/day_03_path_checker.md
```

Day 03 goal:

```text
Add PathChecker so blocked arrows fail and count mistakes.
```

---

## 16. Critical Rule

Do not add blockers or mistakes until arrow movement is perfect.

Movement must be stable first. Collision logic depends on it.
