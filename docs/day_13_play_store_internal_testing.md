# Arrow Escape Master — Day 13 Play Store Internal Testing

This document defines Day 13 tasks for **Arrow Escape Master**.

Day 13 goal:

```text
Upload the Android App Bundle to Google Play Console internal testing, add testers, install the app through the Play Store test link, and verify the app behaves correctly as a store-distributed build.
```

Internal testing is mandatory before any production release.

---

## 1. Required Before Day 13

Day 12 must already be complete:

- [ ] APK exports successfully
- [ ] APK installs on a real Android phone
- [ ] App opens without crash
- [ ] Touch input works on phone
- [ ] Screen scaling is acceptable
- [ ] Save/load works on phone
- [ ] AAB exports successfully
- [ ] Package name is correct
- [ ] Version code is increased
- [ ] Signing keys are safe and not committed to GitHub
- [ ] Build notes are prepared

Do not upload to Play Console if the local Android build is broken.

---

## 2. Day 13 Scope

Day 13 includes:

```text
Create app entry in Play Console
Upload AAB to internal testing
Create internal testing release
Add tester email list
Prepare release notes
Complete required Play Console setup sections enough for testing
Install app from internal test link
Run real Play Store install test
Document bugs and blockers
```

Day 13 does not include:

```text
Public production release
Marketing campaign
Final ASO optimization
Paid user acquisition
Advanced analytics review
```

---

## 3. Internal Testing Build Target

Recommended first internal testing build:

```text
Version name: 0.1.0
Version code: 1
Track: Internal testing
Levels: 10 minimum
Ads: disabled or test ads only
Purpose: install + core gameplay validation
```

MVP internal testing build later:

```text
Version name: 0.5.0
Version code: 5+
Track: Internal testing
Levels: 50
Ads: test mode first
Purpose: release candidate validation
```

---

## 4. Play Console App Identity

Use these values:

```text
App name: Arrow Escape Master
Default language: English
App or game: Game
Free or paid: Free
Category: Puzzle
Package name: com.foxboxstudio.arrowescapemaster
Developer/studio: FoxBoxStudio Dev
```

Do not change the package name after uploading the first final app bundle.

---

## 5. Required Store Setup for Internal Testing

Before internal testing can work smoothly, Play Console may require several setup sections.

Prepare:

```text
App name
App category
Content rating
Target audience
Data Safety draft
Privacy policy URL if ads are included
Developer contact email
App icon
Short description
Full description
```

For early internal testing, use draft assets if allowed, but do not use misleading text or fake screenshots.

---

## 6. Privacy Policy Requirement

Because the game will use ads, prepare a privacy policy before public release.

Repository draft:

```text
docs/privacy_policy_draft.md
```

Before internal testing with ads enabled:

```text
Publish privacy policy on a public URL
Add that URL to Play Console
Make sure policy matches actual SDK behavior
```

If ads are disabled in the first internal test, keep the privacy policy draft ready for the next build.

---

## 7. Data Safety Draft

Data Safety answers must match the real build.

Before final answers, check:

```text
Is AdMob included?
Are personalized ads enabled?
Is Advertising ID used?
Is analytics SDK included?
Is crash reporting included?
Is any account/login data collected?
```

MVP expectation:

```text
No account login
No user-generated content
No precise location collected by the game itself
Advertising SDK may process Advertising ID and ad interaction data
Local progress is stored on device
```

Do not guess final Data Safety answers if SDK configuration is not finalized.

---

## 8. Create Internal Testing Track

In Play Console:

```text
Testing
↓
Internal testing
↓
Create new release
↓
Upload AAB
↓
Add release notes
↓
Review release
↓
Roll out to internal testing
```

Release notes for first internal build:

```text
First internal test build of Arrow Escape Master. Includes basic arrow puzzle gameplay, MainMenu, GameScene, win/lose screens, level progress testing, and early Android device validation.
```

---

## 9. Tester List

Create an internal tester list.

Minimum:

```text
Your own Google account email
```

Recommended:

```text
2–5 trusted testers
```

Tester requirements:

```text
Tester must use the same Google account on the Android phone
Tester must open the opt-in link
Tester must accept testing
Tester installs the app from Play Store test listing
```

---

## 10. Internal Test Link Flow

After release is available:

```text
Copy internal test opt-in link
Open link from tester Google account
Join test
Open Play Store listing
Install app
Run test checklist
```

Important:

```text
Direct APK install is not enough for Day 13.
The app must be installed through the Play Store internal testing flow.
```

---

## 11. Internal Test Install Checklist

On tester device:

- [ ] Opt-in link opens correctly
- [ ] Tester can join test
- [ ] App listing opens in Play Store
- [ ] Install button appears
- [ ] App installs successfully
- [ ] App icon appears correctly
- [ ] App name appears correctly
- [ ] App opens without crash
- [ ] App version is correct
- [ ] App can be updated from Play Store when a new internal build is uploaded

