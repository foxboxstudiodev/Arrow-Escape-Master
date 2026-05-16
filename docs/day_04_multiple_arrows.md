# Arrow Escape Master — Day 04 Multiple Arrows

This document defines Day 04 tasks for **Arrow Escape Master** in GDevelop.

Day 04 goal:

```text
Create levels with multiple arrows where arrows block each other, and clearing one arrow opens the path for another arrow.
```

This is the first point where Arrow Escape Master becomes a real puzzle game instead of a one-arrow prototype.

---

## 1. Required Before Day 04

Day 03 must already be complete:

- [ ] Arrow movement works in all four directions
- [ ] PathChecker works for all four directions
- [ ] Blockers can block arrows
- [ ] Other arrows can block arrows
- [ ] Selected arrow does not block itself
- [ ] Failed move increases Mistakes
- [ ] LoseLayer appears after mistake limit
- [ ] Clear path still triggers WinLayer
- [ ] Restart resets the level correctly

Do not start Day 04 if PathChecker is unreliable.

---

## 2. Day 04 Scope

Day 04 includes:

```text
Multiple arrows in one level
Arrow-to-arrow blocking
Correct ArrowsRemaining count
Clear order puzzle logic
Win only after all arrows are removed
Several manual test levels
Direction animation matching
```

Day 04 does not include:

```text
JSON loading
LevelSelect
Coins
Hints
Undo
AdMob
Locks
Color gates
Portals
```

---

## 3. Core Puzzle Principle

A real level works like this:

```text
Some arrows are immediately clear
Some arrows are blocked by other arrows
Player must remove clear arrows first
Removed arrows open paths for blocked arrows
All arrows removed = level complete
```

Bad puzzle:

```text
No arrow can move first
```

Good puzzle:

```text
At least one arrow can move first
Every removed arrow creates progress
```

---

## 4. Required Objects

Confirm these objects exist:

```text
Arrow
Blocker
PathChecker
BoardBackground
LevelText
MistakeText
MoveText
RestartButton
WinLayer
LoseLayer
```

---

## 5. Required Variables

### GameScene Variables

```text
ArrowsRemaining
Mistakes
Moves
InputLocked
PathBlocked
SelectedArrowID
LevelCompleted
LevelFailed
MoveSpeed
```

### Arrow Variables

```text
ArrowID
GridX
GridY
Direction
IsMoving
IsRemoved
```

---

## 6. Update Scene Start Event

For Day 04, replace the one-arrow test level with a multi-arrow manual level.

Reset variables:

```text
Set Mistakes = 0
Set Moves = 0
Set ArrowsRemaining = 3
Set LevelCompleted = 0
Set LevelFailed = 0
Set InputLocked = 0
Set PathBlocked = 0
Hide WinLayer
Hide LoseLayer
```

---

## 7. Manual Test Level 1 — Vertical Chain

This level teaches arrow-to-arrow blocking.

Create 3 arrows in the same column:

```text
Arrow 1: GridX=2, GridY=2, Direction=up
Arrow 2: GridX=2, GridY=3, Direction=up
Arrow 3: GridX=2, GridY=4, Direction=up
```

Pixel positions:

```text
Arrow 1: X=264, Y=412
Arrow 2: X=264, Y=508
Arrow 3: X=264, Y=604
```

Correct solution:

```text
Tap Arrow 1 first
Then Arrow 2
Then Arrow 3
```

Expected behavior:

```text
Arrow 3 is blocked until Arrow 1 and Arrow 2 are removed
Arrow 2 is blocked until Arrow 1 is removed
Arrow 1 can escape immediately
```

---

## 8. Create Arrow 1

At scene start:

```text
Create Arrow at X=264, Y=412
Set Arrow.ArrowID = 1
Set Arrow.GridX = 2
Set Arrow.GridY = 2
Set Arrow.Direction = up
Set Arrow.IsMoving = 0
Set Arrow.IsRemoved = 0
Set Arrow animation = ArrowUp
```

---

## 9. Create Arrow 2

At scene start:

```text
Create Arrow at X=264, Y=508
Set Arrow.ArrowID = 2
Set Arrow.GridX = 2
Set Arrow.GridY = 3
Set Arrow.Direction = up
Set Arrow.IsMoving = 0
Set Arrow.IsRemoved = 0
Set Arrow animation = ArrowUp
```

---

## 10. Create Arrow 3

At scene start:

```text
Create Arrow at X=264, Y=604
Set Arrow.ArrowID = 3
Set Arrow.GridX = 2
Set Arrow.GridY = 4
Set Arrow.Direction = up
Set Arrow.IsMoving = 0
Set Arrow.IsRemoved = 0
Set Arrow animation = ArrowUp
```

---

## 11. Critical PathChecker Rule for Multiple Arrows

When checking arrow collision:

```text
PathChecker collides with Arrow
AND Arrow.ArrowID != SelectedArrowID
```

Then:

```text
PathBlocked = 1
```

This prevents the selected arrow from blocking itself.

Even if PathChecker formulas are correct, keep this ID protection.

---

## 12. Successful Move With Multiple Arrows

When one arrow escapes:

```text
Delete escaped Arrow
ArrowsRemaining -= 1
InputLocked = 0
```

Then check:

```text
If ArrowsRemaining <= 0 → WinLayer
Else → continue gameplay
```

Do not show WinLayer after the first arrow unless it was the last arrow.

---

## 13. Input Locking With Multiple Arrows

For MVP, only one arrow moves at a time.

When arrow starts moving:

