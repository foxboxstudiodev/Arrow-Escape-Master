# Arrow Escape Master — Testing Checklist

This document defines the testing checklist for **Arrow Escape Master** before internal testing and public release.

The game must not be released until the core gameplay, levels, UI, save system, ads, and Android build are verified.

---

## 1. Testing Stages

Testing must happen in this order:

```text
1. Editor gameplay test
2. Local Android APK test
3. Android AAB internal testing through Play Console
4. Pre-production release test
5. Production release validation
```

Do not skip internal testing.

---

## 2. Core Gameplay Test

Test every core gameplay rule.

- [ ] GameScene opens without errors
- [ ] Arrow object appears on correct grid cell
- [ ] Arrow direction is visually clear
- [ ] Tap/click on arrow is detected
- [ ] Clear arrow moves in the correct direction
- [ ] Arrow leaves the board correctly
- [ ] Escaped arrow is deleted
- [ ] `ArrowsRemaining` decreases after escape
- [ ] Blocked arrow does not move
- [ ] Blocked arrow counts as mistake
- [ ] Failed move gives visible feedback
- [ ] Player cannot tap while arrow is moving
- [ ] Input unlocks after arrow movement ends
- [ ] Win condition triggers when all arrows are removed
- [ ] Lose condition triggers after mistake limit
- [ ] Restart resets level correctly
- [ ] Next button loads next level correctly

---

## 3. Direction Test

Every direction must be tested separately.

### Up

- [ ] Up arrow moves upward
- [ ] Up arrow checks blockers above it
- [ ] Up arrow exits through top side
- [ ] Up arrow deletes after leaving screen

### Right

- [ ] Right arrow moves right
- [ ] Right arrow checks blockers to the right
- [ ] Right arrow exits through right side
- [ ] Right arrow deletes after leaving screen

### Down

- [ ] Down arrow moves downward
- [ ] Down arrow checks blockers below it
- [ ] Down arrow exits through bottom side
- [ ] Down arrow deletes after leaving screen

### Left

- [ ] Left arrow moves left
- [ ] Left arrow checks blockers to the left
- [ ] Left arrow exits through left side
- [ ] Left arrow deletes after leaving screen

---

## 4. PathChecker Test

The hidden `PathChecker` must behave correctly.

- [ ] PathChecker appears only during check or remains hidden
- [ ] PathChecker does not overlap selected arrow
- [ ] PathChecker detects other arrows in the path
- [ ] PathChecker detects blockers in the path
- [ ] PathChecker does not detect objects behind the arrow
- [ ] PathChecker resets after every check
- [ ] PathChecker works for all four directions
- [ ] PathChecker does not stay visible in release build

---

## 5. Level Solvability Test

Every level must be tested manually before release.

For each level:

- [ ] Level loads correctly
- [ ] All arrows are inside board bounds
- [ ] No two objects incorrectly overlap
- [ ] At least one valid first move exists
- [ ] Level can be completed fully
- [ ] Difficulty feels fair
- [ ] Mistake limit is reasonable
- [ ] Reward coins are assigned
- [ ] No arrow gets stuck during escape
- [ ] No false win or false lose happens

MVP level requirement:

```text
All 50 public release levels must be solvable.
```

Internal testing requirement:

```text
First 10 levels must be solvable.
```

---

## 6. UI Test

Test all UI elements.

- [ ] Main menu opens correctly
- [ ] Play button works
- [ ] Level Select button works
- [ ] Settings button works
- [ ] Restart button works
- [ ] Hint button does not break gameplay
- [ ] Undo button does not break gameplay
- [ ] Next button works
- [ ] Replay button works
- [ ] Home button works
- [ ] WinLayer appears only after win
- [ ] LoseLayer appears only after lose
- [ ] UI text updates after every move
- [ ] CoinText updates after rewards
- [ ] Buttons are large enough for mobile touch
- [ ] No placeholder debug text is visible in production

---

## 7. Save / Load Test

Test local storage behavior.

- [ ] First launch starts at Level 1
- [ ] Completing Level 1 unlocks Level 2
- [ ] Closing and reopening the game preserves unlocked level
- [ ] Coin balance is saved
- [ ] Sound setting is saved
- [ ] Vibration setting is saved
- [ ] Restart does not incorrectly reset global progress
- [ ] Replaying completed levels does not lock progress
- [ ] Player cannot open locked levels from LevelSelect

---

## 8. Coin and Reward Test

