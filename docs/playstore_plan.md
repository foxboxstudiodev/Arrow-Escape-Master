# Arrow Escape Master — Google Play Store Plan

This document defines the Google Play release plan for **Arrow Escape Master**.

The game must not be uploaded randomly. The store release needs a clean build, correct metadata, privacy policy, screenshots, content rating, and internal testing before production.

---

## 1. Store Identity

### App Name

```text
Arrow Escape Master
```

### Package Name

```text
com.foxboxstudio.arrowescapemaster
```

### Developer / Studio Name

```text
FoxBoxStudio Dev
```

### Category

```text
Game / Puzzle
```

### Platform

```text
Android
```

### Orientation

```text
Portrait
```

---

## 2. Release Strategy

Correct release order:

```text
1. Build MVP locally
2. Test on Android phone
3. Export AAB from GDevelop
4. Upload to Play Console internal testing
5. Test install from Play Store internal testing link
6. Fix build/policy/gameplay issues
7. Prepare production release
8. Publish publicly
```

Do not publish the first build directly to production.

---

## 3. First Public Version Scope

The first public version should include:

```text
Main menu
Game scene
Level select
50 levels
Save progress
Coin system
Hint system
Restart / next level
Win / lose popups
Basic sound and vibration
Rewarded ad support
Interstitial ad support
Privacy policy
Stable Android AAB build
```

The first version should not include:

```text
Online multiplayer
Leaderboard
Cloud save
Complex purchases
Account login
Aggressive ad frequency
Unfinished mechanics
```

---

## 4. Build Requirements

### Export Format

For Google Play, export:

```text
Android App Bundle (.aab)
```

APK can be useful for local testing, but the Play Store release should use AAB.

### Build Source

The Android build will be exported from:

```text
GDevelop
```

### Signing

The build must be signed correctly before Play Store release.

Recommended approach:

```text
Use Google Play App Signing
Keep upload key safe
Do not lose signing credentials
```

---

## 5. Versioning

Use semantic public version names:

```text
0.1.0 = first internal testing build
0.2.0 = improved test build with 10+ levels
0.5.0 = MVP candidate
1.0.0 = first public production release
```

Use increasing internal version codes:

```text
1, 2, 3, 4, 5...
```

Example:

```text
Version name: 0.1.0
Version code: 1
```

---

## 6. Store Listing Assets

### Required Text Assets

```text
App name
Short description
Full description
Privacy policy URL
Developer contact email
```

### Required Visual Assets

```text
App icon
Feature graphic
Phone screenshots
```

Recommended screenshot count for first release:

```text
6 screenshots
```

Screenshot themes:

```text
1. Main menu
2. Easy level
3. Harder level
4. Win screen
5. Hint/coin screen
6. Level select
```

---

## 7. Store Text Draft

### Short Description

```text
Tap arrows, clear the path, and solve relaxing escape puzzles.
```

### Full Description Draft

```text
Arrow Escape Master is a simple and relaxing puzzle game where every move matters.

Tap arrows in the correct order, clear the board, avoid blocked paths, and solve clever escape levels. Each arrow moves only in its own direction, so you must think before you tap.

Features:

• Simple tap-to-play puzzle gameplay
• Relaxing arrow escape levels
• Offline play
• Easy to learn, harder to master
• Coins and hints
• Many levels with increasing difficulty
• Clean 2D design

Train your brain, plan the right order, and become the Arrow Escape Master.
```

---

## 8. Keywords / ASO Targets

Primary keywords:

```text
arrow puzzle
escape puzzle
arrow escape
brain puzzle
logic puzzle
casual puzzle
relaxing puzzle
```

Do not overload the title with keywords.

Approved title:

```text
Arrow Escape Master
```

---

## 9. Privacy Policy

A privacy policy is required because the game will use ads.

Privacy policy must mention:

```text
AdMob / advertising
Device identifiers used by ad networks
No account registration
No direct collection of personal information by the game developer
Analytics if added later
Contact email
```

A separate draft file will be stored here:

```text
docs/privacy_policy_draft.md
```

---

## 10. Data Safety Form

The Google Play Data Safety form must match the real game behavior.

For first version, expected data areas:

```text
Advertising ID may be used by ad SDK
Approximate app activity may be processed by ad services
No login data
No user-created content
No location collection by the game itself
No financial data collected by the game itself
```

Important rule:

```text
Do not guess the final Data Safety answers until the real SDKs are added.
```

Final answers must be checked after AdMob integration.

---

## 11. Content Rating

Expected rating category:

```text
Everyone / suitable for general audience
```

The game must avoid:

```text
Violence
Gambling simulation
Real money rewards
Adult content
User-generated content
Chat
```

---

## 12. Ads Policy

Ad types planned:

```text
Rewarded ads for hints
Rewarded ads for undo / extra chance
Interstitial ads after several completed levels
```

Ad frequency rule:

```text
No interstitial after every level
No ad before the player understands the game
No ad during active gameplay
Rewarded ads only after player action
```

Recommended MVP ad frequency:

```text
Interstitial after every 3 completed levels
Rewarded ad only for optional hint / extra chance
```

---

## 13. Play Console Checklist

Before internal testing:

- [ ] AAB exported from GDevelop
- [ ] App icon ready
- [ ] Feature graphic ready
- [ ] Screenshots ready
- [ ] Short description ready
- [ ] Full description ready
- [ ] Privacy policy URL ready
- [ ] Developer email ready
- [ ] App category selected
- [ ] Content rating completed
- [ ] Data Safety form completed
- [ ] Target audience selected
- [ ] Internal testers added

Before production:

- [ ] Internal test install works
- [ ] No launch crash
- [ ] Ads use production IDs only after testing
- [ ] All 50 levels are solvable
- [ ] Save progress works
- [ ] No broken buttons
- [ ] No placeholder text visible
- [ ] Privacy policy matches real behavior
- [ ] Store screenshots match actual gameplay

---

## 14. Internal Testing Plan

Internal test build target:

```text
Version name: 0.1.0
Version code: 1
Levels: 10
Ads: test mode only
Purpose: gameplay and build validation
```

MVP test build target:

```text
Version name: 0.5.0
Version code: 5
Levels: 50
Ads: test mode first, production later
Purpose: pre-release validation
```

Production build target:

```text
Version name: 1.0.0
Version code: 10
Levels: 50+
Ads: production AdMob IDs
Purpose: public release
```

---

## 15. First Release Quality Gate

The game is ready for first public release only when all conditions pass:

```text
Game opens without crash
Main menu works
Level select works
At least 50 levels are playable
All levels are solvable
Win screen works
Lose screen works
Restart works
Next level works
Save/load progress works
Coins work
Hints work
Ads do not break gameplay
Android AAB installs through internal testing
Store listing is complete
Privacy policy is published
```

---

## 16. Post-Launch Plan

After public release:

```text
Monitor crashes
Monitor reviews
Improve screenshots
Improve first 10 levels
Add 50 new levels
Adjust ad frequency if users complain
Add more themes
Add daily challenge later
```

---

## 17. Critical Rule

Do not release an unfinished prototype under the final name.

The public release must feel like a small but complete game.
