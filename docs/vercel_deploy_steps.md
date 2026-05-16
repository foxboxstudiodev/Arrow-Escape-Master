# Arrow Escape Master — Vercel Deploy Steps

This document defines the exact steps for deploying the Arrow Escape Master web pages to Vercel.

Vercel is used for:

```text
Landing page
Privacy Policy page
Support page
Web demo placeholder / future HTML5 demo
```

Vercel is not used for Android APK/AAB builds.

---

## 1. Current Web Structure

The repository already contains:

```text
web/
├─ index.html
├─ privacy.html
├─ support.html
├─ game/
│  └─ index.html
└─ styles/
   └─ main.css
```

The repository also contains:

```text
vercel.json
```

Current public routes after deployment should be:

```text
/          → landing page
/privacy   → privacy policy
/support   → support page
/game      → web demo placeholder
```

---

## 2. Important Deploy Decision

When importing the project into Vercel, set:

```text
Root Directory: web
```

Because all public HTML pages are inside the `web/` folder.

---

## 3. Step-by-Step Vercel Setup

### Step 1 — Open Vercel

Go to:

```text
https://vercel.com
```

Sign in with GitHub.

---

### Step 2 — Add New Project

Click:

```text
Add New...
↓
Project
```

---

### Step 3 — Import GitHub Repository

Select repository:

```text
foxboxstudiodev/Arrow-Escape-Master
```

Click:

```text
Import
```

---

### Step 4 — Configure Project

Set project name:

```text
arrow-escape-master
```

Set Framework Preset:

```text
Other
```

Set Root Directory:

```text
web
```

Build command:

```text
Leave empty
```

Output directory:

```text
Leave default
```

Install command:

```text
Leave empty
```

Reason:

```text
The website is static HTML/CSS. No build process is needed.
```

---

### Step 5 — Deploy

Click:

```text
Deploy
```

Wait until Vercel shows deployment success.

---

## 4. Expected URLs

After deploy, Vercel will provide a URL similar to:

```text
https://arrow-escape-master.vercel.app
```

Expected pages:

```text
https://arrow-escape-master.vercel.app
https://arrow-escape-master.vercel.app/privacy
https://arrow-escape-master.vercel.app/support
https://arrow-escape-master.vercel.app/game
```

If clean URLs do not work, try:

```text
https://arrow-escape-master.vercel.app/privacy.html
https://arrow-escape-master.vercel.app/support.html
https://arrow-escape-master.vercel.app/game/index.html
```

---

## 5. Vercel Test Checklist

After deploy, test:

- [ ] Landing page opens
- [ ] Privacy page opens
- [ ] Support page opens
- [ ] Game page opens
- [ ] Mobile layout looks acceptable
- [ ] Buttons work
- [ ] Back links work
- [ ] No 404 on main pages
- [ ] No private files are visible
- [ ] Privacy URL is public without login

---

## 6. Privacy Policy URL for Play Console

Use this URL later in Play Console:

```text
https://arrow-escape-master.vercel.app/privacy
```

Before using it officially:

- [ ] Add final effective date
- [ ] Add final developer email
- [ ] Confirm AdMob details
- [ ] Confirm Data Safety answers match real build
- [ ] Confirm the page is publicly accessible

---

## 7. Future Web Demo Update

When the GDevelop web export is ready:

```text
1. Export HTML5/Web from GDevelop
2. Copy exported files into web/game/
3. Replace the placeholder web/game/index.html
4. Commit changes
5. Push to GitHub
6. Vercel deploys automatically
```

Do not replace the placeholder until the GDevelop prototype works.

---

## 8. Common Problems

### Problem: Vercel shows 404

Check:

```text
Root Directory is set to web
index.html exists inside web/
Deployment finished successfully
```

---

### Problem: CSS does not load

Check:

```text
web/styles/main.css exists
HTML uses styles/main.css
File path is case-sensitive
```

---

### Problem: /privacy does not open

Try:

```text
/privacy.html
```

If clean URLs fail, Vercel config may need adjustment.

---

### Problem: Repo not visible in Vercel

Check:

```text
GitHub account connected to Vercel
Vercel has access to foxboxstudiodev/Arrow-Escape-Master
Repository is selected during import
```

---

## 9. Critical Rule

Vercel deployment must stay simple.

No framework is required for the first version. Static HTML/CSS is enough for landing page, privacy policy, support page, and web demo placeholder.
