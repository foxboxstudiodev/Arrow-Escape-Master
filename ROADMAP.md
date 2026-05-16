# Arrow Escape Master — Roadmap

This roadmap defines the development path for **Arrow Escape Master**, a 2D mobile puzzle game built with GDevelop and prepared for Google Play release.

---

## Project Identity

- Game name: **Arrow Escape Master**
- Repository: `foxboxstudiodev/Arrow-Escape-Master`
- Engine: **GDevelop**
- First platform: **Android**
- Target store: **Google Play**
- Package name: `com.foxboxstudio.arrowescapemaster`
- Monetization: **AdMob rewarded ads + interstitial ads**
- Game type: **2D puzzle / hyper-casual / offline**

---

## Final Game Concept

The player taps arrows in the correct order to clear the board. Each arrow moves in its own direction. If the path is clear, the arrow escapes. If another arrow, wall, blocker, or locked object blocks the path, the move fails.

### Core Rule

```text
Tap arrow → arrow moves forward → clear path = success → blocked path = fail
```

### Level Completion

```text
All arrows removed → level completed
Mistake limit reached → level failed
```

---

## Phase 1 — Core Prototype

Goal: create the first playable version of the game.

### Tasks

- [ ] Create GDevelop project: `ArrowEscapeMaster`
- [ ] Create `GameScene`
- [ ] Add `Arrow` object
- [ ] Add direction system: up, down, left, right
- [ ] Add tap/click detection
- [ ] Add arrow movement logic
- [ ] Add board boundary detection
- [ ] Add collision detection
- [ ] Add successful arrow escape logic
- [ ] Add failed move logic
- [ ] Add level win condition
- [ ] Add level fail condition
- [ ] Add restart button
- [ ] Add next level button

### Result

A basic playable puzzle scene where arrows can be tapped and removed from the board.

---

## Phase 2 — Level System

Goal: build a scalable level system.

### Tasks

- [ ] Define level data format
- [ ] Create `levels/levels.json`
- [ ] Create first 10 test levels
- [ ] Add level loading logic
- [ ] Add current level variable
- [ ] Add level progress saving
- [ ] Add local storage save/load
- [ ] Create `LevelSelect` scene
- [ ] Add locked/unlocked level states
- [ ] Add level completed visual state

### Result

The game can load different levels and save player progress.

---

## Phase 3 — MVP Content

Goal: prepare the first real release candidate.

### Tasks

- [ ] Create 50 playable levels
- [ ] Add difficulty curve
- [ ] Add tutorial levels
- [ ] Add level groups: Easy, Normal, Hard
- [ ] Add move counter
- [ ] Add mistake counter
- [ ] Add level complete popup
- [ ] Add level failed popup
- [ ] Add basic sound effects
- [ ] Add vibration feedback
- [ ] Add pause/settings button

### Result

A complete MVP with enough content for internal testing.

---

## Phase 4 — Puzzle Depth

Goal: make the game more original and less like a simple clone.

### New Mechanics

- [ ] `KeyArrow` — unlocks locked objects
- [ ] `LockGate` — blocks arrows until unlocked
- [ ] `ColorGate` — only matching color arrows can pass
- [ ] `PortalIn` and `PortalOut` — redirects arrow movement
- [ ] Limited moves mode
- [ ] Boss puzzle every 10 levels

### Result

The game becomes more unique and has stronger retention potential.

---

## Phase 5 — Economy and Rewards

Goal: add simple player progression and reward loops.

### Tasks

- [ ] Add coin system
- [ ] Add coin reward after completed level
- [ ] Add extra coin reward for perfect completion
- [ ] Add hint cost
- [ ] Add undo cost
- [ ] Add daily reward placeholder
- [ ] Add simple skin/theme unlock structure

### Result

The game has a lightweight progression system suitable for casual players.

---

## Phase 6 — Hint and Undo System

Goal: improve player experience and prepare rewarded ads.

### Tasks

- [ ] Add `HintButton`
- [ ] Detect safe next arrow
- [ ] Highlight suggested arrow
- [ ] Add `UndoButton`
- [ ] Store previous move state
- [ ] Restore previous move state on undo
- [ ] Connect hint to coins
- [ ] Connect hint to rewarded ad placeholder

### Result

The player can continue difficult levels without immediate frustration.

---

## Phase 7 — Monetization

Goal: prepare the game for revenue.

### Ad Types

- Rewarded ad for hints
- Rewarded ad for undo
- Rewarded ad for extra chance after failure
- Interstitial ad after several completed levels
- Remove ads option placeholder

### Tasks

- [ ] Create AdMob account
- [ ] Create Android app in AdMob
- [ ] Add test ad IDs first
- [ ] Add rewarded ad events
- [ ] Add interstitial ad events
- [ ] Add ad frequency rules
- [ ] Add remove ads placeholder
- [ ] Test ads only in development mode

### Result

The game has monetization prepared without damaging user experience.

---

## Phase 8 — UI and Visual Polish

Goal: make the game look clean enough for Google Play.

### Tasks

- [ ] Design app icon
- [ ] Design main menu background
- [ ] Design arrow sprites
- [ ] Design button UI
- [ ] Design level select UI
- [ ] Add win animation
- [ ] Add fail animation
- [ ] Add arrow movement animation
- [ ] Add simple particle effect on escape
- [ ] Add 3 themes: Classic, Neon, Wood

### Result

The game looks complete, not like a prototype.

---

## Phase 9 — Testing

Goal: catch gameplay, UI, and build issues before Play Store submission.

### Tasks

- [ ] Test all 50 levels
- [ ] Check every level is solvable
- [ ] Check level fail conditions
- [ ] Check restart/next level buttons
- [ ] Check save/load progress
- [ ] Check coins and hints
- [ ] Check ads in test mode
- [ ] Test on at least one Android phone
- [ ] Fix screen scaling problems
- [ ] Fix touch input problems

### Result

The game is stable enough for internal testing release.

---

## Phase 10 — Play Store Preparation

Goal: prepare everything required for Google Play release.

### Store Assets

- [ ] App icon
- [ ] Feature graphic
- [ ] Phone screenshots
- [ ] Short description
- [ ] Full description
- [ ] Privacy policy
- [ ] Content rating
- [ ] Data safety form
- [ ] App category
- [ ] Target audience settings

### Technical Tasks

- [ ] Export Android AAB from GDevelop
- [ ] Sign build correctly
- [ ] Upload AAB to Play Console
- [ ] Create internal testing release
- [ ] Test install from Play Store internal testing
- [ ] Fix policy or build issues
- [ ] Prepare production release

### Result

The game is ready for Google Play publication.

---

## Phase 11 — Post-Launch Updates

Goal: improve downloads, retention, and revenue after launch.

### Tasks

- [ ] Add 50 new levels
- [ ] Add daily challenge
- [ ] Add more themes
- [ ] Add better level difficulty balancing
- [ ] Review analytics
- [ ] Improve screenshots and store description
- [ ] Monitor crashes
- [ ] Optimize ad placement
- [ ] Add localization later if needed

### Result

The game continues improving after the first release.

---

## First Release Target

The first public version should include:

- Main menu
- Game scene
- Level select
- 50 levels
- Save progress
- Hint system
- Coins
- Basic ads
- Clean UI
- Android AAB build
- Google Play listing materials

---

## Development Rule

Do not build a weak prototype and publish it as final. Every phase must produce a clean, working, testable result before moving to the next phase.
