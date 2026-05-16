# Arrow Escape Master — Day 11 50 Level Expansion

This document defines Day 11 tasks for **Arrow Escape Master** in GDevelop.

Day 11 goal:

```text
Expand the game from 10 prototype levels to 50 release-ready levels with a fair difficulty curve, solvability checks, and clean level progression.
```

The first public release must feel like a complete small game, not a demo.

---

## 1. Required Before Day 11

Day 10 must already be complete or stable enough:

- [ ] Core gameplay works
- [ ] PathChecker works
- [ ] Multiple arrows work
- [ ] LevelSelect works
- [ ] Save/load progress works
- [ ] Coins/hints/undo/extra chance are stable or safely deferred
- [ ] UI is readable
- [ ] Temporary visuals are replaced or acceptable for internal testing
- [ ] Existing 10 levels are playable

Do not create 50 levels if the first 10 levels are still unstable.

---

## 2. Day 11 Scope

Day 11 includes:

```text
50-level content plan
Difficulty curve
Level groups
Level design rules
Level solvability checks
Manual testing process
RewardCoins balancing
MistakeLimit balancing
LevelSelect extension from 10 to 50
levels.json expansion from 10 to 50
```

Day 11 does not include:

```text
Play Store upload
Final AAB export
Production ad IDs
Advanced analytics
Cloud save
Daily challenge
Leaderboard
```

---

## 3. First Release Level Target

First public release target:

```text
50 playable levels
```

Minimum internal test target:

```text
10 levels
```

MVP candidate target:

```text
50 levels
```

Do not publish public version with fewer than 50 levels unless the game is clearly labeled as early/internal test only.

---

## 4. Level Groups

Use this structure:

```text
Levels 1–10: Tutorial / Easy
Levels 11–20: Easy+
Levels 21–30: Normal
Levels 31–40: Normal+
Levels 41–50: Hard / Boss-style
```

Every 10th level should feel slightly more important:

```text
Level 10: First boss order
Level 20: Bigger chain puzzle
Level 30: Mixed direction challenge
Level 40: Blocker-heavy challenge
Level 50: Final MVP boss puzzle
```

---

## 5. Difficulty Curve

### Levels 1–10 — Tutorial / Easy

Purpose:

```text
Teach arrow movement, path blocking, and order logic.
```

Rules:

```text
1–10 arrows
0–2 blockers
No locks
No portals
No color gates
MistakeLimit = 3
RewardCoins = 10–20
```

Player should understand the game without reading instructions.

---

### Levels 11–20 — Easy+

Purpose:

```text
Introduce longer chains and simple blockers.
```

Rules:

```text
8–14 arrows
1–4 blockers
Simple row/column chains
Few mixed directions
MistakeLimit = 3
RewardCoins = 14–22
```

---

### Levels 21–30 — Normal

Purpose:

```text
Create real puzzle ordering.
```

Rules:

```text
12–18 arrows
2–5 blockers
Mixed directions
Several wrong-order traps
MistakeLimit = 3
RewardCoins = 18–26
```

---

### Levels 31–40 — Normal+

Purpose:

```text
Increase planning depth without becoming unfair.
```

Rules:

```text
16–24 arrows
4–7 blockers
More compact boards
More dependencies between arrows
MistakeLimit = 3 or 2
RewardCoins = 22–32
```

---

### Levels 41–50 — Hard / Boss-style

Purpose:

```text
Make the end of MVP feel challenging and satisfying.
```

Rules:

```text
20–30 arrows
5–9 blockers
Multi-step ordering
Several dependent chains
MistakeLimit = 2 or 3
RewardCoins = 30–45
```

Hard does not mean random or unfair.

---

## 6. Level Design Rule

Every level must satisfy this rule:

```text
At least one legal first move exists.
```

Every solved move should create progress:

```text
A removed arrow opens a path or reduces puzzle complexity.
```

Bad level:

```text
All arrows permanently block each other.
No starting move.
Solution requires guessing invisible rules.
```

Good level:

```text
There is a visible first move.
Wrong choices are understandable.
Correct order is learnable.
```

---

## 7. Object Count Guidelines

Use this as a balancing guide:

