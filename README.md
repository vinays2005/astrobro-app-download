# Astrobro.ai website

Static landing page for the Astrobro.ai Android app: features, plans, FAQ, a built-in help chat widget,
privacy/terms/refund pages, and the signed APK download.

## Deploy (GitHub Pages)
Settings → Pages → source: `main` branch, `/` (root). The repo must be public (free Pages requires it).
Site: https://vinays2005.github.io/astrobro-app-download/

The APK itself is NOT committed to this repo — it lives as a GitHub Release asset instead (keeps the git
history small; a binary that changes every release doesn't belong in it).

## Releasing a new APK
1. Build: `flutter build apk --release --dart-define=BACKEND_API_KEY=...`
2. Create a release with the APK attached:
   `gh release create vX.Y.Z build/app/outputs/flutter-apk/app-release.apk --repo vinays2005/astrobro-app-download --title "Astrobro.ai vX.Y.Z" --notes "..."`
3. Update the download link in `index.html` to the new release's asset URL
   (`https://github.com/vinays2005/astrobro-app-download/releases/download/vX.Y.Z/AstrobroAI.apk`).
4. Update the SHA-256 shown in `index.html` (`sha256sum app-release.apk`) and the size, then commit and push.
5. Publish the new version code/name/URL in the admin dashboard's **Updates** tab so the in-app update
   screen picks it up.

## Before going live
Add a support email address to `privacy.html`, `terms.html` and `refund.html` (yellow notice boxes).
Optional live chat: create a free Tawk.to property and set `TAWK_EMBED` near the bottom of `index.html`.
