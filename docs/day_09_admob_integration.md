# Arrow Escape Master — Day 09 AdMob Integration

This document defines Day 09 tasks for **Arrow Escape Master** in GDevelop.

Day 09 goal:

```text
Integrate AdMob safely using rewarded ads for optional rewards and interstitial ads only between gameplay moments.
```

Ads must never break gameplay, corrupt progress, or annoy the player with excessive frequency.

---

## 1. Required Before Day 09

Day 08 must already be complete:

- [ ] Coins work
- [ ] Hint flow exists
- [ ] Undo flow exists or placeholder exists
- [ ] Extra Chance flow exists
- [ ] WinLayer works
- [ ] LoseLayer works
- [ ] Save/load progress works
- [ ] GameScene transitions are stable
- [ ] No core gameplay crash exists

Do not add AdMob before the gameplay loop is stable.

---

## 2. Day 09 Scope

Day 09 includes:

```text
AdMob setup plan
Test ad IDs first
Rewarded ad for Hint
Rewarded ad for Extra Chance
Rewarded ad for Double Reward
Interstitial ad after safe level completion points
Ad frequency rules
Ad cooldown rules
AdsRemoved placeholder handling
Ad testing checklist
```

Day 09 does not include:

```text
Real in-app purchase Remove Ads
Advanced analytics
Mediation network setup
A/B testing
Production release upload
```

---

## 3. Ad Types Used

First release uses:

```text
Rewarded ads
Interstitial ads
```

First release does not use:

```text
Banner ads
App open ads
Native ads
```

Reason:

```text
The game needs clean portrait puzzle space. Banner ads reduce board clarity and make the game feel cheap.
```

---

## 4. Rewarded Ad Placements

Rewarded ads are optional and player-triggered.

Use rewarded ads for:

```text
Free hint when coins are not enough
Extra chance after losing
Double coins after winning
Optional undo when coins are not enough
```

Do not auto-play rewarded ads.

---

## 5. Interstitial Ad Placements

Interstitial ads are allowed only at safe breaks.

Allowed:

```text
After several completed levels
After returning to MainMenu from GameScene
After a long gameplay session
```

Forbidden:

```text
During active gameplay
Immediately after app launch
Before first level starts
After every failed tap
After every restart
Immediately after rewarded ad
When player is in the middle of solving a level
```

---

## 6. Required Global Variables

Confirm or create:

```text
AdsRemoved = 0
CompletedLevels = 0
Coins = 0
```

Optional global variables:

```text
TotalRewardedAdsWatched = 0
TotalInterstitialAdsShown = 0
```

---

## 7. Required GameScene Variables

Create or confirm:

```text
CanShowInterstitial = 0
InterstitialCooldown = 0
RewardedAdPurpose = none
WaitingForRewardedAd = 0
LastRewardedAdWatched = 0
DoubleRewardAvailable = 1
RewardAlreadyDoubled = 0
ExtraChanceUsed = 0
```

`RewardedAdPurpose` allowed values:

```text
none
hint
extra_chance
double_reward
undo
```

---

## 8. AdMob Setup Order

Correct order:

```text
1. Create AdMob account
2. Create Android app in AdMob
3. Add the game package name
4. Create rewarded ad unit
5. Create interstitial ad unit
6. Use test IDs first
7. Integrate in GDevelop
8. Test on real Android phone
9. Confirm callbacks work
10. Replace with production IDs only before release
```

Do not use production ad IDs while doing random development testing.

---

## 9. Test Ads Rule

During development:

```text
Use test ads only
```

Before production:

```text
Replace test IDs with real AdMob ad unit IDs
```

Critical rule:

```text
Never click your own live production ads for testing.
```

---

## 10. Rewarded Ad Purpose System

Before showing a rewarded ad, set:

```text
RewardedAdPurpose = hint
```

or:

```text
RewardedAdPurpose = extra_chance
```

or:

