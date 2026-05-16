# Arrow Escape Master — Asset Plan

This document defines the visual and audio asset plan for **Arrow Escape Master**.

The first release must look clean, simple, and polished. The game should not look like a raw prototype.

---

## 1. Visual Style Direction

Recommended first visual style:

```text
Clean 2D casual puzzle
Bright but not childish
Soft rounded UI
Clear arrows
Readable level board
Minimal distractions
```

The game should feel:

```text
Simple
Relaxing
Fast to understand
Mobile-friendly
```

Avoid:

```text
Too many colors
Complicated backgrounds
Small unreadable UI
Cheap clipart look
Overloaded effects
```

---

## 2. Required Asset Folders

Repository structure:

```text
assets/
├─ arrows/
├─ blockers/
├─ backgrounds/
├─ buttons/
├─ icons/
├─ ui/
├─ effects/
├─ sounds/
└─ store/
```

---

## 3. Arrow Assets

Main object:

```text
Arrow
```

Required sprites:

```text
arrow_up.png
arrow_right.png
arrow_down.png
arrow_left.png
```

Recommended size:

```text
256 x 256 source
96 x 96 in game
```

Style:

```text
Rounded arrow body
Thick clear direction head
Slight shadow
High contrast against board
```

Color variants for later phases:

```text
arrow_up_red.png
arrow_up_blue.png
arrow_up_green.png
arrow_up_yellow.png
arrow_right_red.png
arrow_right_blue.png
arrow_right_green.png
arrow_right_yellow.png
arrow_down_red.png
arrow_down_blue.png
arrow_down_green.png
arrow_down_yellow.png
arrow_left_red.png
arrow_left_blue.png
arrow_left_green.png
arrow_left_yellow.png
```

MVP required:

```text
Only 4 basic arrow sprites
```

---

## 4. Blocker Assets

Main object:

```text
Blocker
```

Required sprites:

```text
blocker_stone.png
blocker_wood.png
blocker_metal.png
```

Recommended size:

```text
256 x 256 source
96 x 96 in game
```

Style:

```text
Simple square/rounded tile
Clearly different from arrows
Does not look clickable
```

MVP required:

```text
blocker_stone.png
```

Wood and metal can be added after the prototype.

---

## 5. Board Assets

Required:

```text
board_background.png
board_cell.png
board_frame.png
```

Recommended board size:

```text
576 x 768
```

Based on:

```text
6 columns x 8 rows
Cell size 96
```

Style:

```text
Soft puzzle grid
Light background
Subtle cell separation
No visual noise
```

---

## 6. UI Button Assets

Required buttons:

```text
button_play.png
button_levels.png
button_settings.png
button_restart.png
button_hint.png
button_undo.png
button_next.png
button_replay.png
button_home.png
button_extra_chance.png
button_remove_ads.png
```

Recommended size:

```text
Main menu buttons: 300 x 90
Gameplay buttons: 120 x 90
Small icon buttons: 80 x 80
```

Style:

```text
Rounded rectangles
High readability
Consistent shadow
Large tap area
```

---

## 7. UI Panels

Required:

```text
panel_win.png
panel_lose.png
panel_pause.png
panel_settings.png
```

Recommended size:

```text
560 x 520
```

Style:

```text
Rounded panel
Soft shadow
Readable text contrast
```

---

## 8. Icons

Required app icons:

```text
app_icon_512.png
app_icon_foreground.png
app_icon_background.png
```

Main Play Store icon:

```text
512 x 512 PNG
```

Icon concept:

```text
Large arrow escaping from a small puzzle board
Clean background
Strong contrast
Readable at small size
```

Do not put too much text in the icon.

Recommended icon text:

```text
No text
```

---

## 9. Background Assets

Required:

```text
bg_main_menu.png
bg_game.png
bg_level_select.png
bg_settings.png
```

Style:

```text
Soft gradient or simple pattern
Does not distract from arrows
Works in portrait screen
```

Resolution:

```text
720 x 1280
```

---

## 10. Effects Assets

Optional but useful:

```text
particle_escape.png
particle_coin.png
flash_success.png
flash_fail.png
```

MVP required:

```text
None
```

Add effects after gameplay works.

---

## 11. Sound Assets

Required basic sounds:

```text
tap.wav
arrow_escape.wav
move_fail.wav
level_win.wav
level_lose.wav
coin.wav
button_click.wav
```

Audio style:

```text
Short
Soft
Not annoying
Mobile-friendly
```

Avoid:

```text
Long sounds
Harsh fail sounds
Loud music by default
Copyrighted audio
```

Music:

```text
No music in MVP unless very light and optional
```

---

## 12. Store Assets

Required for Google Play:

```text
store_icon_512.png
feature_graphic_1024x500.png
screenshot_01_main_menu.png
screenshot_02_easy_level.png
screenshot_03_harder_level.png
screenshot_04_win_screen.png
screenshot_05_level_select.png
screenshot_06_hint_reward.png
```

Recommended screenshot size:

```text
1080 x 1920 portrait
```

Store screenshot text overlays:

```text
Tap Arrows
Clear the Path
Solve Smart Puzzles
Use Hints
Unlock Levels
Play Offline
```

---

## 13. Asset Priority

Build assets in this order:

```text
1. Basic arrow sprites
2. Basic blocker sprite
3. Board background
4. Gameplay UI buttons
5. Win/Lose panels
6. Main menu UI
7. App icon
8. Store screenshots
9. Extra themes
10. Sound effects
```

---

## 14. MVP Minimum Asset Set

The minimum visual set required for the first playable prototype:

```text
arrow_up.png
arrow_right.png
arrow_down.png
arrow_left.png
blocker_stone.png
board_background.png
button_restart.png
button_next.png
panel_win.png
panel_lose.png
```

The first prototype can use simple temporary shapes, but the public release cannot.

---

## 15. Theme Plan

First release theme:

```text
Classic
```

Future themes:

```text
Neon
Wood
Space
Candy
Dark Mode
```

Do not build theme system before core gameplay works.

---

## 16. Asset Naming Rules

Use lowercase file names with underscores:

Correct:

```text
arrow_up.png
button_restart.png
panel_win.png
```

Wrong:

```text
Arrow Up.png
restartButton.PNG
win-panel-final-new2.png
```

---

## 17. Copyright Rule

Do not use random images from Google search.

Allowed asset sources:

```text
Self-created assets
AI-generated assets checked for commercial use
Licensed asset packs
Public domain / CC0 assets
Custom vector drawings
```

Every asset used in the public release must be safe for commercial use.

---

## 18. Quality Gate

Assets are ready for MVP when:

```text
All arrows are clearly readable
Board grid is easy to understand
Buttons are large enough for mobile touch
Win/Lose screens look complete
App icon is readable at small size
Screenshots show real gameplay
No copyrighted material is used
```

---

## 19. Critical Rule

Gameplay clarity is more important than decorative graphics.

The player must instantly understand:

```text
Which object is an arrow
Which direction it moves
What blocks the path
When the level is completed
Why a move failed
```
