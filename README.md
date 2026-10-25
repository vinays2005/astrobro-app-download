# Astrobro.ai website

Static landing page for the Astrobro.ai Android app: features, plans, FAQ, a built-in help chat widget,
privacy/terms/refund pages, and the signed APK download.

## Deploy (GitHub Pages)
Settings → Pages → source: `main` branch, `/` (root). The repo must be public (free Pages requires it).
Site: https://vinays2005.github.io/astrobro-app-download/

The APK itself is NOT committed to this repo — it lives as a GitHub Release asset instead (keeps the git
history small; a binary that changes every release doesn't belong in it).

## Releasing a new APK
1. Bump `version:` in the Flutter project's `pubspec.yaml` (the `+N` build number is what the in-app
   update screen compares against; it must go up).
2. Build: `flutter build apk --release --dart-define=BACKEND_API_KEY=...` (or `./build_release.sh`,
   which reads the key from the backend's `.env` for you).
3. Create a release with the APK attached, **keeping the asset named `AstrobroAI.apk`** — every URL that
   points at a release (`index.html`'s download button, and the admin dashboard's default APK URL) uses
   GitHub's evergreen `/releases/latest/download/AstrobroAI.apk` alias, which only resolves correctly
   when every release's asset keeps that exact filename:
   `gh release create vX.Y.Z AstrobroAI.apk --repo vinays2005/astrobro-app-download --title "AstroBro AI vX.Y.Z" --notes "..."`
4. Update the SHA-256 and the file size shown in `index.html` (`sha256sum AstrobroAI.apk`), then commit
   and push. The download link itself does not need editing — it's the evergreen alias above, not a
   version-pinned URL, so step 4 is only the checksum and size now.
5. Publish the new version code/name in the admin dashboard's **App update** section (Notifications
   page) so the in-app update screen picks it up. Its APK URL field already defaults to the same
   evergreen alias, so it only needs editing if you ever rename the asset.

## Before going live
Add a support email address to `privacy.html`, `terms.html` and `refund.html` (yellow notice boxes).
Optional live chat: create a free Tawk.to property and set `TAWK_EMBED` near the bottom of `index.html`.
