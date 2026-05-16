# Arrow Escape Master — Day 07 Coins, Hints, and Rewards

This document defines Day 07 tasks for **Arrow Escape Master** in GDevelop.

Day 07 goal:

```text
Add coin rewards, basic hint logic, reward balancing, and level-completion economy for the first MVP.
```

This phase makes the game feel like a real mobile puzzle product instead of a raw gameplay prototype.

---

## 1. Required Before Day 07

Day 06 must already be stable:

- [ ] CurrentLevel works
- [ ] LevelSelect works
- [ ] Progress saves locally
- [ ] Levels 1–10 can be loaded manually or from structured data
- [ ] Multiple arrows work
- [ ] Blocked paths work
- [ ] Win/Lose logic works
- [ ] Restart and Next buttons work

Do not add economy systems if basic level flow is unstable.

---

## 2. Day 07 Scope

Day 07 includes:

```text
Coin balance
RewardCoins per level
Perfect bonus placeholder
Coin saving/loading
HintButton
Basic safe-arrow hint detection
Hint cost
Not enough coins behavior
Win reward display
Double reward placeholder
```

Day 07 does not include:

```text
Real AdMob rewarded ads
Undo state history
In-app purchases
Skins shop
Daily reward final system
Analytics
```

---

## 3. Required Global Variables

Confirm these global variables exist:

```text
Coins = 0
CompletedLevels = 0
CurrentLevel = 1
UnlockedLevel = 1
```

For Day 07, the most important variable is:

```text
Coins
```

---

## 4. Required GameScene Variables

Create or confirm these scene variables:

```text
RewardCoins = 10
PerfectBonusCoins = 5
RewardAlreadyGiven = 0
RewardAlreadyDoubled = 0
HintCost = 20
HintActive = 0
HintTargetArrowID = 0
NotEnoughCoinsTimer = 0
```

Optional later:

```text
DailyRewardAvailable = 0
ExtraChanceUsed = 0
```

---

## 5. Required UI Objects

Create these objects on `UILayer`:

```text
CoinText
HintButton
HintMessageText
```

Create these on `WinLayer`:

```text
CoinRewardText
DoubleRewardButton
```

For Day 07, `DoubleRewardButton` is a placeholder only.

Recommended positions:

```text
CoinText: X=500, Y=40
HintButton: X=260, Y=1120
HintMessageText: X=120, Y=1040
CoinRewardText: center inside WinLayer
DoubleRewardButton: below CoinRewardText
```

---

## 6. Load Coins at Game Start

At the beginning of `MainMenu` or `BootScene`:

```text
Read Coins from storage
If Coins < 0, set Coins = 0
Update MenuCoinText if it exists
```

If no stored value exists:

```text
Coins = 0
```

---

## 7. Update CoinText in GameScene

At the beginning of `GameScene`:

```text
Set CoinText = Coins
```

After any coin change:

```text
Update CoinText
Write Coins to storage
```

---

## 8. Set RewardCoins by Level Difficulty

If level data has `rewardCoins`, use it.

Example from `levels/levels.json`:

```text
Level 1 rewardCoins = 10
Level 5 rewardCoins = 12
Level 10 rewardCoins = 20
```

Manual fallback rule:

```text
Easy levels: RewardCoins = 10
Normal levels: RewardCoins = 14
Boss levels: RewardCoins = 20
```

---

## 9. Give Coins After Win

When win condition triggers:

Conditions:

```text
ArrowsRemaining <= 0
LevelCompleted = 0
LevelFailed = 0
RewardAlreadyGiven = 0
```

Actions:

```text
Set LevelCompleted = 1
Set InputLocked = 1
Add RewardCoins to Coins
Set RewardAlreadyGiven = 1
Write Coins to storage
Set CoinRewardText = "+" + RewardCoins + " coins"
Update CoinText
Show WinLayer
```

Important:

```text
RewardAlreadyGiven prevents duplicate coin rewards from the same win event.
```

---

## 10. Perfect Bonus Placeholder

Perfect bonus condition:

```text
Mistakes = 0
```

If perfect bonus is enabled:

```text
Add PerfectBonusCoins to Coins
Show text: Perfect +5
```

For MVP:

```text
Keep Perfect Bonus optional.
```

Do not overcomplicate reward animation yet.

---

## 11. Hint Button Basic Logic

When player taps `HintButton`:

If level is active:

```text
LevelCompleted = 0
LevelFailed = 0
InputLocked = 0
```

Then check coins:

```text
If Coins >= HintCost:
  Subtract HintCost from Coins
  Write Coins to storage
  Find safe arrow
  Highlight safe arrow
  Update CoinText
Else:
  Show Not enough coins message
```

For Day 07, no rewarded ad yet.

---

## 12. Basic Safe Arrow Detection

A safe arrow is an arrow whose path is clear.

Use the same PathChecker logic from Day 03:

```text
For each Arrow:
  Place PathChecker based on Arrow.Direction
  If no collision with Blocker or other Arrow:
    This arrow is safe
    Save HintTargetArrowID
    Stop checking
```

GDevelop visual events may make loop logic harder.

Practical MVP approach:

