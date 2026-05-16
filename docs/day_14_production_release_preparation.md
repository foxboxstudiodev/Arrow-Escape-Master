# Arrow Escape Master — Day 14 Production Release Preparation

This document defines Day 14 tasks for **Arrow Escape Master**.

Day 14 goal:

```text
Prepare the final production release package for Google Play: store listing, screenshots, final privacy policy, Data Safety, content rating, final AAB, release notes, and production launch gate.
```

This is the final checklist before public release.

---

## 1. Required Before Day 14

Day 13 must already be complete:

- [ ] AAB was uploaded to internal testing
- [ ] Internal testing release was created
- [ ] Tester opt-in link worked
- [ ] App installed from Play Store internal testing
- [ ] App opened without crash
- [ ] Core gameplay worked from Play Store install
- [ ] Save/load worked from Play Store install
- [ ] Critical and high bugs were fixed
- [ ] Store-distributed build was validated

Do not prepare production release if internal testing failed.

---

## 2. Day 14 Scope

Day 14 includes:

```text
Final production checklist
Store listing completion
Screenshots and feature graphic
Final privacy policy
Data Safety form
Content rating
Target audience settings
Final AAB review
Release notes
Production rollout plan
Post-launch monitoring plan
```

Day 14 does not include:

```text
Ignoring internal test bugs
Publishing unfinished levels
Uploading fake screenshots
Using mismatched privacy answers
Changing package name
Skipping final device test
```

---

## 3. Production Build Target

Recommended first production release:

```text
Version name: 1.0.0
Version code: 10 or higher
Track: Production
Levels: 50+
Ads: production IDs only after final testing
Build type: Android App Bundle (.aab)
Package name: com.foxboxstudio.arrowescapemaster
```

Rule:

```text
Version code must be higher than all internal testing builds.
```

---

## 4. Final Game Scope

First public version must include:

```text
MainMenu
GameScene
LevelSelect
50 playable levels
Save/load progress
Win/Lose screens
Coins
Hints
Restart / Replay / Next level
Optional Undo or safely disabled Undo
Extra Chance flow
Clean UI
App icon
Play Store screenshots
Privacy policy
Stable Android AAB
```

Ads may be included only if:

```text
Rewarded ads work correctly
Interstitial ads are not aggressive
Privacy policy and Data Safety match actual SDK behavior
```

---

## 5. Production Blockers

Production release is blocked if any of these are true:

```text
App crashes on launch
AAB rejected by Play Console
Any public level is impossible
Save/load progress fails
Main gameplay input fails
UI is unusable on common phone screen
Ads reward users incorrectly
Ads appear during active gameplay
Privacy policy is missing
Data Safety answers are inaccurate
Content rating is incomplete
Screenshots are fake or misleading
```

Do not override these blockers.

---

## 6. Store Listing — Final Values

### App Name

```text
Arrow Escape Master
```

### Category

```text
Game / Puzzle
```

### Pricing

```text
Free
```

### Developer Name

```text
FoxBoxStudio Dev
```

### Package Name

```text
com.foxboxstudio.arrowescapemaster
```

---

## 7. Short Description

Final short description candidate:

```text
Tap arrows, clear the path, and solve relaxing escape puzzles.
```

Rules:

```text
Keep it simple
Use relevant keywords naturally
Do not overpromise
Do not claim features not inside the game
```

---

## 8. Full Description

Final full description candidate:

```text
Arrow Escape Master is a relaxing arrow puzzle game where every tap matters.

Tap arrows in the correct order, clear the path, avoid blocked moves, and solve smart escape puzzles. Each arrow moves only in its own direction, so you need to plan the right sequence before you tap.

Features:

• Simple tap-to-play puzzle gameplay
• Relaxing arrow escape levels
• Offline play
• Easy to learn, harder to master
• Coins and helpful hints
• Increasing level difficulty
• Clean 2D puzzle design

Think carefully, clear every arrow, and become the Arrow Escape Master.
```

Before release, check that every listed feature exists.

---

## 9. Store Keywords / ASO Direction

Primary search targets:

```text
arrow puzzle
escape puzzle
arrow escape
brain puzzle
logic puzzle
casual puzzle
relaxing puzzle
```

