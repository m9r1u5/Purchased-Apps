# Purchased Apps

See every app you've ever bought on each of your Google accounts — offline, private, no login.

**Open the app:** https://m9r1u5.github.io/Purchased-Apps/

## How it works
Google has no public API for Play Store purchase history, so the app reads your **Google Takeout** export:

1. In the app, tap **Add Account** and enter a label (e.g. "Work Gmail") and the email.
2. Tap **Open Google Takeout** → **Deselect all** → tick only **Google Play Store** → **Next step** → **Export once**, **.zip** → **Create export**.
3. When Google emails you, download the .zip, return to the app and tap **Import**.

Re-importing for the same account merges and removes duplicates. All data is stored on the phone in IndexedDB — nothing is uploaded.

## Files (flat layout)
| File | Purpose |
|---|---|
| `index.html` | The whole app (UI, Takeout parser, IndexedDB, export) |
| `manifest.json` | PWA manifest |
| `sw.js` | Service worker (offline cache) |
| `version.json` | Version checked by the **Update** button |
| `icon-*.png`, `apple-touch-icon.png`, `favicon.png` | Icons |
| `.github/workflows/build-apk.yml` | Builds the Android APK with Capacitor |

## Releasing an update
1. Change `version.json` **and** `APP_VERSION` in `index.html` **and** `VERSION` in `sw.js` to the same new number (e.g. `1.0.1`).
2. Commit. Users tap **Update** and the app reloads with the new version.
3. For Android APK users, run the **Build Android APK** workflow again — the Update button sends them to the newest release.

## Build the APK from your phone
GitHub → this repo → **Actions** → **Build Android APK** → **Run workflow**. After ~5 minutes the APK is on the **Releases** page (and under the run's **Artifacts**).
