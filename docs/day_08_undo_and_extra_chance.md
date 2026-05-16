# Arrow Escape Master — Day 08 Undo and Extra Chance

This document defines Day 08 tasks for **Arrow Escape Master** in GDevelop.

Day 08 goal:

```text
Add Undo flow and Extra Chance flow so the player can recover from mistakes without breaking level logic.
```

This phase improves player retention and prepares the game for rewarded ads in Day 09.

---

## 1. Required Before Day 08

Day 07 must already be complete:

- [ ] Coins work
- [ ] CoinText updates correctly
- [ ] Coins save/load from storage
- [ ] Level win rewards coins once
- [ ] HintButton exists
- [ ] Hint cost does not allow negative coins
- [ ] WinLayer reward text works
- [ ] Basic gameplay remains stable

Do not add Undo or Extra Chance if coin and win reward logic is unstable.

---

## 2. Day 08 Scope

Day 08 includes:

```text
UndoButton
Undo cost
Undo placeholder or single-step restore
Previous move state concept
ExtraChanceButton
ExtraChanceUsed flag
Continue after losing
Coin-based extra chance placeholder
Rewarded-ad-ready structure
```

Day 08 does not include:

```text
Real AdMob rewarded ads
Full replay history
Cloud save
In-app purchase
Analytics
```

---

## 3. Required Global Variables

Confirm these global variables exist:

```text
Coins
CurrentLevel
UnlockedLevel
```

---

## 4. Required GameScene Variables

Create or confirm these scene variables:

```text
UndoCost = 30
CanUndo = 0
UndoUsedThisMove = 0
PreviousMoveSaved = 0
PreviousArrowID = 0
PreviousArrowGridX = 0
PreviousArrowGridY = 0
PreviousArrowDirection = none
PreviousMistakes = 0
PreviousMoves = 0
PreviousArrowsRemaining = 0
ExtraChanceUsed = 0
ExtraChanceCost = 50
```

For MVP, required:

```text
UndoCost
CanUndo
PreviousMoveSaved
ExtraChanceUsed
ExtraChanceCost
```

---

## 5. Required UI Objects

Create on `UILayer`:

```text
UndoButton
UndoMessageText
```

Create on `LoseLayer`:

```text
ExtraChanceButton
```

Recommended positions:

```text
UndoButton: X=480, Y=1120
UndoMessageText: X=120, Y=1040
ExtraChanceButton: center below LoseText
```

---

## 6. Undo Design Decision

There are two possible Undo versions.

### Version A — Placeholder Undo

```text
UndoButton checks coins and shows message, but does not restore level yet.
```

Use only if real undo is too complex during MVP.

### Version B — Single-Step Undo

```text
Before a successful move, save the selected arrow state.
If player taps Undo, recreate the removed arrow and restore counters.
```

Recommended target:

```text
Version B — Single-Step Undo
```

But only one previous move is stored.

---

## 7. Single-Step Undo Rule

Undo should restore only the last successful removed arrow.

It does not restore:

```text
Multiple earlier moves
Coins spent on hints
Level progress after win
Ad states
```

MVP rule:

```text
Undo is available only while level is active and before win/lose.
```

---

## 8. Save Previous Move State

Before a clear arrow starts moving, save its data:

```text
PreviousArrowID = Arrow.ArrowID
PreviousArrowGridX = Arrow.GridX
PreviousArrowGridY = Arrow.GridY
PreviousArrowDirection = Arrow.Direction
PreviousMistakes = Mistakes
PreviousMoves = Moves
PreviousArrowsRemaining = ArrowsRemaining
PreviousMoveSaved = 1
CanUndo = 1
UndoUsedThisMove = 0
```

Important:

```text
Save state before changing Moves or deleting Arrow.
```

---

## 9. Undo Button Flow

When player taps `UndoButton`:

Conditions:

```text
LevelCompleted = 0
LevelFailed = 0
InputLocked = 0
CanUndo = 1
PreviousMoveSaved = 1
```

Then check coins:

```text
If Coins >= UndoCost:
  Spend coins
  Restore previous move
Else:
  Show Not enough coins message
```

---

## 10. Undo Coin Logic

If player has enough coins:

```text
Subtract UndoCost from Coins
If Coins < 0, set Coins = 0
Write Coins to storage
Update CoinText
```

If not enough coins:

```text
Show UndoMessageText = "Not enough coins"
Do not restore state
Do not change Coins
```

---

## 11. Restore Previous Move

To restore the last removed arrow:

```text
Create Arrow at previous grid position
Set Arrow.ArrowID = PreviousArrowID
Set Arrow.GridX = PreviousArrowGridX
Set Arrow.GridY = PreviousArrowGridY
Set Arrow.Direction = PreviousArrowDirection
Set Arrow.IsMoving = 0
Set Arrow.IsRemoved = 0
Set animation by PreviousArrowDirection
Set Arrow position using grid formula
Set Mistakes = PreviousMistakes
Set Moves = PreviousMoves
Set ArrowsRemaining = PreviousArrowsRemaining
Set CanUndo = 0
Set PreviousMoveSaved = 0
Update UI
```

Important:

```text
Undo restores the arrow only once.
```

---

## 12. Undo After Failed Move

MVP decision:

```text
Undo only restores successful removed arrows.
```

Failed move undo is not included in MVP.

Reason:

```text
Failed move does not change board layout, only counters. It is simpler to let Extra Chance handle mistakes.
```