```text
RewardedAdPurpose = double_reward
```

or:

```text
RewardedAdPurpose = undo
```

When rewarded ad completes, run reward action based on `RewardedAdPurpose`.

After reward is handled:

```text
RewardedAdPurpose = none
WaitingForRewardedAd = 0
LastRewardedAdWatched = 1
```

---

## 11. Rewarded Hint Flow

When player taps `HintButton`:

```text
If Coins >= HintCost:
  Spend coins
  Show hint
Else:
  Set RewardedAdPurpose = hint
  Show rewarded ad
```

If rewarded ad completes:

```text
Show hint
Do not subtract coins
```

If rewarded ad is cancelled:

```text
No hint
No coin change
```

---

## 12. Rewarded Extra Chance Flow

When player is on `LoseLayer` and taps `ExtraChanceButton`:

```text
If ExtraChanceUsed = 0:
  Set RewardedAdPurpose = extra_chance
  Show rewarded ad
```

If rewarded ad completes:

```text
Set Mistakes = MistakeLimit - 1
Set LevelFailed = 0
Set InputLocked = 0
Set ExtraChanceUsed = 1
Hide LoseLayer
Update MistakeText
```

If rewarded ad is cancelled:

```text
Stay on LoseLayer
Do not continue level
```

---

## 13. Rewarded Double Reward Flow

On `WinLayer`, show `DoubleRewardButton` if:

```text
RewardAlreadyDoubled = 0
DoubleRewardAvailable = 1
```

When tapped:

```text
Set RewardedAdPurpose = double_reward
Show rewarded ad
```

If rewarded ad completes:

```text
Add RewardCoins to Coins
Set RewardAlreadyDoubled = 1
Write Coins to storage
Update CoinText
Update CoinRewardText
Disable DoubleRewardButton
```

If rewarded ad is cancelled:

```text
No extra coins
Button remains available if desired
```

---

## 14. Rewarded Undo Flow

Undo can remain coin-based in first MVP.

Optional rewarded undo:

```text
If Coins < UndoCost and CanUndo = 1:
  Set RewardedAdPurpose = undo
  Show rewarded ad
```

If rewarded ad completes:

```text
Restore previous move
Do not subtract coins
```

For first release, this can be disabled if it creates too much complexity.

---

## 15. Interstitial Frequency Rule

Recommended MVP rule:

```text
Show interstitial after every 3 completed levels, starting after Level 4.
```

Condition:

```text
AdsRemoved = 0
CompletedLevels > 3
CompletedLevels % 3 = 0
LastRewardedAdWatched = 0
```

If all true:

```text
Show interstitial after WinLayer flow or before next level load
```

Do not show interstitial immediately after a rewarded ad.

---

## 16. Interstitial Timing Rule

Best timing:

```text
Player taps NextButton on WinLayer
↓
If interstitial allowed, show interstitial
↓
After ad closes, load next level
```

Avoid:

```text
Showing interstitial the instant the level is completed
```

Reason:

```text
The player should first see success feedback.
```

---

## 17. AdsRemoved Placeholder

If `AdsRemoved = 1`:

```text
Do not show interstitial ads
```

Rewarded ads may still be available because they are optional rewards.

For MVP:

```text
Remove Ads button can be placeholder only
```

Real in-app purchase comes later.

---

## 18. Ad State Safety

Before showing any ad:

```text
InputLocked = 1
WaitingForRewardedAd = 1 if rewarded
```

After ad closes or fails:

```text
Restore correct scene state
Do not leave InputLocked stuck at 1 unless popup is active
```

Critical:

```text
Ad callbacks must not trigger duplicate rewards.
```

Use flags:

```text
RewardAlreadyDoubled
ExtraChanceUsed
RewardedAdPurpose
WaitingForRewardedAd
```

---

## 19. Ad Failure Handling

If ad fails to load:

For rewarded hint:

```text
Show message: Ad not available
No reward
No coin change
```

