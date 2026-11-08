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

### 3. Runtime permissions (optional but recommended)
Create a small Capacitor plugin or use `@capacitor/geolocation` + camera plugin, or rely on WebView permission prompts. Current web code already requests camera, geolocation, and DeviceOrientation.

### 4. Build debug APK
```bash
cd android
./gradlew assembleDebug
```
Output: `android/app/build/outputs/apk/debug/app-debug.apk`

### 5. Install via ADB
```bash
adb install -r app-debug.apk
```

### 6. Release build (for selling)
```bash
# Create keystore once
keytool -genkey -v -keystore sky-ar.keystore -alias skyar -keyalg RSA -keysize 2048 -validity 10000

# Add signing config to android/app/build.gradle then:
./gradlew assembleRelease
```

## Live browser test (before APK)
Open `www/index.html` in Chrome on the phone, or host it.
Tap **Start Sensors** then **Load Sats**.

## Known limits
- CelesTrak TLE fetch requires network.
- DeviceOrientation absolute heading works best on Android Chrome; iOS needs permission.
- Star catalog is compact (bright stars only). Expand `STARS` array for more.
- Debris groups can be added by extending the `groups` array in `loadSats()`.

## Monetization path
1. Debug APK → sideload / direct sale (Gumroad, etc.)
2. Signed release APK → Google Play ($25 developer account)
3. Privacy policy required (camera + location)

Repo mirror: https://github.com/Dmgedgoodz/constellation-ar
Local handoff: this folder.