---

## 13. Undo Restrictions

Disable Undo when:

```text
LevelCompleted = 1
LevelFailed = 1
InputLocked = 1
CanUndo = 0
PreviousMoveSaved = 0
```

Also disable Undo after using it once.

---

## 14. Extra Chance Design

Extra Chance appears after losing.

Flow:

```text
Player reaches MistakeLimit
↓
LoseLayer appears
↓
Player taps ExtraChanceButton
↓
If ExtraChanceUsed = 0:
  Continue level with one mistake slot restored
Else:
  Extra chance unavailable
```

Day 08 uses coin-based placeholder.

Day 09 will connect this to rewarded ads.

---

## 15. Extra Chance Variables

At scene start:

```text
ExtraChanceUsed = 0
ExtraChanceCost = 50
```

When player uses extra chance:

```text
ExtraChanceUsed = 1
```

---

## 16. ExtraChanceButton Flow — Coin Placeholder

When player taps `ExtraChanceButton`:

Conditions:

```text
LevelFailed = 1
ExtraChanceUsed = 0
```

Then:

```text
If Coins >= ExtraChanceCost:
  Subtract ExtraChanceCost from Coins
  Set Coins storage
  Set Mistakes = MistakeLimit - 1
  Set LevelFailed = 0
  Set InputLocked = 0
  Set ExtraChanceUsed = 1
  Hide LoseLayer
  Update MistakeText
  Update CoinText
Else:
  Show "Not enough coins"
```

---

## 17. Extra Chance With Rewarded Ads Later

Day 09 target:

```text
Tap ExtraChanceButton
↓
Show rewarded ad
↓
If ad completed:
  Continue level
Else:
  Stay on LoseLayer
```

Reward action:

```text
Mistakes = MistakeLimit - 1
LevelFailed = 0
InputLocked = 0
ExtraChanceUsed = 1
Hide LoseLayer
```

---

## 18. Extra Chance Limit

Only one extra chance per level attempt.

If player loses again after using extra chance:

```text
ExtraChanceButton disabled or hidden
Restart is the only option
```

Reason:

```text
Unlimited extra chances make puzzle difficulty meaningless.
```

---

## 19. UI Text Rules

UndoMessageText examples:

```text
Undo used
Not enough coins
Nothing to undo
```

ExtraChanceButton text:

```text
Extra Chance
```

If already used:

```text
Extra Chance Used
```

---

## 20. Testing Undo

Test scenario:

```text
Start with 100 coins
Complete one successful arrow move in multi-arrow level
Tap UndoButton
```

Expected:

```text
Coins decreases by 30
Last removed arrow returns
ArrowsRemaining is restored
Moves is restored
CanUndo becomes 0
```

Tap Undo again.

Expected:

```text
Nothing happens or message appears
No duplicate arrow is created
```

---

## 21. Testing Not Enough Coins for Undo

Set Coins to 10.

Tap UndoButton after successful move.

Expected:

```text
Coins remains 10
Arrow is not restored
Message: Not enough coins
```

---

## 22. Testing Extra Chance

Set Coins to 100.

Make 3 mistakes.

Expected:

```text
LoseLayer appears
```

Tap ExtraChanceButton.

Expected:

```text
Coins decreases by 50
LoseLayer hides
Mistakes becomes 2/3
Player can continue
ExtraChanceUsed = 1
```

Lose again.

Expected:

```text
ExtraChanceButton disabled or hidden
```

---

## 23. Common Problems

### Problem: Undo creates duplicate arrows

Check:

```text
CanUndo is set to 0 after undo
PreviousMoveSaved is set to 0 after undo
Undo event uses mouse released / trigger once
```

---

### Problem: Undo restores wrong arrow position

Check:

```text
PreviousArrowGridX
PreviousArrowGridY
BoardStartX
BoardStartY
CellSize
Position formula
```

---

### Problem: Extra Chance hides LoseLayer but player cannot move

Check:

```text
InputLocked is set to 0
LevelFailed is set to 0
LevelCompleted is still 0
```

---

### Problem: Extra Chance can be used repeatedly

Check:

```text
ExtraChanceUsed is set to 1
ExtraChanceButton condition requires ExtraChanceUsed = 0
```

---

## 24. Day 08 Acceptance Test

Day 08 is complete only when all checks pass:

- [ ] UndoButton exists
- [ ] UndoCost exists
- [ ] Previous move state is saved before successful move
- [ ] Undo restores last removed arrow
- [ ] Undo restores counters correctly
- [ ] Undo spends coins
- [ ] Undo cannot make coins negative
- [ ] Undo cannot be used twice for the same move
- [ ] Undo is disabled after win
- [ ] Undo is disabled after lose
- [ ] ExtraChanceButton exists
- [ ] ExtraChanceUsed exists
- [ ] Extra Chance continues level after lose
- [ ] Extra Chance sets Mistakes to MistakeLimit - 1
- [ ] Extra Chance can be used only once per attempt
- [ ] Extra Chance cannot make coins negative
- [ ] Restart resets ExtraChanceUsed

---

## 25. After Day 08

Next file to follow:

```text
docs/day_09_admob_integration.md
```

Day 09 goal:

```text
Connect rewarded ads to Hint, Extra Chance, and Double Reward; connect interstitial ads after safe gameplay points.
```

---

## 26. Critical Rule

Undo and Extra Chance must never corrupt the board state.

A recovered level must still be solvable and deterministic.
