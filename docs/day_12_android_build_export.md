# Arrow Escape Master — Day 12 Android Build and Export

This document defines Day 12 tasks for **Arrow Escape Master** in GDevelop.

Day 12 goal:

```text
Export a working Android build from GDevelop, test it on a real Android phone, prepare AAB for Google Play, and confirm versioning, package name, signing, and install behavior.
```

This phase moves the project from editor gameplay to real mobile app testing.

---

## 1. Required Before Day 12

Day 11 must already be stable enough:

- [ ] Core gameplay works
- [ ] Levels load correctly
- [ ] LevelSelect works
- [ ] Save/load progress works
- [ ] At least 10 levels work for internal test
- [ ] 50-level plan exists
- [ ] UI is readable
- [ ] No critical crash is known
- [ ] Privacy policy draft exists
- [ ] Play Store plan exists

Do not export for Play Store if the game crashes inside GDevelop preview.

---

## 2. Day 12 Scope

Day 12 includes:

```text
Project settings review
Package name verification
Version name and version code
Android APK test build
Android AAB Play Store build
Signing check
Real Android phone install test
Basic performance test
Build artifact storage
Release notes draft
```

Day 12 does not include:

```text
Production Play Store release
Final store listing submission
Final Data Safety answers
Real in-app purchase setup
Post-launch analytics
```

---

## 3. Android Package Name

Final package name:

```text
com.foxboxstudio.arrowescapemaster
```

Rules:

```text
Use lowercase only
Do not use spaces
Do not change after Play Store release
Do not publish test package under final name unless ready
```

Critical:

```text
Changing package name after release creates a different app.
```

---

## 4. App Name

Final app name:

```text
Arrow Escape Master
```

Check that Android launcher name displays correctly.

---

## 5. Orientation and Resolution

Settings:

```text
Orientation: Portrait
Base resolution: 720 x 1280
```

Test on real device:

```text
No UI cut off
Board centered
Buttons visible
Text readable
```

---

## 6. Versioning

Use this sequence:

```text
0.1.0 = first internal Android test
0.2.0 = gameplay fixes
0.5.0 = MVP candidate
1.0.0 = public production release
```

Version code must increase every uploaded build:

```text
Version name: 0.1.0
Version code: 1

Version name: 0.1.1
Version code: 2

Version name: 0.2.0
Version code: 3
```

Rule:

```text
Never reuse an old version code in Play Console.
```

---

## 7. Build Types

### APK

Use APK for:

```text
Local phone testing
Fast install checks
Quick debugging
```

### AAB

Use AAB for:

```text
Google Play upload
Internal testing release
Production release
```

Google Play target build:

```text
Android App Bundle (.aab)
```

---

## 8. Pre-Build Checklist

Before exporting:

- [ ] Game opens in GDevelop preview
- [ ] MainMenu works
- [ ] GameScene works
- [ ] At least first 10 levels work
- [ ] Restart works
- [ ] Next button works
- [ ] LevelSelect works
- [ ] WinLayer works
- [ ] LoseLayer works
- [ ] Save/load works
- [ ] No debug-only visible objects remain
- [ ] PathChecker is hidden in release
- [ ] Temporary placeholder text is removed or acceptable for test
- [ ] App icon exists or temporary icon is acceptable for internal build
- [ ] Version name is set
- [ ] Version code is increased
- [ ] Package name is correct

---

## 9. Export APK for Local Test

In GDevelop:

```text
Share / Export
↓
Android
↓
APK build
↓
Use test/debug build settings if available
```

Output target folder:

```text
exports/android/apk/
```

Recommended file name:

```text
ArrowEscapeMaster_0.1.0_test.apk
```

---

## 10. Install APK on Android Phone

Methods:

```text
USB transfer
Telegram/file transfer to phone
Google Drive download
ADB install if available
```

If using ADB:

```powershell
adb install exports/android/apk/ArrowEscapeMaster_0.1.0_test.apk
```

If Android blocks install:

```text
Allow install from unknown sources for the file manager/browser used.
```

---

## 11. APK Device Test

On real phone, test:

- [ ] App installs successfully
- [ ] App icon appears
- [ ] App name appears correctly
- [ ] App opens without crash
- [ ] MainMenu button touch works
- [ ] GameScene touch works
- [ ] Arrow movement feels responsive
- [ ] PathChecker logic still works
- [ ] UI fits screen
- [ ] LevelSelect works
- [ ] Save/load works after closing app
- [ ] Back button behavior is acceptable
- [ ] Audio does not blast too loudly
- [ ] App does not freeze after multiple restarts

