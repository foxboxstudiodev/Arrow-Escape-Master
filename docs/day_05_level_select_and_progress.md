# Arrow Escape Master — Day 05 Level Select and Progress

This document defines Day 05 tasks for **Arrow Escape Master** in GDevelop.

Day 05 goal:

```text
Add a LevelSelect scene, unlock progress, save/load local player progress, and allow the player to choose unlocked levels.
```

This phase converts the game from a single manual prototype into a structured level-based mobile game.

---

## 1. Required Before Day 05

Day 04 must already be complete:

- [ ] Multiple arrows work correctly
- [ ] Arrows can block each other
- [ ] Removing arrows opens paths
- [ ] ArrowsRemaining is accurate
- [ ] WinLayer appears only after all arrows are removed
- [ ] Restart recreates the level correctly
- [ ] Basic MainMenu exists
- [ ] GameScene works

Do not start Day 05 if multi-arrow logic is unstable.

---

## 2. Day 05 Scope

Day 05 includes:

```text
LevelSelect scene
10 manual level buttons
UnlockedLevel global variable
CurrentLevel global variable
Local storage save/load
MainMenu Play button continues latest unlocked level
Level buttons open selected level
Locked buttons are disabled
Progress saves after level win
```

Day 05 does not include:

```text
Full JSON level loading
AdMob
Coins economy finalization
Hints
Undo
Skins
Advanced gates
Play Store upload
```

---

## 3. Global Variables

Confirm these project/global variables exist:

```text
CurrentLevel = 1
UnlockedLevel = 1
Coins = 0
CompletedLevels = 0
SoundEnabled = 1
VibrationEnabled = 1
AdsRemoved = 0
```

For Day 05, required variables are:

```text
CurrentLevel
UnlockedLevel
CompletedLevels
```

---

## 4. Storage Keys

Use these exact storage keys:

```text
CurrentLevel
UnlockedLevel
CompletedLevels
Coins
SoundEnabled
VibrationEnabled
AdsRemoved
```

Do not rename these keys after release unless migration is added.

---

## 5. MainMenu Update

MainMenu must have these objects:

```text
GameTitleText
PlayButton
LevelSelectButton
SettingsButton
```

For Day 05, required:

```text
PlayButton
LevelSelectButton
```

---

## 6. MainMenu Scene Start Logic

At the beginning of `MainMenu`:

```text
Read UnlockedLevel from storage
Read CurrentLevel from storage
Read CompletedLevels from storage
If UnlockedLevel <= 0, set UnlockedLevel = 1
If CurrentLevel <= 0, set CurrentLevel = 1
```

Important:

```text
First launch must always start with Level 1 unlocked.
```

---

## 7. MainMenu Play Button Logic

When player taps `PlayButton`:

```text
Set CurrentLevel = UnlockedLevel
Change scene to GameScene
```

Meaning:

```text
PLAY continues from the latest unlocked level.
```

Alternative later:

```text
PLAY continues LastPlayedLevel
```

For Day 05, use:

```text
CurrentLevel = UnlockedLevel
```

---

## 8. MainMenu LevelSelect Button Logic

When player taps `LevelSelectButton`:

```text
Change scene to LevelSelect
```

---

## 9. Create LevelSelect Scene

Create new scene:

```text
LevelSelect
```

Purpose:

```text
Show available levels and allow player to choose unlocked levels.
```

Required objects:

```text
LevelSelectTitleText
BackButton
LevelButton01
LevelButton02
LevelButton03
LevelButton04
LevelButton05
LevelButton06
LevelButton07
LevelButton08
LevelButton09
LevelButton10
```

Optional objects:

```text
LockedIcon01
LockedIcon02
CompletedIcon01
CompletedIcon02
```

For Day 05, text buttons are acceptable.

---

## 10. Level Button Layout

Recommended 2-column layout:

```text
LevelButton01: X=130, Y=250
LevelButton02: X=390, Y=250
LevelButton03: X=130, Y=370
LevelButton04: X=390, Y=370
LevelButton05: X=130, Y=490
LevelButton06: X=390, Y=490
LevelButton07: X=130, Y=610
LevelButton08: X=390, Y=610
LevelButton09: X=130, Y=730
LevelButton10: X=390, Y=730
```

Button size:

```text
200 x 90
```

BackButton:

```text
X=40, Y=1120
```

---

## 11. LevelSelect Scene Start Logic

At the beginning of `LevelSelect`:

```text
Read UnlockedLevel from storage
If UnlockedLevel <= 0, set UnlockedLevel = 1
Update level button states
```

Button state logic:

```text
If button level number <= UnlockedLevel:
  Show as unlocked
Else:
  Show as locked
```

For Day 05, locked can be shown by changing text:

```text
Level 5
Locked
```

or by reducing opacity.

---

## 12. Level Button Tap Logic

For each button:

Example: LevelButton01

Conditions:

```text
Cursor/touch is on LevelButton01
Left mouse button released OR touch released
UnlockedLevel >= 1
```

Actions:

```text
Set CurrentLevel = 1
Write CurrentLevel to storage
Change scene to GameScene
```

Example: LevelButton05

Conditions:

```text
Cursor/touch is on LevelButton05
Left mouse button released OR touch released
UnlockedLevel >= 5
```

Actions:

```text
Set CurrentLevel = 5
Write CurrentLevel to storage
Change scene to GameScene
```

If locked:

```text
Do nothing
or show Locked message
```

---

## 13. BackButton Logic

In `LevelSelect`:

Conditions:

```text
Cursor/touch is on BackButton
Left mouse button released OR touch released
```

Action:

```text
Change scene to MainMenu
```