Rules:

```text
Do not keyword-stuff the title
Do not repeat keywords unnaturally
Do not use competitor names
Do not make misleading claims
```

---

## 10. Store Visual Assets

Required production assets:

```text
App icon
Feature graphic
Phone screenshots
```

Recommended files:

```text
assets/icons/app_icon_512.png
assets/store/feature_graphic_1024x500.png
assets/store/screenshot_01_main_menu.png
assets/store/screenshot_02_easy_level.png
assets/store/screenshot_03_puzzle_order.png
assets/store/screenshot_04_win_screen.png
assets/store/screenshot_05_level_select.png
assets/store/screenshot_06_hint_reward.png
```

Rules:

```text
Screenshots must show real gameplay
No fake UI
No copyrighted elements
No misleading rewards or claims
```

---

## 11. Screenshot Checklist

Use 6 screenshots:

```text
1. Main menu
2. First easy level
3. Multi-arrow puzzle
4. Win screen with coin reward
5. Level select screen
6. Hint / extra chance feature
```

Optional overlay texts:

```text
Tap Arrows
Clear the Path
Solve Smart Puzzles
Unlock Levels
Use Hints
Play Offline
```

Check:

```text
Text is readable
Screenshots are high quality
Screenshots match actual game
No debug UI visible
No placeholder objects visible
```

---

## 12. App Icon Final Check

App icon must be:

```text
Clear at small size
High contrast
No small unreadable text
No copied artwork
Representative of arrow puzzle gameplay
```

Approved concept:

```text
Large arrow escaping from a small puzzle board
```

---

## 13. Privacy Policy Finalization

Draft file:

```text
docs/privacy_policy_draft.md
```

Before production:

```text
Add effective date
Add developer contact email
Add final third-party service links
Confirm AdMob usage
Confirm analytics/crash reporting usage
Publish privacy policy on public URL
Add privacy policy URL to Play Console
```

Privacy policy must match the actual production build.

---

## 14. Data Safety Form

Data Safety must match actual SDK behavior.

Before final submission, confirm:

```text
Is AdMob included?
Is Advertising ID used?
Are personalized ads enabled?
Is analytics included?
Is crash reporting included?
Is any user account data collected?
Is any precise location collected?
Is any user-generated content collected?
```

Expected MVP behavior:

```text
No account registration
No user-created content
No direct personal data collection by developer
Local progress stored on device
Advertising SDK may process ad-related data
```

Do not submit guessed answers.

---

## 15. Content Rating

Expected game type:

```text
General puzzle game
No violence
No gambling
No sexual content
No user chat
No user-generated content
```

Complete Play Console content rating questionnaire honestly.

Production is blocked until content rating is complete.

---

## 16. Target Audience

Target audience should match the real design and advertising configuration.

Before choosing audience:

```text
Check whether ads are child-directed or not
Check game visuals and content
Check Google Play requirements
```

If targeting general audience:

```text
Do not claim children-specific targeting unless all policies and ad settings are configured correctly.
```

---

## 17. Ads Final Check

If ads are enabled in production:

Rewarded ads:

```text
Hint reward works
Extra Chance reward works
Double Reward works or is disabled
Cancelled ad gives no reward
Failed ad does not block gameplay
```

Interstitial ads:

```text
Not shown before first gameplay
Not shown during gameplay
Not shown after every level
Not shown immediately after rewarded ad
Appears only at safe transition points
```

Final rule:

```text
Retention first, revenue second.
```

---

## 18. Final AAB Checklist

Before production upload:

- [ ] Version name is final
- [ ] Version code is higher than internal test builds
- [ ] Package name is correct
- [ ] App icon is correct
- [ ] Production assets included
- [ ] Debug objects hidden
- [ ] Test-only text removed
- [ ] Test ad IDs replaced with production IDs only when ready
- [ ] Privacy/Data Safety match SDK behavior
- [ ] AAB exports successfully
- [ ] AAB was tested through internal testing or closed testing

---

## 19. Release Notes

Production release notes candidate:

```text
Arrow Escape Master is now available.
Solve relaxing arrow escape puzzles, clear the board in the right order, use hints when needed, and unlock new levels.
```