For extra chance:

```text
Stay on LoseLayer
Show message: Ad not available
```

For double reward:

```text
Keep base reward
No extra reward
```

For interstitial:

```text
Skip ad and continue to next level
```

Do not block gameplay because an ad failed.

---

## 20. Privacy and Data Safety Reminder

Because AdMob is used, before production:

```text
Update privacy policy
Complete Google Play Data Safety form accurately
Confirm advertising ID usage
Confirm whether personalized ads are enabled
```

Do not publish with mismatched privacy answers.

---

## 21. Testing Rewarded Ads

Use test ads only.

Test Hint:

```text
Set Coins = 0
Tap HintButton
Watch rewarded ad fully
Expected: hint appears, Coins remain 0
```

Cancel rewarded ad:

```text
Tap HintButton
Close ad early if possible
Expected: no hint, no coin change
```

---

## 22. Testing Extra Chance Ads

Make 3 mistakes.

Expected:

```text
LoseLayer appears
```

Tap ExtraChanceButton and complete rewarded ad.

Expected:

```text
LoseLayer hides
Mistakes = 2/3
Player can continue
ExtraChanceUsed = 1
```

Cancel ad.

Expected:

```text
LoseLayer remains
No extra chance
```

---

## 23. Testing Double Reward Ads

Complete a level.

Expected:

```text
Base coins are given immediately
WinLayer appears
DoubleRewardButton visible
```

Tap DoubleRewardButton and complete rewarded ad.

Expected:

```text
Extra RewardCoins added once
RewardAlreadyDoubled = 1
Button disabled or hidden
```

Tap again.

Expected:

```text
No duplicate reward
```

---

## 24. Testing Interstitial Ads

Complete levels until `CompletedLevels % 3 = 0` and `CompletedLevels > 3`.

Expected:

```text
Interstitial appears only after safe point
After closing ad, next level loads or scene continues correctly
```

Also test:

```text
Interstitial does not appear during gameplay
Interstitial does not appear after every level
Interstitial does not appear immediately after rewarded ad
```

---

## 25. Common Problems

### Problem: Reward is given even if ad is cancelled

Check:

```text
Use completed rewarded callback only
Do not reward on ad opened
Do not reward on ad closed unless completed flag is true
```

---

### Problem: Double reward repeats forever

Check:

```text
RewardAlreadyDoubled = 1 after reward
DoubleRewardButton condition requires RewardAlreadyDoubled = 0
```

---

### Problem: Game freezes after ad closes

Check:

```text
InputLocked is restored correctly
WaitingForRewardedAd resets to 0
Scene transition continues after interstitial close
```

---

### Problem: Interstitial appears too often

Check:

```text
CompletedLevels count
Modulo rule
Cooldown rule
LastRewardedAdWatched rule
AdsRemoved rule
```

---

## 26. Day 09 Acceptance Test

Day 09 is complete only when all checks pass:

- [ ] AdMob setup plan exists
- [ ] Test ad IDs are used in development
- [ ] Rewarded hint flow works
- [ ] Rewarded extra chance flow works
- [ ] Rewarded double reward flow works or is safely disabled
- [ ] Cancelled rewarded ads do not give rewards
- [ ] Failed ads do not block gameplay
- [ ] Interstitial appears only at safe points
- [ ] Interstitial does not appear during gameplay
- [ ] Interstitial frequency is controlled
- [ ] AdsRemoved disables interstitials
- [ ] Ad callbacks do not duplicate rewards
- [ ] Privacy policy and Data Safety requirements are noted

---

## 27. After Day 09

Next file to follow:

```text
docs/day_10_ui_polish_and_assets.md
```

Day 10 goal:

```text
Replace temporary shapes with real UI, arrows, blockers, backgrounds, icon, and store-ready visual direction.
```

---

## 28. Critical Rule

Ads must never be more important than retention.

Bad ad timing kills the game faster than weak monetization.
