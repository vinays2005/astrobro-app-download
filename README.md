# AstroBro website

Static landing page for the AstroBro Android app: features, plans, FAQ, a built-in help chat widget,
privacy/terms/refund pages, and the signed APK download.

## Deploy (Netlify)
Import this repo in Netlify. Build command: none. Publish directory: `.` (repo root).

## Releasing a new APK
1. Build: `flutter build apk --release --target-platform android-arm,android-arm64 --dart-define=BACKEND_API_KEY=...`
2. Copy `build/app/outputs/flutter-apk/app-release.apk` here as `AstroBro.apk`.
3. Update the SHA-256 shown in `index.html` (`sha256sum AstroBro.apk`) and the size, then commit and push.

## Before going live
Add a support email address to `privacy.html`, `terms.html` and `refund.html` (yellow notice boxes).
Optional live chat: create a free Tawk.to property and set `TAWK_EMBED` near the bottom of `index.html`.