| Level Range | Arrow Count | Blocker Count | Mistake Limit |
|---|---:|---:|---:|
| 1–10 | 1–10 | 0–2 | 3 |
| 11–20 | 8–14 | 1–4 | 3 |
| 21–30 | 12–18 | 2–5 | 3 |
| 31–40 | 16–24 | 4–7 | 2–3 |
| 41–50 | 20–30 | 5–9 | 2–3 |

Do not overload early levels.

---

## 8. RewardCoins Balancing

Recommended reward table:

| Level Range | RewardCoins |
|---|---:|
| 1–10 | 10–20 |
| 11–20 | 14–22 |
| 21–30 | 18–26 |
| 31–40 | 22–32 |
| 41–50 | 30–45 |

Boss level rewards:

```text
Level 10: 20 coins
Level 20: 24 coins
Level 30: 30 coins
Level 40: 36 coins
Level 50: 50 coins
```

---

## 9. MistakeLimit Balancing

Default:

```text
MistakeLimit = 3
```

Use `MistakeLimit = 2` only when:

```text
The level is visually clear
There are not too many traps
The level is later than Level 30
```

Do not use `MistakeLimit = 1` in first release.

Reason:

```text
It creates frustration and pushes users to uninstall.
```

---

## 10. Level 1–10 Status

Existing first 10 levels:

```text
Level 1 — First Arrow
Level 2 — Two Ways Out
Level 3 — Simple Chain
Level 4 — Right Chain
Level 5 — Open Board
Level 6 — Cross Order
Level 7 — Twin Columns
Level 8 — Split Rows
Level 9 — Double Chain
Level 10 — First Boss Order
```

Task:

```text
Review and test these 10 levels before adding 11–50.
```

---

## 11. Level 11–20 Plan

Design target:

```text
Simple dependency puzzles with more arrows.
```

Suggested names:

```text
Level 11 — Soft Block
Level 12 — Open Corners
Level 13 — Two Chains
Level 14 — Side Escape
Level 15 — Center Split
Level 16 — Four Lanes
Level 17 — Calm Trap
Level 18 — Arrow Bridge
Level 19 — Narrow Choice
Level 20 — Second Boss Order
```

---

## 12. Level 21–30 Plan

Design target:

```text
Normal puzzle flow with mixed directions and blocker traps.
```

Suggested names:

```text
Level 21 — Mixed Start
Level 22 — Hidden Order
Level 23 — Crossed Paths
Level 24 — Double Lane
Level 25 — Middle Lockdown
Level 26 — Clean Exit
Level 27 — Broken Chain
Level 28 — Direction Test
Level 29 — Last Lane
Level 30 — Third Boss Order
```

---

## 13. Level 31–40 Plan

Design target:

```text
Harder dependency ordering, still fair.
```

Suggested names:

```text
Level 31 — Tight Board
Level 32 — Long Decision
Level 33 — Side Pressure
Level 34 — Blocker Field
Level 35 — Narrow Split
Level 36 — Smart Chain
Level 37 — Trap Row
Level 38 — Center Escape
Level 39 — Final Opening
Level 40 — Fourth Boss Order
```

---

## 14. Level 41–50 Plan

Design target:

```text
Hardest MVP content with boss-style endings.
```

Suggested names:

```text
Level 41 — Deep Order
Level 42 — Heavy Cross
Level 43 — Last Mistake
Level 44 — Twin Traps
Level 45 — Pressure Board
Level 46 — Long Escape
Level 47 — Broken Center
Level 48 — Edge Control
Level 49 — Master Path
Level 50 — Arrow Escape Master
```

---

## 15. Level Creation Workflow

For every new level:

```text
1. Sketch level on 6x8 grid
2. Mark all arrows and directions
3. Mark blockers
4. Identify first legal move
5. Write solution order
6. Add level to levels.json
7. Load level in GDevelop
8. Test wrong orders
9. Test correct solution
10. Confirm win condition
```

Do not add a level without a known solution order.

---

## 16. Solution Order Requirement

For every level, store a private solution note during development.

Recommended format:

```text
Level 15 solution:
ArrowID 3 → ArrowID 1 → ArrowID 4 → ArrowID 2 → ArrowID 5
```

Optional file later:

```text
levels/solutions_internal.md
```

Do not show solutions inside the public game.

---

## 17. Solvability Checklist

For every level:

- [ ] At least one first move exists
- [ ] Correct solution is known
- [ ] All arrows can eventually escape
- [ ] No object is outside board bounds
- [ ] No duplicate cells exist
- [ ] Direction values are valid
- [ ] ArrowsRemaining matches arrow count
- [ ] MistakeLimit is fair
- [ ] RewardCoins is assigned
- [ ] Level difficulty matches placement

---

## 18. LevelSelect Expansion

Update `LevelSelect` from 10 to 50 buttons.

Recommended pages:

```text
Page 1: Levels 1–10
Page 2: Levels 11–20
Page 3: Levels 21–30
Page 4: Levels 31–40
Page 5: Levels 41–50
```

Do not place 50 tiny buttons on one screen.

Use:

```text
NextPageButton
PreviousPageButton
LevelPageNumber
```

Scene variable:

```text
LevelSelectPage = 1
```

---

## 19. LevelSelect Page Logic

Page 1:

```text
Buttons represent levels 1–10
```

Page 2:

```text
Buttons represent levels 11–20
```

Formula:

```text
DisplayedLevelNumber = (LevelSelectPage - 1) * 10 + ButtonIndex
```

Example:

```text
Page 3, Button 4 → Level 24
```

---

## 20. levels.json Expansion Rule

When adding levels 11–50 to `levels/levels.json`, keep the exact structure:

```json
{
  "id": 11,
  "name": "Soft Block",
  "difficulty": "easy",
  "board": { "width": 6, "height": 8 },
  "mistakeLimit": 3,
  "moveLimit": null,
  "rewardCoins": 14,
  "arrows": [],
  "blockers": [],
  "gates": [],
  "portals": []
}
```

Do not add inconsistent field names.

---

## 21. JSON Validation Before Build

Before exporting build, validate `levels.json`:

```text
Valid JSON syntax
50 levels present
IDs 1–50 exist
No duplicate IDs
Each level has arrows
Every arrow has id/x/y/direction
Every blocker has id/x/y/type
No invalid direction values
No object outside board
```

---

## 22. Testing Plan for 50 Levels

Test in batches:

```text
Batch 1: Levels 1–10
Batch 2: Levels 11–20
Batch 3: Levels 21–30
Batch 4: Levels 31–40
Batch 5: Levels 41–50
```

For each batch:

```text
Test correct solution
Test one wrong order
Test restart
Test next level
Test LevelSelect opening
```

---

## 23. Difficulty Review

After all 50 levels are created, review:

```text
Are first 5 levels too hard?
Are middle levels too repetitive?
Are late levels fair?
Are there too many blockers?
Does every boss level feel different?
```

Adjust before release.

---

## 24. Common Problems

### Problem: Level is impossible

Fix:

```text
Add a legal first move
Remove one blocker
Change one arrow direction
Move one arrow to open chain
```

---

### Problem: Level is too easy for late game

Fix:

```text
Add dependency chain
Add blocker
Add mixed direction trap
Reduce mistake limit from 3 to 2 only if fair
```

---

### Problem: LevelSelect is crowded

Fix:

```text
Use pages of 10 levels
Use larger buttons
Do not show all 50 at once
```

---

### Problem: User gets stuck too early

Fix:

```text
Simplify Levels 1–10
Add clearer arrow order
Use more open board
Do not punish with low mistake limit
```

---

## 25. Day 11 Acceptance Test

Day 11 is complete only when all checks pass:

- [ ] 50-level plan exists
- [ ] Difficulty curve is defined
- [ ] Levels 1–10 are reviewed
- [ ] Levels 11–50 have planned names and roles
- [ ] Level creation workflow is defined
- [ ] Solvability checklist is defined
- [ ] LevelSelect 50-level page plan exists
- [ ] levels.json expansion rule is defined
- [ ] Testing batches are defined
- [ ] No public release level is impossible
- [ ] All release levels have known solution order before publishing

---

## 26. After Day 11

Next file to follow:

```text
docs/day_12_android_build_export.md
```

Day 12 goal:

```text
Export Android APK/AAB from GDevelop, verify package settings, versioning, signing, and real-device install.
```

---

## 27. Critical Rule

Do not compensate bad level design with ads, hints, or extra chances.

A fair puzzle must be solvable by logic.
