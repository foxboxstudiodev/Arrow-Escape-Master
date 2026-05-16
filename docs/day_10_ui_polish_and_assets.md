# Arrow Escape Master — Day 10 UI Polish and Assets

This document defines Day 10 tasks for **Arrow Escape Master** in GDevelop.

Day 10 goal:

```text
Replace temporary prototype visuals with clean mobile-ready assets, improve UI readability, prepare app icon direction, and make the game look like a real Google Play product.
```

This phase must improve presentation without breaking gameplay.

---

## 1. Required Before Day 10

Day 09 must already be complete or safely deferred:

- [ ] Core gameplay works
- [ ] LevelSelect works
- [ ] Progress save/load works
- [ ] Coins and hint flow work
- [ ] Undo / Extra Chance flow works or placeholders are stable
- [ ] AdMob plan exists
- [ ] Temporary UI does not crash the game
- [ ] No major gameplay bug is open

Do not polish visuals while gameplay is broken.

---

## 2. Day 10 Scope

Day 10 includes:

```text
Arrow sprites
Blocker sprites
Board background
MainMenu UI
GameScene UI
WinLayer UI
LoseLayer UI
Button styling
Font/readability pass
Basic sound effects
App icon concept
Store screenshot plan
Theme direction
```

Day 10 does not include:

```text
Adding 50 final levels
Play Store upload
Final AAB export
In-app purchase implementation
Complex animations
Advanced theme shop
```

---

## 3. Visual Style Decision

Approved style:

```text
Clean 2D casual puzzle
Bright but not childish
Soft rounded UI
Clear arrows
Readable board
Relaxing mobile look
```

Avoid:

```text
Messy backgrounds
Low contrast arrows
Small buttons
Random colors
Copyrighted assets
Overloaded animations
```

---

## 4. Required Asset Folders

Confirm these folders exist:

```text
assets/arrows
assets/blockers
assets/backgrounds
assets/buttons
assets/icons
assets/ui
assets/effects
assets/sounds
assets/store
```

If any folder is missing, create it before adding assets.

---

## 5. Arrow Assets

Required MVP arrow sprites:

```text
assets/arrows/arrow_up.png
assets/arrows/arrow_right.png
assets/arrows/arrow_down.png
assets/arrows/arrow_left.png
```

Recommended source size:

```text
256 x 256 PNG
```

In-game size:

```text
96 x 96
```

Arrow design rules:

```text
Direction must be readable instantly
Arrow head must be large
Shape must contrast with board
Slight shadow is allowed
Do not add text on arrow
```

---

## 6. Arrow Animation Mapping

In GDevelop `Arrow` object:

```text
Animation 0 = arrow_up.png
Animation 1 = arrow_right.png
Animation 2 = arrow_down.png
Animation 3 = arrow_left.png
```

Direction mapping must remain:

```text
up    → animation 0
right → animation 1
down  → animation 2
left  → animation 3
```

Do not change this mapping after events are built.

---

## 7. Blocker Assets

Required MVP blocker:

```text
assets/blockers/blocker_stone.png
```

Optional later:

```text
assets/blockers/blocker_wood.png
assets/blockers/blocker_metal.png
```

Recommended source size:

```text
256 x 256 PNG
```

In-game size:

```text
96 x 96
```

Design rules:

```text
Blocker must look non-clickable
Blocker must be visually different from arrow
Blocker must clearly occupy one grid cell
```

---

## 8. Board Assets

Required:

```text
assets/backgrounds/board_background.png
assets/backgrounds/game_background.png
```

Board size:

```text
576 x 768
```

Game background size:

```text
720 x 1280
```

Board rules:

```text
Cells must be readable
Grid must not be too dark
Board must not distract from arrows
Board edges must be clear
```

---

## 9. MainMenu UI Assets

Required:

```text
assets/backgrounds/bg_main_menu.png
assets/buttons/button_play.png
assets/buttons/button_levels.png
assets/buttons/button_settings.png
assets/buttons/button_remove_ads.png
```

Text can remain as GDevelop Text objects if buttons are simple backgrounds.

MainMenu must show:

```text
Game title
Play button
Level select button
Settings button
Remove ads placeholder if used
Coin display if needed
```

---

## 10. GameScene UI Assets

Required:

```text
assets/buttons/button_restart.png
assets/buttons/button_hint.png
assets/buttons/button_undo.png
assets/buttons/button_home.png
```

GameScene UI must show:

```text
LevelText
CoinText
MistakeText
MoveText
RestartButton
HintButton
UndoButton
```

Rules:

```text
UI must not cover board
Buttons must be large enough for thumb tapping
Important text must be readable on small Android phones
```

---

## 11. WinLayer Assets

Required:

```text
assets/ui/panel_win.png
assets/buttons/button_next.png
assets/buttons/button_replay.png
assets/buttons/button_double_reward.png
```

WinLayer must show:

```text
LEVEL COMPLETE
Coin reward
Next button
Replay button
Double reward button if enabled
```

Rules:

```text
Base reward must be clear
Next action must be obvious
Do not make Double Reward more important than Next
```

---

## 12. LoseLayer Assets

Required:

```text
assets/ui/panel_lose.png
assets/buttons/button_restart.png
assets/buttons/button_extra_chance.png
assets/buttons/button_home.png
```

LoseLayer must show:

```text
LEVEL FAILED
Restart button
Extra Chance button
Home button if used
```

