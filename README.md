# Sky AR — Full Build Handoff

Complete Capacitor Android project for a live sky AR viewer.
Coding agent: finish Android platform generation, permissions, and APK build.

## What is already done
- `www/index.html` — full viewer (stars, constellations, planets via astronomy-engine, live sats/debris via satellite.js + CelesTrak, Wake Lock)
- `capacitor.config.json` — appId `com.orbitalreclaim.skyar`, appName `Sky AR`
- `package.json` — Capacitor 6 deps + build scripts

## What the agent must complete

### 1. Generate Android platform
```bash
npm install
npx cap add android
npx cap sync android
```

### 2. Android permissions (edit `android/app/src/main/AndroidManifest.xml`)
Add inside `<manifest>`:
```xml
<uses-permission android:name="android.permission.CAMERA" />
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.WAKE_LOCK" />
<uses-feature android:name="android.hardware.camera" android:required="false" />
<uses-feature android:name="android.hardware.sensor.compass" android:required="false" />
```

Inside `<application>` add:
```xml
android:usesCleartextTraffic="true"
```

### 3. Build debug APK
```bash
cd android
./gradlew assembleDebug
```
Output: `android/app/build/outputs/apk/debug/app-debug.apk`

### 4. Install via ADB
```bash
adb install -r app-debug.apk
```

## Live browser test
Open `www/index.html` or the hosted preview.
Tap **Start Sensors** then **Load Sats**.

Repo: https://github.com/Dmgedgoodz/constellation-ar