Keep release notes honest and concise.

---

## 20. Rollout Strategy

Recommended first rollout:

```text
Do not rush wide release if Play Console allows staged rollout.
Start cautiously, monitor crashes and reviews, then expand.
```

If staged rollout is not used:

```text
Publish production only after internal testing passes fully.
```

---

## 21. Post-Launch Monitoring

After release, monitor:

```text
Crashes
ANRs
User reviews
Install/uninstall behavior
Level difficulty complaints
Ad complaints
Device-specific UI issues
```

First update priorities:

```text
Fix crashes
Fix impossible levels
Reduce ad frequency if complaints appear
Improve first 10 levels if users drop early
Improve screenshots if conversion is weak
```

---

## 22. First Update Plan

Recommended first update after launch:

```text
Version 1.0.1
Fix urgent bugs
Improve early level difficulty
Adjust ad timing if needed
Polish UI text
```

Second update:

```text
Version 1.1.0
Add 25–50 new levels
Add new theme or visual polish
Improve hint system
```

---

## 23. Production Release Gate

Production release is allowed only when all checks pass:

- [ ] Internal testing passed
- [ ] No critical bugs remain
- [ ] No high bugs remain
- [ ] 50 levels are included
- [ ] All 50 levels are solvable
- [ ] Save/load works
- [ ] Main UI is clean
- [ ] App icon is ready
- [ ] Screenshots are ready
- [ ] Feature graphic is ready
- [ ] Short description is ready
- [ ] Full description is ready
- [ ] Privacy policy is published
- [ ] Data Safety is completed accurately
- [ ] Content rating is completed
- [ ] Target audience is completed
- [ ] Final AAB is accepted by Play Console
- [ ] Release notes are ready

---

## 24. Launch-Day Checklist

On launch day:

```text
1. Confirm final AAB version code
2. Confirm store listing text
3. Confirm screenshots
4. Confirm privacy policy URL
5. Confirm Data Safety
6. Confirm content rating
7. Confirm production release notes
8. Submit production release
9. Monitor Play Console status
10. After approval, test live listing
```

---

## 25. Live Listing Check

After app becomes live:

- [ ] Store page opens
- [ ] App name is correct
- [ ] Icon is correct
- [ ] Screenshots load
- [ ] Description is correct
- [ ] Install works
- [ ] App opens after live install
- [ ] Ads behave correctly if enabled
- [ ] No wrong package/app was published

---

## 26. Emergency Rollback / Hotfix Rule

If production has a serious bug:

```text
Prepare hotfix build immediately
Increase version code
Fix only critical issue
Export AAB
Test quickly but carefully
Upload update
```

Do not add new features in emergency hotfix.

Hotfix should be narrow and safe.

---

## 27. Common Production Mistakes

### Mistake: Publishing with impossible levels

Result:

```text
Bad reviews and early uninstall
```

Prevention:

```text
Test every level and keep solution order notes
```

---

### Mistake: Too many ads

Result:

```text
Low retention and negative reviews
```

Prevention:

```text
Use rewarded ads mainly and limit interstitial frequency
```

---

### Mistake: Inaccurate Data Safety answers

Result:

```text
Policy risk and possible app removal
```

Prevention:

```text
Match answers to actual SDK behavior
```

---

### Mistake: Weak first screenshots

Result:

```text
Poor conversion from store visits to installs
```

Prevention:

```text
Use clear real gameplay screenshots with simple benefit text
```

---

## 28. Day 14 Acceptance Test

Day 14 is complete only when all checks pass:

- [ ] Production release checklist exists
- [ ] Store listing text is prepared
- [ ] Screenshot plan is prepared
- [ ] Privacy policy finalization plan is prepared
- [ ] Data Safety plan is prepared
- [ ] Content rating plan is prepared
- [ ] Final AAB checklist is defined
- [ ] Production release gate is defined
- [ ] Launch-day checklist is defined
- [ ] Post-launch monitoring plan is defined
- [ ] Hotfix rule is defined

---

## 29. Final Critical Rule

Do not publish because the app is “almost ready”.

Publish only when the game is stable, understandable, solvable, policy-compliant, and test-installed through Google Play.
