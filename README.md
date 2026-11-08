# Sky AR — Capacitor Android App

Live camera overlay of stars, constellations, planets, satellites, and tracked debris.

## Build APK

```bash
cd sky-ar
npm install
npx cap add android
npx cap sync
npx cap open android
```

In Android Studio: Build → Build Bundle(s) / APK(s) → Build APK(s).

Or command line:

```bash
cd android
./gradlew assembleDebug
```

APK lands at `android/app/build/outputs/apk/debug/app-debug.apk`.

## Install via ADB

```bash
adb install -r app-debug.apk
```

## Permissions

Camera, Location, and Motion sensors are requested at runtime.  
Internet is required for live TLE fetch from CelesTrak.

## Monetization notes

- Debug APK can be sideloaded or sold directly.
- For Play Store: create a release keystore, build `assembleRelease`, upload to Google Play Console.
- Privacy policy required for location + camera.