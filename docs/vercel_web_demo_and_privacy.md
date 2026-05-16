# Arrow Escape Master — Vercel Web Demo and Privacy Plan

This document defines how **Vercel** will be used for Arrow Escape Master.

Vercel is not the main build system for the Android game. The Android version must still be exported from GDevelop as an APK/AAB. Vercel is used for the web demo, landing page, and privacy policy URL.

---

## 1. Final Decision

Approved setup:

```text
Game engine: GDevelop
Source/backup: GitHub
Android build: GDevelop Android export
Google Play upload: Play Console
Web demo: Vercel
Privacy policy URL: Vercel
Landing page: Vercel
```

Vercel will not replace GDevelop or Google Play Console.

---

## 2. What Vercel Is Used For

Use Vercel for:

```text
1. Public web demo of the game
2. Privacy Policy page
3. Simple landing page
4. Optional support/contact page
5. Optional Play Store link page after release
```

Example future URLs:

```text
https://arrow-escape-master.vercel.app
https://arrow-escape-master.vercel.app/privacy
https://arrow-escape-master.vercel.app/game
https://arrow-escape-master.vercel.app/support
```

---

## 3. What Vercel Is Not Used For

Do not use Vercel for:

```text
Android AAB build
APK build
Play Store upload
AdMob mobile build replacement
GDevelop project editing
Signing Android builds
Storing private keys
```

Main Android production path remains:

```text
GDevelop → Android AAB → Google Play Console → Internal testing → Production
```

---

## 4. Repository Structure for Vercel

Add this structure later:

```text
Arrow-Escape-Master/
├─ docs/
├─ levels/
├─ gdevelop/
├─ assets/
├─ web/
│  ├─ index.html
│  ├─ privacy.html
│  ├─ support.html
│  ├─ game/
│  │  ├─ index.html
│  │  ├─ gd.js
│  │  ├─ data.js
│  │  ├─ assets/
│  │  └─ other GDevelop HTML5 export files
│  └─ styles/
│     └─ main.css
└─ vercel.json
```

The `web/` folder will be the Vercel project root.

---

## 5. Web Folder Purpose

### `web/index.html`

Purpose:

```text
Landing page for Arrow Escape Master.
```

It should include:

```text
Game name
Short description
Game screenshot or icon
Play web demo button
Privacy Policy link
Support/contact link
Google Play link after release
```

---

### `web/privacy.html`

Purpose:

```text
Public Privacy Policy page for Play Console.
```

This page will be based on:

```text
docs/privacy_policy_draft.md
```

Before Play Store production release, the final privacy policy must be copied or converted into this page.

---

### `web/support.html`

Purpose:

```text
Simple contact/support page.
```

It should include:

```text
Developer name
Contact email
Game name
Basic support message
```

---

### `web/game/`

Purpose:

```text
HTML5 export from GDevelop.
```

When GDevelop exports the web version, the exported files should be placed inside:

```text
web/game/
```

The playable web game URL should become:

```text
https://arrow-escape-master.vercel.app/game
```

---

## 6. GDevelop Web Export Flow

When the game is stable enough:

```text
Open GDevelop
↓
Open ArrowEscapeMaster project
↓
Export
↓
Web / HTML5
↓
Export to local folder
↓
Copy exported files into web/game/
↓
Commit and push to GitHub
↓
Vercel deploys automatically
```

Do not export web demo before the basic gameplay works.

---

## 7. Vercel Deployment Flow

Steps:

```text
1. Go to Vercel
2. Connect GitHub account
3. Import repository: foxboxstudiodev/Arrow-Escape-Master
4. Set project root directory to web
5. Build command: leave empty for static HTML
6. Output directory: leave default or use .
7. Deploy
```

If using only static HTML files, no framework build is needed.

---

## 8. `vercel.json` Plan

Optional file:

```text
vercel.json
```

Possible simple config:

```json
{
  "cleanUrls": true,
  "trailingSlash": false
}
```

This is optional. The first version can work without it.

---

## 9. Privacy Policy URL for Play Console

After deploy, use this URL in Play Console:

```text
https://arrow-escape-master.vercel.app/privacy
```

Before using it in Play Console, verify:

```text
Page opens publicly
No login required
Policy includes developer contact email
Policy matches actual AdMob/SDK behavior
Effective date is added
```

---

## 10. Landing Page Content Draft

Landing page headline:

```text
Arrow Escape Master
```

Subtitle:

```text
Tap arrows, clear the path, and solve relaxing escape puzzles.
```

Buttons:

```text
Play Web Demo
Privacy Policy
Support
Google Play — coming soon
```

Short page text:

```text
Arrow Escape Master is a simple puzzle game where every arrow moves in its own direction. Plan the right order, clear the board, and complete smart escape levels.
```

---

## 11. Support Page Draft

Support text:

```text
For questions, feedback, or support related to Arrow Escape Master, contact FoxBoxStudio Dev.
```

Contact email:

```text
To be added before release
```

Do not publish without a working developer email.

---

## 12. Web Demo Rules

The web demo should not replace the mobile game.

Purpose of web demo:

```text
Show gameplay quickly
Test first impressions
Share link with testers
Use as simple marketing page
```

Rules:

```text
Web demo can have fewer levels than Android version
Web demo may not include AdMob
Web demo must not collect unnecessary user data
Web demo must not show fake gameplay
```

---

## 13. Android vs Web Differences

Android version:

```text
Google Play release
AdMob rewarded/interstitial ads
Mobile save system
AAB package
Phone-first experience
```

Web version:

```text
Browser demo
No Play Store install required
Useful for quick testing
Useful for landing page
May have limited monetization or no ads
```

Do not assume every Android feature must exist in the web demo.

---

## 14. Security Rules

Never commit these to GitHub or Vercel:

```text
Android signing keys
Keystore files
Passwords
Private API keys
AdMob account secrets
Personal documents
```

Allowed in repo:

```text
Static HTML
CSS
Public images
GDevelop web export files
Privacy policy text
Support page text
```

---

## 15. Vercel Testing Checklist

After deployment:

- [ ] Landing page opens
- [ ] Privacy page opens
- [ ] Support page opens
- [ ] Game demo opens if exported
- [ ] Mobile browser layout is readable
- [ ] Privacy URL is public
- [ ] No broken links
- [ ] No missing images
- [ ] No private files are exposed
- [ ] Google Play coming soon link is not misleading

---

## 16. When to Add Vercel

Correct timing:

```text
After GDevelop Day 02 or Day 03, create basic landing/privacy pages
After game prototype works, add web demo
Before Play Store release, finalize privacy policy URL
```

Do not spend too much time on Vercel before the actual game works.

---

## 17. Day Plan Integration

Vercel work fits into roadmap like this:

```text
After Day 02: create web landing skeleton
After Day 07: add privacy page draft
After Day 10: add screenshots/icon to landing page
After Day 12: add Play Store coming soon / internal testing note
Before Day 14: finalize Privacy Policy URL
```

---

## 18. Acceptance Test

Vercel setup is complete only when:

- [ ] `web/` folder exists
- [ ] Landing page exists
- [ ] Privacy page exists
- [ ] Support page exists
- [ ] Vercel project is connected to GitHub
- [ ] Public URL works
- [ ] Privacy Policy URL works without login
- [ ] No private files are exposed
- [ ] Play Console can use the Privacy Policy URL

---

## 19. Final Rule

Vercel is a support layer, not the core game pipeline.

The main production path remains:

```text
GDevelop project → Android AAB → Play Console → Internal testing → Production release
```
