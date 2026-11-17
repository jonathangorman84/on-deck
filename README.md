# On Deck launcher (GitHub Pages)

Static wrapper so iPhone, Pixel, and Samsung can “Add to Home Screen” with the On Deck icon. The page iframes the live Apps Script web app.

The live `/exec` app already sets `XFrameOptionsMode.ALLOWALL`, so framing should work without a new Apps Script deploy. A fallback “Open On Deck” link is on the page if the iframe is blocked.

## App name

Default display name is **On Deck** (the logo text). The Apps Script project title is “Port App”. To rename, change `name` and `short_name` in `manifest.webmanifest` and the `<title>` / `application-name` / `apple-mobile-web-app-title` values in `index.html`.

## Publish on GitHub Pages

`gh` on this box is installed but not logged in, and there are no stored git credentials. After logging in on a machine that can push:

1. Create a public repo (public is required so the icons are reachable for `setFaviconUrl` later), for example `on-deck-launcher`.
2. Copy the contents of this `launcher/` folder to the repo root (or set Pages to serve this folder).
3. Enable GitHub Pages (Settings → Pages → Deploy from a branch, usually `main` / root).
4. The site URL will be `https://<user>.github.io/<repo>/`.
5. On each phone, open that Pages URL in Safari (iPhone) or Chrome (Pixel / Samsung), then Add to Home Screen. The 180px apple-touch-icon is used on iOS; the Web App Manifest icons (192, 512, 512 maskable) are used on Android.

## Optional Apps Script tab icon

The prepared copy at `../apps-script-next/Code.gs` adds `setFaviconUrl`, gated on a placeholder:

```
var FAVICON_URL = ''; // REPLACE_WITH_PUBLIC_PNG_URL
```

After Pages is live, set that to `https://<user>.github.io/<repo>/icons/icon-192.png`, paste the file into the Apps Script editor, Save, then **Deploy → Manage deployments → Edit → New version → Deploy**. Do not put that URL in an Index.html JS string as `https://` — in HtmlService JS strings write `https:\/\/`.