Rules:

```text
Restart must always be available
Extra Chance must be optional
Do not trap player behind ad or coin requirement
```

---

## 13. Font and Text Rules

Use one clean readable font.

Text size recommendations:

```text
Game title: 56–72 px
Menu buttons: 32–40 px
HUD text: 24–32 px
Popup title: 42–56 px
Popup buttons: 30–38 px
```

Rules:

```text
No tiny text
No low-contrast text
No too many font styles
No text overlapping buttons
```

---

## 14. Sound Effects

Required basic sounds:

```text
assets/sounds/button_click.wav
assets/sounds/arrow_escape.wav
assets/sounds/move_fail.wav
assets/sounds/level_win.wav
assets/sounds/level_lose.wav
assets/sounds/coin.wav
```

Rules:

```text
Short sounds only
No harsh fail sounds
No copyrighted audio
Sound must respect SoundEnabled variable
```

MVP can launch without background music.

---

## 15. Visual Feedback

Minimum feedback needed:

```text
Arrow tap feedback
Arrow escape movement
Blocked move shake or flash
Coin reward text on win
Button press feedback
```

Avoid complex effects until gameplay is stable.

---

## 16. App Icon Plan

Required file:

```text
assets/icons/app_icon_512.png
```

Size:

```text
512 x 512 PNG
```

Icon concept:

```text
A bold arrow escaping from a small puzzle board
Clean background
Strong contrast
No small text
```

Do not include the full game name inside the icon.

Reason:

```text
Small text becomes unreadable on phone screens.
```

---

## 17. Feature Graphic Plan

Required file:

```text
assets/store/feature_graphic_1024x500.png
```

Size:

```text
1024 x 500
```

Concept:

```text
Arrow Escape Master title
Board with arrows
Clean puzzle feel
No misleading gameplay claims
```

---

## 18. Screenshot Plan

Required store screenshots:

```text
assets/store/screenshot_01_main_menu.png
assets/store/screenshot_02_easy_level.png
assets/store/screenshot_03_puzzle_order.png
assets/store/screenshot_04_win_screen.png
assets/store/screenshot_05_level_select.png
assets/store/screenshot_06_hint_reward.png
```

Recommended screenshot size:

```text
1080 x 1920 portrait
```

Overlay text ideas:

```text
Tap Arrows
Clear the Path
Solve Smart Puzzles
Use Hints
Unlock Levels
Play Offline
```

Screenshots must show real gameplay, not fake scenes.

---

## 19. Theme Plan

First release theme:

```text
Classic
```

Later themes:

```text
Neon
Wood
Space
Dark
Candy
```

Do not build a theme shop before release. Only prepare visual direction.

---

## 20. Copyright and License Rule

Allowed:

```text
Self-created assets
Commercial-use licensed assets
CC0 assets
AI-generated assets checked for commercial safety
Custom vector drawings
```

Forbidden:

```text
Random Google Images
Assets copied from another game
Unlicensed icons
Copyrighted music/sounds
Screenshots from other games
```

---

## 21. Asset Replacement Order

Replace temporary visuals in this order:

```text
1. Arrow sprites
2. Blocker sprite
3. Board background
4. GameScene HUD buttons
5. Win/Lose panels
6. MainMenu UI
7. LevelSelect UI
8. Sounds
9. App icon
10. Store screenshots
```

Do not replace everything at once. Test after each group.

---

## 22. Testing After Asset Replacement

After replacing every asset group, test:

```text
Game opens
Scene loads
Object size is correct
Collision still works
PathChecker still works
Buttons still work
Text is readable
No asset is missing
No performance issue appears
```

Especially check:

```text
Changing Arrow sprite does not change collision mask incorrectly
Changing Blocker sprite does not break blocking
Changing UI does not cover board
```

---

## 23. Common Problems

### Problem: Arrow collision changes after new sprite

Check:

```text
Collision mask
Object size
Origin point
Hitbox matches 96 x 96 cell
```

---

### Problem: UI looks good in editor but bad on phone

Check:

```text
Screen scaling
Safe area
Button sizes
Text size
Portrait layout
```

---

### Problem: Store icon unreadable

Check:

```text
No small text
Large arrow shape
Strong contrast
Simple background
```

---

### Problem: Game feels visually noisy

Check:

```text
Too many colors
Too much background detail
Effects too strong
Board not readable
```

---

## 24. Day 10 Acceptance Test

Day 10 is complete only when all checks pass:

- [ ] Arrow sprites are added
- [ ] Arrow animations match directions
- [ ] Blocker sprite is added
- [ ] Board background is added
- [ ] MainMenu looks clean
- [ ] GameScene HUD is readable
- [ ] WinLayer looks complete
- [ ] LoseLayer looks complete
- [ ] Buttons are large enough for mobile
- [ ] Basic sounds are added or intentionally deferred
- [ ] App icon concept/file exists
- [ ] Screenshot plan is ready
- [ ] No copyrighted assets are used
- [ ] Gameplay still works after asset replacement
- [ ] PathChecker still works after asset replacement

---

## 25. After Day 10

Next file to follow:

```text
docs/day_11_50_level_expansion.md
```

Day 11 goal:

```text
Expand from 10 prototype levels to 50 release-ready levels with proper difficulty curve.
```

---

## 26. Critical Rule

Polish must not break gameplay.

A beautiful broken puzzle game is still a broken game.
