# Arrow Escape Master — Monetization Plan

This document defines the monetization model for **Arrow Escape Master**.

The goal is to earn revenue without damaging gameplay, retention, or Play Store review quality.

---

## 1. Monetization Model

First release monetization:

```text
AdMob rewarded ads
AdMob interstitial ads
Remove ads placeholder
```

No paid currency or in-app purchases in the first version unless the core game is already stable.

---

## 2. Revenue Sources

### 2.1 Rewarded Ads

Rewarded ads are optional and triggered by the player.

Use rewarded ads for:

```text
Hint
Undo
Extra chance after failure
Double coin reward after win
```

Rewarded ads are the safest ad type because the player chooses to watch them.

---

### 2.2 Interstitial Ads

Interstitial ads are full-screen ads.

Use carefully.

Allowed placement:

```text
After every 3 completed levels
After returning to main menu from gameplay
After several retries, not every retry
```

Forbidden placement:

```text
During active gameplay
Immediately after app launch
Before the first level starts
After every single tap
After every failed move
Too soon after a rewarded ad
```

---

### 2.3 Remove Ads Placeholder

Main menu may show:

```text
Remove Ads
```

For MVP, this can be a placeholder.

Real in-app purchase integration should be added later only after the game is stable.

---

## 3. Ad Frequency Rules

Recommended first release rules:

```text
No interstitial during first 3 levels
Interstitial after every 3 completed levels starting from Level 4
No interstitial if player just watched rewarded ad
No interstitial after quick restart
No interstitial during tutorial explanation
```

Example:

```text
Level 1 completed → no interstitial
Level 2 completed → no interstitial
Level 3 completed → no interstitial
Level 4 completed → no interstitial if tutorial still active
Level 5 completed → possible interstitial
Then every 3 completed levels
```

Better simple rule for MVP:

```text
Show interstitial when CompletedLevels % 3 = 0 and CompletedLevels > 3
```

---

## 4. Coin Economy

Coins should support hints and small rewards.

### 4.1 Coin Sources

```text
Complete level: +10 to +20 coins
Perfect level with 0 mistakes: +5 bonus coins
Rewarded ad double reward: x2 coins after win
Daily reward later: +25 coins
```

### 4.2 Coin Spending

```text
Hint: 20 coins
Undo: 30 coins
Extra chance: rewarded ad first, coin option later
```

---

## 5. Level Reward Table

Recommended MVP reward:

| Level Type | Base Reward | Perfect Bonus |
|---|---:|---:|
| Easy | 10 coins | 5 coins |
| Normal | 14 coins | 7 coins |
| Hard | 20 coins | 10 coins |
| Boss | 25 coins | 15 coins |

---

## 6. Hint System Monetization

Hint button flow:

```text
Player taps Hint
↓
If Coins >= 20:
  Spend 20 coins
  Show safe arrow hint
Else:
  Offer rewarded ad
```

Do not force ad immediately if the player has coins.

---

## 7. Undo System Monetization

Undo button flow:

```text
Player taps Undo
↓
If Coins >= 30:
  Spend 30 coins
  Restore previous move
Else:
  Offer rewarded ad
```

MVP can include Undo as placeholder. Real undo requires storing previous level state.

---

## 8. Extra Chance Monetization

After losing:

```text
Show LoseLayer
Show ExtraChanceButton
```

Extra chance reward:

```text
Watch rewarded ad → Mistakes = MistakeLimit - 1 → Continue level
```

Limit:

```text
Only 1 extra chance per level attempt
```

Scene variable:

```text
ExtraChanceUsed = 0
```

---

## 9. Double Reward Monetization

After winning:

```text
Show WinLayer
Give base coins immediately
Offer double reward button
```

If player watches rewarded ad:

```text
Add extra coins equal to base reward
Disable double reward button
```

Rule:

```text
Do not take away base reward if player refuses ad
```

---

## 10. Required Variables

Global variables:

```text
Coins
AdsRemoved
CompletedLevels
```

Scene variables:

```text
RewardCoins
PerfectBonusCoins
ExtraChanceUsed
RewardAlreadyDoubled
InterstitialCooldown
LastRewardedAdWatched
```

For MVP, required:

```text
Coins
RewardCoins
ExtraChanceUsed
RewardAlreadyDoubled
```

---

## 11. AdMob Setup Plan

Correct setup order:

```text
1. Create AdMob account
2. Create Android app in AdMob
3. Add test ad unit IDs first
4. Integrate ads in GDevelop
5. Test on Android phone
6. Confirm rewarded callback gives reward
7. Confirm interstitial does not break scene flow
8. Replace test IDs with production IDs only before release
```

Do not use production ads while actively testing random builds.

---

## 12. Test Ad IDs Rule

During development:

```text
Use test ads only
```

Before production:

```text
Replace with real AdMob ad unit IDs
```

Never click your own live ads to test revenue.

---

## 13. User Experience Rules

Good monetization:

```text
Rewarded ads are optional
Interstitial ads are predictable and not too frequent
Player can complete levels without paying
Hints help but do not solve the whole game automatically
Coins are useful but not mandatory
```

Bad monetization:

```text
Ad after every level
Ad after every failure
Ad before gameplay starts
Forced ad for every hint
No way to continue without ad
Fake reward buttons
```

---

## 14. First Release Ad Settings

Recommended first public version:

```text
Rewarded Hint: enabled
Rewarded Extra Chance: enabled
Rewarded Double Coins: optional
Interstitial: after every 3 completed levels
Banner ads: disabled
```

Reason:

```text
Banner ads reduce screen space and make puzzle UI worse.
```

---

## 15. Banner Ads Decision

For Arrow Escape Master, banner ads are not recommended in the first version.

Reason:

```text
Portrait puzzle screen needs clean space
Banners can make UI look cheap
Interstitial + rewarded is cleaner
```

Decision:

```text
No banner ads in MVP
```

---

## 16. Monetization Quality Gate

Ads are ready only when:

```text
Rewarded ad gives the correct reward
Rewarded ad does not reward if cancelled
Interstitial does not appear during gameplay
Interstitial does not appear too frequently
Ads do not break scene transitions
Ads are not shown before first meaningful gameplay
Data Safety form matches actual SDK behavior
Privacy policy mentions advertising
```

---

## 17. First Version Monetization Scope

Version `0.1.0` internal test:

```text
Ads disabled or test placeholders only
```

Version `0.5.0` MVP candidate:

```text
Test rewarded ads
Test interstitial ads
```

Version `1.0.0` production:

```text
Production rewarded ads
Production interstitial ads
No banner ads
```

---

## 18. Critical Rule

Do not over-monetize the first release.

The first objective is:

```text
Retention first, revenue second
```

If players uninstall quickly, ad revenue will be weak regardless of ad frequency.