---

## 12. Core Gameplay Test From Play Store Build

Run the same gameplay tests on the Play Store-installed version:

- [ ] MainMenu opens
- [ ] Play button works
- [ ] LevelSelect works
- [ ] GameScene opens
- [ ] Arrow tap works
- [ ] Arrow movement works
- [ ] Blocked path logic works
- [ ] WinLayer works
- [ ] LoseLayer works
- [ ] Restart works
- [ ] Next level works
- [ ] Save/load progress works after closing app
- [ ] Coins save/load if enabled
- [ ] Hint/Undo/Extra Chance do not break scene state

---

## 13. Device Compatibility Test

Test on at least one real Android phone.

Recommended:

```text
One low-end or older Android phone
One newer Android phone if available
```

Check:

```text
Screen scaling
Touch accuracy
Performance
Sound
Vibration
App resume after minimize
Back button behavior
```

---

## 14. Ads Test in Internal Testing

If ads are included in the internal build:

```text
Use test ads first
Do not click live production ads
Verify rewarded ad callback
Verify interstitial timing
Verify failed ad handling
```

Rewarded ad tests:

```text
Hint reward works
Extra chance reward works
Double reward works or is disabled
Cancelled ad gives no reward
```

Interstitial tests:

```text
No interstitial during gameplay
No interstitial before first level
No excessive frequency
After ad closes, player returns to correct flow
```

---

## 15. Build Update Test

Upload a second internal build with a higher version code.

Expected:

```text
Play Store offers update
Updated app installs correctly
Progress remains if app data is not cleared
New version opens without crash
```

This confirms the app can receive future updates.

---

## 16. Bug Report Format

Every internal testing bug must be written like this:

```text
Bug ID:
Build version:
Version code:
Device:
Android version:
Scene:
Level:
Steps to reproduce:
Expected result:
Actual result:
Severity: low / medium / high / critical
Status: open / fixed / retest / closed
```

Store bugs separately later in:

```text
docs/internal_testing_report.md
```

---

## 17. Severity Rules

### Critical

```text
App crashes
App cannot install
Main gameplay impossible
Save system corrupts progress
AAB rejected by Play Console
```

### High

```text
Level cannot be completed
Buttons fail often
Ads break gameplay
Progress does not save
UI unusable on phone
```

### Medium

```text
Small visual bug
Minor layout issue
Occasional animation problem
Unclear text
```

### Low

```text
Typo
Small cosmetic issue
Minor polish problem
```

Critical and high bugs block production release.

---

## 18. Internal Testing Exit Criteria

Internal testing is successful only when:

- [ ] App installs from Play Store internal test link
- [ ] App opens without crash
- [ ] Core gameplay works
- [ ] At least first 10 levels are verified for early test
- [ ] 50 levels are verified for release candidate
- [ ] Save/load works
- [ ] No critical bugs remain
- [ ] No high bugs remain
- [ ] Ads do not break gameplay if enabled
- [ ] Store listing draft is not misleading
- [ ] Privacy policy and Data Safety plan are consistent with build behavior

---

## 19. Common Problems

### Problem: Tester cannot install app

Check:

```text
Tester email is added to tester list
Tester opened opt-in link with correct Google account
Release is rolled out to internal testing
AAB processing is complete
Device is compatible
```

---

### Problem: Play Console rejects AAB

Check:

```text
Version code increased
Package name correct
AAB signed correctly
No broken manifest settings
Target SDK requirements satisfied by export
```

---

### Problem: App installs but crashes on open

Check:

```text
Starting scene exists
Missing assets
Bad scene transition
Export logs
Large unsupported assets
```

---

### Problem: Internal build does not update

Check:

```text
New version code is higher
Tester is on same testing track
Release rollout completed
Play Store cache may need time/refresh
```

---

## 20. Day 13 Acceptance Test

Day 13 is complete only when all checks pass:

- [ ] AAB is uploaded to internal testing
- [ ] Internal testing release is created
- [ ] Tester list is created
- [ ] Test opt-in link works
- [ ] App installs from Play Store
- [ ] App opens without crash
- [ ] Core gameplay works from Play Store install
- [ ] Save/load works from Play Store install
- [ ] Store-distributed update test is planned or completed
- [ ] Bugs are documented
- [ ] No critical blocker remains for MVP candidate

---

## 21. After Day 13

Next file to follow:

```text
docs/day_14_production_release_preparation.md
```

Day 14 goal:

```text
Prepare the final production release checklist: store listing, screenshots, final privacy policy, Data Safety, content rating, release notes, and launch gate.
```

---

## 22. Critical Rule

Internal testing is not a formality.

If the internal Play Store build fails, production release is blocked.
