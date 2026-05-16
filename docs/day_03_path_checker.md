# Arrow Escape Master — Day 03 PathChecker and Mistakes

This document defines Day 03 tasks for **Arrow Escape Master** in GDevelop.

Day 03 goal:

```text
Add PathChecker logic so arrows move only when their path is clear. If the path is blocked, the move fails, Mistakes increases, and LoseLayer appears after the mistake limit.
```

---

## 1. Required Before Day 03

Day 02 must already be complete:

- [ ] Arrow starts moving after tap
- [ ] Arrow moves in all four directions
- [ ] Arrow deletes after leaving screen
- [ ] ArrowsRemaining decreases
- [ ] WinLayer appears after last arrow exits
- [ ] Restart works
- [ ] InputLocked works during movement

Do not start Day 03 if arrow movement is unstable.

---

## 2. Day 03 Scope

Day 03 includes:

```text
Create blocker test level
Place PathChecker in front of selected arrow
Detect collision with Arrow and Blocker
Prevent movement if path is blocked
Increase Moves and Mistakes on failed move
Update UI after failed move
Show LoseLayer after 3 mistakes
```

Day 03 does not include:

```text
JSON level loading
Coins
Hints
Undo
Ads
Locks
Portals
Color gates
```

---

## 3. Required Objects

Confirm these objects exist:

```text
Arrow
Blocker
PathChecker
BoardBackground
MistakeText
MoveText
LoseLayer
LoseText
RestartLoseButton
```

---

## 4. Required Variables

### GameScene Variables

Confirm these scene variables exist:

```text
MistakeLimit = 3
Mistakes = 0
Moves = 0
InputLocked = 0
PathBlocked = 0
SelectedArrowID = 0
LevelCompleted = 0
LevelFailed = 0
```

### Arrow Object Variables

Confirm these object variables exist:

```text
ArrowID
GridX
GridY
Direction
IsMoving
IsRemoved
```

### Blocker Object Variables

Confirm these object variables exist:

```text
BlockerID
GridX
GridY
Type
```

---

## 5. Create Day 03 Test Level

Update the `GameScene` start event so the scene creates one arrow and one blocker.

### Arrow

```text
Create Arrow at X=264, Y=604
Set Arrow.ArrowID = 1
Set Arrow.GridX = 2
Set Arrow.GridY = 4
Set Arrow.Direction = up
Set Arrow.IsMoving = 0
Set Arrow.IsRemoved = 0
```

### Blocker

Place blocker above the arrow:

```text
Create Blocker at X=264, Y=412
Set Blocker.BlockerID = 1
Set Blocker.GridX = 2
Set Blocker.GridY = 2
Set Blocker.Type = stone
```

Why this blocks the arrow:

```text
Arrow is at grid cell (2,4)
Blocker is at grid cell (2,2)
Arrow direction is up
Blocker is in front of the arrow
Therefore path must be blocked
```

Set:

```text
ArrowsRemaining = 1
Mistakes = 0
Moves = 0
InputLocked = 0
LevelCompleted = 0
LevelFailed = 0
PathBlocked = 0
```

---

## 6. PathChecker Setup Rule

When player taps an arrow, before moving it, place `PathChecker` in front of it.

Important:

```text
PathChecker must not overlap the selected arrow itself.
```

For an up arrow:

```text
PathChecker.X = Arrow.X
PathChecker.Y = BoardStartY
PathChecker.Width = CellSize
PathChecker.Height = Arrow.Y - BoardStartY
```

With the Day 03 test level:

```text
Arrow.X = 264
Arrow.Y = 604
BoardStartY = 220
CellSize = 96

PathChecker.X = 264
PathChecker.Y = 220
PathChecker.Width = 96
PathChecker.Height = 384
```

This area checks the cells above the arrow.

---

## 7. PathChecker Direction Formulas

Use these formulas for all four directions.

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

---

## 8. Tap Arrow Logic Update

Replace the simple Day 02 tap logic with path-checking logic.

Conditions:

```text
Cursor/touch is on Arrow
Left mouse button released OR touch released
InputLocked = 0
Arrow.IsMoving = 0
Arrow.IsRemoved = 0
LevelCompleted = 0
LevelFailed = 0
```

Actions:

```text
Set SelectedArrowID = Arrow.ArrowID
Set PathBlocked = 0
Place PathChecker based on Arrow.Direction
Check if PathChecker collides with Blocker or another Arrow
If blocked: run failed move logic
If clear: run successful move logic
```

---

## 9. Detect Blocker Collision

After PathChecker is placed:

Condition:

```text
PathChecker is in collision with Blocker
```

Action:

```text
Set PathBlocked = 1
```

Expected in Day 03 test level:

```text
PathBlocked becomes 1 when tapping the up arrow.
```

---

## 10. Detect Arrow Collision

Later levels may have another arrow in the path.

Condition:

```text
PathChecker is in collision with Arrow
Arrow.ArrowID != SelectedArrowID
```

Action:

```text
Set PathBlocked = 1
```

Important:

```text
The selected arrow must not block itself.
```

