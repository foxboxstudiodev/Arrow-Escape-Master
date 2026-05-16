# Arrow Escape Master

**Arrow Escape Master** is a simple 2D mobile puzzle game planned for Google Play. The player taps arrows in the correct order to clear the board without collisions.

## Project Target

- Engine: GDevelop
- Platform: Android first
- Store: Google Play
- Package name: `com.foxboxstudio.arrowescapemaster`
- Monetization: AdMob rewarded ads + interstitial ads
- Game type: 2D puzzle / hyper-casual / offline

## Core Gameplay

The player sees a board filled with arrows. Each arrow has a direction. When tapped, the arrow tries to move forward and escape the board.

Rules:

1. If the path is clear, the arrow exits the board.
2. If another arrow or blocker is in the path, the move fails.
3. The level is completed when all arrows are removed.
4. The player loses after the allowed number of mistakes.
5. Harder levels add locks, keys, portals, color gates, and limited moves.

## Main Scenes

1. `BootScene` - loading and initial variables
2. `MainMenu` - Play, Level Select, Settings, Remove Ads
3. `LevelSelect` - level list and progress
4. `GameScene` - main puzzle gameplay
5. `WinPopup` - level completed screen
6. `LosePopup` - failed level screen
7. `Settings` - sound, vibration, language, privacy

## Main Objects

- `Arrow`
- `Wall`
- `Blocker`
- `ExitArea`
- `KeyArrow`
- `LockGate`
- `ColorGate`
- `PortalIn`
- `PortalOut`
- `HintButton`
- `UndoButton`
- `RestartButton`
- `NextButton`
- `CoinText`
- `LevelText`

## MVP Scope

Version 0.1 will include:

- Main menu
- 50 playable levels
- Arrow tap and movement logic
- Collision/fail detection
- Win/lose conditions
- Restart and next level
- Basic level select
- Coins
- Hint system
- Rewarded ad placeholder
- Interstitial ad placeholder

## Development Phases

### Phase 1 - Core Prototype

- Create GDevelop project
- Create GameScene
- Add Arrow object
- Add movement logic
- Add collision detection
- Add win/lose checks

### Phase 2 - Level System

- Build level structure
- Add 50 hand-made levels
- Save progress locally
- Add level select screen

### Phase 3 - Puzzle Depth

- Add locked arrows
- Add key arrows
- Add color gates
- Add portals
- Add limited moves

### Phase 4 - Monetization

- Add AdMob rewarded ads for hints
- Add interstitial ads after several levels
- Add remove ads button

### Phase 5 - Play Store Release

- Export Android AAB from GDevelop
- Prepare icon, screenshots, descriptions
- Add privacy policy
- Fill content rating and data safety forms
- Release to internal testing
- Publish production version

## Repository Structure

```text
Arrow-Escape-Master/
├─ README.md
├─ docs/
│  ├─ game_structure.md
│  ├─ level_design.md
│  ├─ monetization.md
│  ├─ playstore_plan.md
│  └─ privacy_policy_draft.md
├─ gdevelop/
│  └─ ArrowEscapeMaster.json
├─ assets/
│  ├─ arrows/
│  ├─ backgrounds/
│  ├─ buttons/
│  ├─ icons/
│  ├─ sounds/
│  └─ ui/
├─ levels/
│  ├─ levels.json
│  └─ level_format.md
└─ exports/
   └─ android/
```

## Final Product Goal

A clean, fast, offline, ad-monetized 2D puzzle game that can be published on Google Play and expanded with new levels after launch.
