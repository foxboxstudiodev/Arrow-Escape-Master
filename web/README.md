# Arrow Escape Master — Web Folder

This folder is used as the Vercel root directory.

## Purpose

The `web/` folder contains the public static website for Arrow Escape Master:

```text
/          Landing page
/privacy   Privacy Policy page
/support   Support page
/game      Web demo placeholder or future GDevelop HTML5 export
```

## Vercel Settings

When importing the GitHub repository into Vercel, use:

```text
Repository: foxboxstudiodev/Arrow-Escape-Master
Root Directory: web
Framework Preset: Other
Build Command: empty
Output Directory: empty/default
Install Command: empty
```

The site is static HTML/CSS. No Node.js framework is required for the first version.

## Important Files

```text
index.html          Main landing page
privacy.html        Privacy Policy page
support.html        Support/contact page
game/index.html     Web demo placeholder
styles/main.css     Shared styles
```

## Future GDevelop Web Demo

After the GDevelop prototype is ready:

```text
1. Export HTML5/Web from GDevelop.
2. Copy exported files into web/game/.
3. Replace the current placeholder page.
4. Commit and push to GitHub.
5. Vercel deploys automatically.
```

## Privacy Policy URL

After deployment, the expected Privacy Policy URL will be:

```text
https://arrow-escape-master.vercel.app/privacy
```

Before using it in Google Play Console, update:

```text
Effective date
Developer contact email
Final AdMob / SDK details
Data Safety consistency
```