PathChecker formulas avoid overlapping the selected arrow, but still keep this ID check as protection.

---

## 11. Failed Move Logic

If `PathBlocked = 1`, the arrow must not move.

Conditions:

```text
PathBlocked = 1
Selected Arrow is still valid
```

Actions:

```text
Add 1 to Moves
Add 1 to Mistakes
Set InputLocked = 0
Update MoveText
Update MistakeText
Run fail feedback
Check lose condition
```

The arrow remains in the same position.

---

## 12. Successful Move Logic Update

If `PathBlocked = 0`, use the Day 02 movement logic.

Actions:

```text
Set Arrow.IsMoving = 1
Set InputLocked = 1
Add 1 to Moves
Update MoveText
```

The arrow then moves using the direction movement events from Day 02.

---

## 13. Lose Condition

Create or confirm this event:

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

Expected result:

```text
After 3 blocked taps, LoseLayer appears.
```

---

## 14. UI Update Rules

At scene start:

```text
MistakeText = Mistakes: 0/3
MoveText = Moves: 0
```

After failed move:

```text
MistakeText = Mistakes: [Mistakes]/[MistakeLimit]
MoveText = Moves: [Moves]
```

After successful move:

```text
MoveText = Moves: [Moves]
```

---

## 15. Fail Feedback

Minimum Day 03 feedback:

```text
Temporarily change arrow color/tint
or move arrow slightly left/right
or show small fail text
```

Recommended simple feedback:

```text
Shake selected arrow for 0.15 seconds
```

Do not overwork animation yet. The key is that the player understands the move failed.

---

## 16. Test: Blocked Arrow

Use the Day 03 test level:

```text
Arrow:   GridX=2, GridY=4, Direction=up
Blocker: GridX=2, GridY=2
```

Expected behavior:

```text
Tap arrow once → arrow does not move
Moves = 1
Mistakes = 1
Tap arrow again → Moves = 2, Mistakes = 2
Tap arrow third time → LoseLayer appears
```

---

## 17. Test: Clear Arrow

After blocked test passes, remove the blocker or move it away.

Example blocker position that should not block:

```text
Blocker.GridX = 4
Blocker.GridY = 2
```

Expected behavior:

```text
Tap arrow → arrow moves up
Arrow exits screen
Arrow is deleted
ArrowsRemaining = 0
WinLayer appears
```

---

## 18. Test All Directions With Blockers

### Up Block Test

```text
Arrow at (2,4), direction up
Blocker at (2,2)
Expected: blocked
```

### Right Block Test

```text
Arrow at (2,4), direction right
Blocker at (4,4)
Expected: blocked
```

### Down Block Test

```text
Arrow at (2,4), direction down
Blocker at (2,6)
Expected: blocked
```

### Left Block Test

```text
Arrow at (2,4), direction left
Blocker at (0,4)
Expected: blocked
```

For each test:

```text
PathBlocked = 1
Arrow does not move
Mistakes increases
```

---

## 19. Common Problems

### Problem: Arrow moves through blocker

Check:

```text
PathChecker position and size
Blocker collision mask
PathChecker collision mask
PathBlocked is set before successful move logic
Successful move event requires PathBlocked = 0
```

---

### Problem: Arrow always fails even when path is clear

Check:

```text
PathChecker is overlapping selected Arrow
PathChecker size is too large
Arrow collision check does not exclude SelectedArrowID
PathBlocked is reset to 0 before every path check
```

---

### Problem: LoseLayer never appears

Check:

```text
Mistakes increases
MistakeLimit is 3
Lose condition event exists
LevelCompleted is still 0
LevelFailed starts as 0
LoseLayer visibility action works
```

---

### Problem: Mistakes increase multiple times from one tap

Check:

```text
Use trigger once / mouse released condition
Do not run failed logic every frame
Set a temporary input lock during check if needed
```

---

## 20. Day 03 Acceptance Test

Day 03 is complete only when all checks pass:

- [ ] PathChecker is placed correctly for up direction
- [ ] PathChecker is placed correctly for right direction
- [ ] PathChecker is placed correctly for down direction
- [ ] PathChecker is placed correctly for left direction
- [ ] Blocker in path blocks movement
- [ ] Another arrow in path blocks movement
- [ ] Selected arrow does not block itself
- [ ] Clear path allows movement
- [ ] Blocked path increases Moves
- [ ] Blocked path increases Mistakes
- [ ] Arrow stays in place after failed move
- [ ] MistakeText updates correctly
- [ ] MoveText updates correctly
- [ ] LoseLayer appears after 3 mistakes
- [ ] Restart resets Mistakes and Moves
- [ ] Clear path still triggers WinLayer

---

## 21. After Day 03

Next file to follow:

```text
docs/day_04_multiple_arrows.md
```

Day 04 goal:

```text
Add multiple arrows in one level and make them block/unblock each other correctly.
```

---

## 22. Critical Rule

Path checking must be deterministic.

Same board + same tap order must always produce the same result.

No random physics. No unclear collision behavior. No hidden movement rules.