```text
Start with manually checking currently picked Arrow objects through event picking.
If full auto hint is too hard, create a placeholder hint first.
```

Acceptable Day 07 placeholder:

```text
HintButton highlights a pre-defined safe arrow for the current manual level.
```

Final target:

```text
HintButton dynamically finds the first safe arrow.
```

---

## 13. Hint Highlight Effect

When hint target is found:

```text
Set HintActive = 1
Set HintTargetArrowID = target ArrowID
Apply visual highlight to that arrow
```

Possible highlight methods:

```text
Change arrow opacity repeatedly
Add glow object behind arrow
Tint arrow yellow briefly
Scale arrow up/down slightly
```

Recommended simple MVP:

```text
Scale selected arrow to 1.15 for 0.4 seconds, then return to 1.0
```

---

## 14. Not Enough Coins Behavior

If player has fewer than `HintCost` coins:

```text
Show HintMessageText = "Not enough coins"
Set NotEnoughCoinsTimer = 2
```

Every frame:

```text
If NotEnoughCoinsTimer > 0:
  Subtract TimeDelta from NotEnoughCoinsTimer
Else:
  Hide HintMessageText
```

Later this flow becomes:

```text
Offer rewarded ad for free hint
```

---

## 15. Double Reward Placeholder

On WinLayer, show `DoubleRewardButton`.

For Day 07:

```text
DoubleRewardButton can be disabled or show "Coming soon"
```

Later with AdMob:

```text
Watch rewarded ad → add RewardCoins again → RewardAlreadyDoubled = 1
```

Rules:

```text
Base reward is always given immediately
Double reward can only be claimed once
Cancelling ad gives no extra reward
```

---

## 16. Coin Save Rules

Write `Coins` to storage after:

```text
Level win reward
Hint purchase
Perfect bonus
Double reward later
Daily reward later
```

Never let coins go below zero:

```text
If Coins < 0:
  Set Coins = 0
```

---

## 17. UI Update Rules

Update UI after:

```text
Scene start
Level win
Hint purchase
Perfect bonus
Double reward
Storage load
```

Minimum UI:

```text
CoinText = Coins
CoinRewardText = +RewardCoins coins
HintMessageText = Not enough coins
```

---

## 18. Testing Coin Rewards

Test Level 1:

```text
Start with Coins = 0
Complete Level 1
Expected: Coins = 10
Restart app
Expected: Coins still = 10
```

Test Level 10:

```text
Complete Level 10
Expected: Coins increases by 20
```

---

## 19. Testing Hint Cost

Set Coins to 30.

Tap HintButton.

Expected:

```text
Coins = 10
Hint highlights arrow or placeholder hint appears
Coins saved to storage
```

Set Coins to 5.

Tap HintButton.

Expected:

```text
Coins remains 5
Not enough coins message appears
No hint cost deducted
```

---

## 20. Testing Duplicate Rewards

Complete a level.

Expected:

```text
Coins added once
```

Wait on WinLayer.

Expected:

```text
Coins do not keep increasing every frame
```

Press Replay and complete again.

Expected:

```text
Coins can be earned again from a replay only if allowed by design.
```

MVP design decision:

```text
Allow coins on replay for now, but watch for abuse later.
```

Later production rule may limit repeated farming.

---

## 21. Common Problems

### Problem: Coins increase every frame after win

Check:

```text
RewardAlreadyGiven starts at 0
Win reward condition requires RewardAlreadyGiven = 0
Set RewardAlreadyGiven = 1 immediately after giving reward
```

---

### Problem: Coins reset after restart

Check:

```text
Write Coins to storage after change
Read Coins from storage at game start
Use GlobalVariable(Coins), not only scene variable
```

---

### Problem: Hint takes coins but shows no hint

Check:

```text
HintTargetArrowID is found
Safe arrow detection works
Highlight action targets correct ArrowID
PathChecker resets after hint check
```

---

### Problem: Hint highlights blocked arrow

Check:

```text
Use same path-checking rules as actual gameplay
Selected arrow is excluded from its own PathChecker collision
Blocker and Arrow collisions are both checked
```

---

## 22. Day 07 Acceptance Test

Day 07 is complete only when all checks pass:

- [ ] Coins global variable exists
- [ ] CoinText displays current coins
- [ ] RewardCoins is set per level
- [ ] Completing level adds coins once
- [ ] Coins save to storage
- [ ] Coins load after app restart
- [ ] HintButton exists
- [ ] HintCost exists
- [ ] Hint deducts coins only when enough coins exist
- [ ] Not enough coins message appears when needed
- [ ] Hint highlight or placeholder works
- [ ] WinLayer shows coin reward text
- [ ] DoubleRewardButton placeholder exists or is intentionally hidden
- [ ] Coins never become negative
- [ ] No duplicate coin reward loop exists

---

## 23. After Day 07

Next file to follow:

```text
docs/day_08_undo_and_extra_chance.md
```

Day 08 goal:

```text
Add Undo placeholder/state handling and Extra Chance flow after losing.
```

---

## 24. Critical Rule

Economy must support gameplay, not block gameplay.

The player must still be able to complete levels without paying or watching ads.
