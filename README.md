# Yappy Hour Bingo — Public Static Build

A deployment-ready, mobile-first static website. It preserves the agreed 5×5 people-bingo experience and 24-prompt set while removing any dependency on Teams, SharePoint, authentication, a database, or server-side code.

**Live site:** https://sponnada.github.io/yappy-hour-bingo/

## Deploy

Upload **the contents of this folder** to the document root of any HTTPS static host. There is no build command and no environment configuration.

Compatible deployment patterns include:

- **GitHub Pages:** commit these files to the publishing branch/folder and enable Pages.
- **Azure Static Web Apps:** set the app location to this folder and leave the build/output steps empty. `staticwebapp.config.json` adds security headers.
- **Netlify or Cloudflare Pages:** publish this folder directly with no build command. `_headers` adds security and cache headers where supported.
- **Any web server/CDN:** copy the files to the public root and serve `index.html` for `/`.

The site works from a domain root or a subdirectory because all asset paths and service-worker scope are relative.

## Local preview

A web server is recommended because service workers are not enabled on `file://` URLs:

```bash
python3 -m http.server 8080 --directory .
```

Then open `http://localhost:8080/`.

## Included behavior

- Randomized 5×5 card using 24 agreed prompts and a FREE center square
- First-name entry from each tappable square
- Case-insensitive prevention of reusing a person on the same card
- Automatic row, column, and diagonal bingo detection
- Highlighted winning line, confetti, and celebratory win dialog
- Clear-names reset and fully randomized new-card flow
- Local progress persistence
- Responsive mobile/desktop UI, keyboard support, reduced-motion support, and screen-reader announcements
- Installable web-app manifest and same-origin offline cache
- Public privacy page, custom 404 page, robots file, icons, and social preview

## Privacy and security

- No authentication or account
- No backend or database
- No analytics, ads, tracking pixels, or third-party API calls
- Bingo entries remain in browser local storage and are not transmitted by the app
- First names only are requested
- Optional host configuration files set a restrictive same-origin Content Security Policy and disable sensitive browser permissions

A hosting provider may retain standard request logs according to its own policies; those logs do not contain the locally stored bingo entries.

## Production checklist

1. Deploy the folder over HTTPS.
2. Confirm `/`, `/manifest.webmanifest`, `/sw.js`, and `/privacy.html` return HTTP 200.
3. Open the site on a phone and enter one test name.
4. Refresh once to confirm local progress persistence.
5. If deploying a new version later, update `CACHE_NAME` in `sw.js` so clients receive the refreshed app shell.
