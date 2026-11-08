# Agent Instructions — Finish Sky AR Android APK

## Goal
Produce a working debug APK that can be installed via `adb install` and shows the live sky AR overlay.

## Steps (execute in order)

1. `cd` into this directory.
2. `npm install`
3. `npx cap add android`
4. `npx cap sync android`
5. Edit `android/app/src/main/AndroidManifest.xml`:
   - Add CAMERA, ACCESS_FINE_LOCATION, ACCESS_COARSE_LOCATION, INTERNET, WAKE_LOCK permissions.
   - Add `android:usesCleartextTraffic="true"` on `<application>`.
6. `cd android && ./gradlew assembleDebug`
7. Confirm APK exists at `android/app/build/outputs/apk/debug/app-debug.apk`.
8. (Optional) `adb install -r android/app/build/outputs/apk/debug/app-debug.apk`

## Verification
- App launches without crash.
- “Start Sensors” requests camera + location.
- Overlay draws stars and (after Load Sats) green/red points for stations/visual objects.
- Screen stays on while active.

## Files that must not be deleted
- `www/index.html`
- `capacitor.config.json`
- `package.json`

## Expansion points (optional)
- Add more CelesTrak groups in `loadSats()` (`debris`, `rocket-bodies` if available).
- Increase star catalog size.
- Add app icon and splash.
- Sign for release.