```text
InputLocked = 1
```

When arrow is deleted:

```text
If ArrowsRemaining > 0:
  InputLocked = 0
```

If the level is completed:

```text
InputLocked remains 1
```

Reason:

```text
This prevents multiple arrow deletes in the same moment and keeps logic stable.
```

---

## 14. Test: Wrong Order

Using Vertical Chain level:

Tap Arrow 3 first.

Expected:

```text
Arrow 3 does not move
Mistakes = 1
Moves = 1
```

Tap Arrow 2 next.

Expected:

```text
Arrow 2 does not move
Mistakes = 2
Moves = 2
```

Tap Arrow 1.

Expected:

```text
Arrow 1 moves up and exits
ArrowsRemaining = 2
WinLayer does not appear yet
```

---

## 15. Test: Correct Order

Using Vertical Chain level:

```text
Tap Arrow 1
Tap Arrow 2
Tap Arrow 3
```

Expected:

```text
Arrow 1 escapes
Arrow 2 escapes
Arrow 3 escapes
ArrowsRemaining = 0
WinLayer appears
```

---

## 16. Manual Test Level 2 — Horizontal Chain

After Vertical Chain works, test right direction.

Create 3 right-facing arrows:

```text
Arrow 1: GridX=4, GridY=3, Direction=right
Arrow 2: GridX=3, GridY=3, Direction=right
Arrow 3: GridX=2, GridY=3, Direction=right
```

Pixel positions:

```text
Arrow 1: X=456, Y=508
Arrow 2: X=360, Y=508
Arrow 3: X=264, Y=508
```

Correct solution:

```text
Tap Arrow 1 first
Then Arrow 2
Then Arrow 3
```

Expected:

```text
Rightmost arrow exits first
Then the middle arrow
Then the leftmost arrow
```

---

## 17. Manual Test Level 3 — Mixed Directions

Create a small mixed-direction puzzle:

```text
Arrow 1: GridX=1, GridY=2, Direction=left
Arrow 2: GridX=4, GridY=2, Direction=right
Arrow 3: GridX=2, GridY=4, Direction=up
Arrow 4: GridX=3, GridY=5, Direction=down
```

Correct behavior:

```text
All arrows should be able to escape if their paths are clear.
No false blocking should happen across unrelated rows/columns.
```

This level checks that PathChecker rectangles are not too large.

---

## 18. Manual Test Level 4 — Blocker + Arrows

Create:

```text
Arrow 1: GridX=2, GridY=4, Direction=up
Arrow 2: GridX=3, GridY=4, Direction=up
Blocker 1: GridX=2, GridY=2
```

Expected:

```text
Arrow 1 is blocked by Blocker 1
Arrow 2 should move if its path is clear
```

This confirms blocker collision and arrow collision can coexist.

---

## 19. Direction Animation Rule

When creating arrows, set animation by direction:

```text
up    → animation 0
right → animation 1
down  → animation 2
left  → animation 3
```

If temporary graphics are used, still keep the direction variable correct.

---

## 20. UI Rules With Multiple Arrows

MoveText updates after every tap:

```text
Moves: 0
Moves: 1
Moves: 2
```

MistakeText updates only after failed moves:

```text
Mistakes: 0/3
Mistakes: 1/3
Mistakes: 2/3
```

WinLayer appears only after:

```text
ArrowsRemaining <= 0
```

---

## 21. Common Problems

### Problem: WinLayer appears after first arrow

Check:

```text
ArrowsRemaining is set to correct number at scene start
ArrowsRemaining subtracts only once per deleted arrow
Win condition checks ArrowsRemaining <= 0
```

---

### Problem: Wrong arrow is deleted

Check:

```text
Movement events pick only Arrow where IsMoving = 1
Do not delete all Arrow objects at once
Delete only the moving arrow outside screen
```

---

### Problem: All arrows start moving

Check:

```text
Tap event modifies only selected Arrow instance
GDevelop object picking conditions are correct
Arrow.IsMoving is changed only for tapped Arrow
```

---

### Problem: PathChecker sees arrows outside the path

Check:

```text
PathChecker width and height
PathChecker X and Y
Direction-specific formula
Collision mask size
```

---

### Problem: Selected arrow blocks itself

Check:

```text
PathChecker does not overlap selected Arrow
Arrow collision condition uses ArrowID != SelectedArrowID
SelectedArrowID is set before collision check
```

---

## 22. Day 04 Acceptance Test

Day 04 is complete only when all checks pass:

- [ ] Scene can create at least 3 arrows
- [ ] Each arrow has unique ArrowID
- [ ] ArrowsRemaining starts with correct value
- [ ] One arrow can block another arrow
- [ ] Removing an arrow opens the path for another
- [ ] Wrong order increases Mistakes
- [ ] Correct order completes the level
- [ ] WinLayer appears only after all arrows are removed
- [ ] Movement works for vertical chain
- [ ] Movement works for horizontal chain
- [ ] Mixed directions do not falsely block each other
- [ ] Blockers and arrows both block movement correctly
- [ ] Restart recreates all arrows correctly
- [ ] No arrow is deleted twice
- [ ] No crash after multiple restarts

---

## 23. After Day 04

Next file to follow:

```text
docs/day_05_level_select_and_progress.md
```

Day 05 goal:

```text
Add LevelSelect and save unlocked level progress locally.
```

---

## 24. Critical Rule

Multiple-arrow logic must be stable before level loading.

If manual multi-arrow levels do not work, JSON level loading will only make debugging harder.