---

## 14. GameScene Start Logic Update

At the beginning of `GameScene`:

```text
Read CurrentLevel from storage
If CurrentLevel <= 0, set CurrentLevel = 1
Set LevelID = CurrentLevel
Set LevelText = "Level " + CurrentLevel
Load level based on CurrentLevel
```

For Day 05, levels may still be loaded manually with conditions:

```text
If CurrentLevel = 1: create manual Level 1
If CurrentLevel = 2: create manual Level 2
If CurrentLevel = 3: create manual Level 3
...
If CurrentLevel = 10: create manual Level 10
```

JSON loading comes later.

---

## 15. Manual Level Loading Rule

For Day 05, create separate event groups:

```text
LoadLevel01
LoadLevel02
LoadLevel03
LoadLevel04
LoadLevel05
LoadLevel06
LoadLevel07
LoadLevel08
LoadLevel09
LoadLevel10
```

Each group must:

```text
Delete old Arrow and Blocker objects
Create arrows and blockers
Set ArrowsRemaining correctly
Set MistakeLimit
Set RewardCoins if used
Set LevelText
Reset Mistakes and Moves
Hide WinLayer
Hide LoseLayer
```

---

## 16. Progress Save After Win

When level is completed:

```text
If CurrentLevel >= UnlockedLevel:
  Set UnlockedLevel = CurrentLevel + 1

If UnlockedLevel > 10:
  Set UnlockedLevel = 10

Add 1 to CompletedLevels
Write UnlockedLevel to storage
Write CurrentLevel to storage
Write CompletedLevels to storage
```

For a 10-level prototype, cap:

```text
UnlockedLevel <= 10
```

Later when 50 levels exist, cap becomes:

```text
UnlockedLevel <= 50
```

---

## 17. NextButton Logic Update

When player taps `NextButton`:

```text
If CurrentLevel < 10:
  Add 1 to CurrentLevel
  Write CurrentLevel to storage
  Restart GameScene
Else:
  Change scene to LevelSelect
```

For production with 50 levels:

```text
If CurrentLevel < 50:
  CurrentLevel += 1
Else:
  show Coming Soon or LevelSelect
```

---

## 18. ReplayButton Logic

When player taps `ReplayButton`:

```text
Restart GameScene
```

Do not change CurrentLevel.

---

## 19. RestartButton Logic

When player taps `RestartButton` or `RestartLoseButton`:

```text
Restart GameScene
```

Do not change CurrentLevel.

---

## 20. Locked Level Feedback

If player taps a locked level:

```text
Show text: Level locked
```

Optional scene variable:

```text
LockedMessageTimer
```

For Day 05, locked buttons can simply do nothing.

---

## 21. Testing First Launch

Clear storage or install fresh build.

Expected:

```text
UnlockedLevel = 1
CurrentLevel = 1
Only Level 1 is unlocked
PLAY starts Level 1
```

---

## 22. Testing Unlock Progress

Complete Level 1.

Expected:

```text
UnlockedLevel = 2
Level 2 becomes available in LevelSelect
NextButton opens Level 2
```

Complete Level 2.

Expected:

```text
UnlockedLevel = 3
Level 3 becomes available
```

---

## 23. Testing Save After Closing Game

Steps:

```text
Complete Level 1
Close the game
Open the game again
Open LevelSelect
```

Expected:

```text
Level 2 is still unlocked
Progress was saved
```

---

## 24. Testing Replay Completed Level

Steps:

```text
Unlock Level 3
Open LevelSelect
Tap Level 1
Complete Level 1 again
```

Expected:

```text
UnlockedLevel stays at least 3
Progress must not go backward
```

Rule:

```text
Never reduce UnlockedLevel.
```

---

## 25. Common Problems

### Problem: Progress resets after reopening game

Check:

```text
Storage write action exists
Storage read action exists
Storage key names match exactly
Game uses GlobalVariable(UnlockedLevel), not only scene variable
```

---

### Problem: All levels are unlocked immediately

Check:

```text
UnlockedLevel default is 1
Button condition uses level <= UnlockedLevel
Debug values are not left at 10
```

---

### Problem: NextButton skips levels

Check:

```text
NextButton adds exactly 1 to CurrentLevel
Button event triggers once only
Use mouse released / touch released
```

---

### Problem: Completed old level resets progress backward

Check:

```text
Use condition: If CurrentLevel >= UnlockedLevel
Only then set UnlockedLevel = CurrentLevel + 1
Do not set UnlockedLevel = CurrentLevel always
```

---

## 26. Day 05 Acceptance Test

Day 05 is complete only when all checks pass:

- [ ] LevelSelect scene exists
- [ ] MainMenu has LevelSelect button
- [ ] LevelSelect has 10 level buttons
- [ ] Only Level 1 is unlocked on first launch
- [ ] Locked levels cannot be opened
- [ ] Level 1 opens GameScene
- [ ] CurrentLevel is set correctly
- [ ] GameScene shows correct LevelText
- [ ] Completing Level 1 unlocks Level 2
- [ ] NextButton opens next level
- [ ] Progress saves after app restart
- [ ] Replaying old level does not reduce progress
- [ ] Restart does not change CurrentLevel
- [ ] BackButton returns to MainMenu
- [ ] No crash when moving between scenes

---

## 27. After Day 05

Next file to follow:

```text
docs/day_06_json_level_loading.md
```

Day 06 goal:

```text
Replace manual level creation with structured level loading based on levels/levels.json.
```

---

## 28. Critical Rule

Progress must never move backward.

If the player unlocks Level 5, replaying Level 1 must not lock Levels 2–5 again.