---

## 12. Screen Scaling Test

Test especially:

```text
Small phone screen
Tall Android screen
Navigation bar area
Top status bar area
```

Problems to look for:

```text
Buttons outside screen
Board too low/high
Text overlapping
Win/Lose popup cut off
Bottom buttons covered by navigation bar
```

Fix before AAB upload.

---

## 13. Performance Test

Minimum performance check:

```text
Play 10 levels in a row
Restart levels repeatedly
Open and close WinLayer/LoseLayer
Use hint/undo placeholders
Return to MainMenu and LevelSelect
```

Watch for:

```text
Lag
Freezing
Broken touch input
Objects not deleted
Memory growth symptoms
```

---

## 14. Export AAB for Google Play

In GDevelop:

```text
Share / Export
↓
Android
↓
Android App Bundle (.aab)
```

Output target folder:

```text
exports/android/aab/
```

Recommended file name:

```text
ArrowEscapeMaster_0.1.0_v1_internal.aab
```

---

## 15. Signing and Key Safety

Android builds must be signed.

Rules:

```text
Use Google Play App Signing when uploading to Play Console
Keep upload key safe
Do not delete signing credentials
Do not publish with random throwaway signing setup unless you understand the consequence
```

If a keystore/upload key is created, store details securely outside public GitHub.

Never commit private signing keys to GitHub.

Forbidden in repository:

```text
.keystore files
.jks files
private passwords
API secrets
AdMob private account data
```

---

## 16. GitHub Build Artifact Rule

Do not commit heavy build files unless intentionally needed.

Recommended:

```text
Keep APK/AAB locally
Upload AAB to Play Console
Use GitHub only for source, docs, levels, and safe assets
```

If adding export placeholders, keep:

```text
exports/android/.gitkeep
```

Do not commit production signing keys.

---

## 17. Build Notes File

For every Android build, write a short note.

Suggested file:

```text
docs/build_notes.md
```

Build note format:

```text
Build: 0.1.0
Version code: 1
Date:
Build type: APK/AAB
Purpose: Internal gameplay test
Known issues:
Test result:
```

---

## 18. Release Notes Draft

For internal testing version `0.1.0`:

```text
First internal test build.
Includes core arrow puzzle gameplay, MainMenu, GameScene, basic level flow, win/lose screens, and local progress testing.
```

For MVP candidate version `0.5.0`:

```text
MVP candidate with expanded levels, improved UI, coin and hint systems, and ad test integration.
```

---

## 19. Common Build Problems

### Problem: AAB upload fails because version code was reused

Fix:

```text
Increase version code
Re-export AAB
Upload again
```

---

### Problem: App opens to black screen

Check:

```text
Starting scene
Scene names
Missing assets
GDevelop export errors
Large unsupported assets
```

---

### Problem: Touch works in editor but not on phone

Check:

```text
Use touch conditions, not only mouse conditions
Button hitboxes
Layer positions
Screen scaling
```

---

### Problem: UI is cut off on phone

Check:

```text
Portrait resolution
Anchor positions
Bottom navigation bar
Safe area
Text size
```

---

### Problem: Build is too large

Check:

```text
Unused assets
Large PNGs
Uncompressed audio
Duplicate files
```

---

## 20. Day 12 Acceptance Test

Day 12 is complete only when all checks pass:

- [ ] Package name is correct
- [ ] App name is correct
- [ ] Version name is set
- [ ] Version code is increased
- [ ] APK exports successfully
- [ ] APK installs on Android phone
- [ ] App opens without crash
- [ ] Touch input works on phone
- [ ] Screen layout is acceptable
- [ ] Save/load works on phone
- [ ] AAB exports successfully
- [ ] AAB file is ready for Play Console internal testing
- [ ] Signing keys are not committed to GitHub
- [ ] Build notes are prepared

---

## 21. After Day 12

Next file to follow:

```text
docs/day_13_play_store_internal_testing.md
```

Day 13 goal:

```text
Upload AAB to Play Console internal testing, configure testers, install through Play Store, and verify the app as a real store-distributed build.
```

---

## 22. Critical Rule

Do not upload a broken AAB to production.

Internal testing exists to catch problems before public users see them.