- [ ] Completing a level adds base coins
- [ ] Perfect completion bonus works if enabled
- [ ] Hint cost is deducted correctly
- [ ] Hint is not allowed if coins are insufficient unless rewarded ad is used
- [ ] Double reward gives only one extra reward
- [ ] Coins cannot become negative
- [ ] Coins save correctly after app restart

---

## 9. Hint Test

- [ ] Hint button can detect at least one safe arrow
- [ ] Hint highlights a valid arrow
- [ ] Hint does not highlight blocked arrow as safe
- [ ] Hint does not trigger after level is completed
- [ ] Hint does not trigger after level failed
- [ ] Hint does not break input lock

For MVP, hint may be placeholder, but it must not crash or corrupt the level.

---

## 10. Ads Test

Use test ads during development.

Rewarded ads:

- [ ] Rewarded ad opens from Hint button when needed
- [ ] Rewarded ad opens from Extra Chance button
- [ ] Reward is given only after completed ad
- [ ] Reward is not given if ad is cancelled
- [ ] Rewarded ad does not break scene state

Interstitial ads:

- [ ] Interstitial is not shown during gameplay
- [ ] Interstitial is not shown before first level
- [ ] Interstitial appears only after allowed frequency
- [ ] Closing interstitial returns player to correct screen
- [ ] Interstitial does not appear immediately after rewarded ad

Production rule:

```text
Never click live production ads for testing.
```

---

## 11. Android Device Test

Test on at least one real Android phone before Play Store internal testing.

- [ ] Game installs successfully
- [ ] Game opens without crash
- [ ] Touch input works
- [ ] Screen scaling is correct
- [ ] No important UI is outside screen
- [ ] Back button behavior is acceptable
- [ ] Sound works
- [ ] Vibration works if enabled
- [ ] Game resumes correctly after app minimized
- [ ] Game does not freeze after several levels

Recommended test devices:

```text
One low-end Android phone
One modern Android phone if available
```

---

## 12. Performance Test

- [ ] No visible lag during arrow movement
- [ ] No lag when opening WinLayer
- [ ] No lag when restarting level
- [ ] No memory issue after replaying multiple levels
- [ ] Asset sizes are not unnecessarily huge
- [ ] Game loads fast enough

Target:

```text
Stable 60 FPS on normal Android phones if possible
```

---

## 13. Audio Test

- [ ] Button sound plays if sound enabled
- [ ] Arrow escape sound plays if sound enabled
- [ ] Fail sound plays if sound enabled
- [ ] Win sound plays if sound enabled
- [ ] Lose sound plays if sound enabled
- [ ] Sounds stop when sound disabled
- [ ] Sounds are not too loud or annoying

---

## 14. Play Store Build Test

Before internal testing:

- [ ] AAB exports successfully from GDevelop
- [ ] Version name is correct
- [ ] Version code is increased
- [ ] Package name is correct
- [ ] App icon appears correctly
- [ ] App name appears correctly
- [ ] Build is signed correctly
- [ ] Play Console accepts the AAB
- [ ] Internal test release is created
- [ ] Internal test install works from Play Store link

---

## 15. Store Listing Test

- [ ] App name is correct
- [ ] Short description is correct
- [ ] Full description is correct
- [ ] Screenshots show actual gameplay
- [ ] Feature graphic is uploaded
- [ ] App icon is uploaded
- [ ] Privacy policy URL works
- [ ] Contact email is correct
- [ ] Category is Game / Puzzle
- [ ] Content rating is completed
- [ ] Data Safety form matches actual SDK usage
- [ ] Target audience settings are correct

---

## 16. Production Release Gate

The game can move to production only when all of these are true:

- [ ] At least 50 levels are included
- [ ] All included levels are solvable
- [ ] No known crash exists
- [ ] No broken UI button exists
- [ ] Save/load works
- [ ] Ads work in correct mode
- [ ] Privacy policy is published
- [ ] Data Safety form is correct
- [ ] Internal testing install works
- [ ] Store listing is complete
- [ ] Final AAB is accepted by Play Console

---

## 17. Bug Report Format

Use this format for every bug:

```text
Bug ID:
Build version:
Device:
Scene:
Level:
Steps to reproduce:
Expected result:
Actual result:
Severity: low / medium / high / critical
Status: open / fixed / retest / closed
```

---

## 18. Critical Rule

If a level cannot be solved, it must not be included in public release.

If an ad breaks gameplay, ads must be disabled until fixed.

If save/load fails, production release is blocked.
