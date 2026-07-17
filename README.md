# Prism Drift — Tilt

An endless drifter you steer entirely by tilting your phone. Tip the top edge
**back toward you to rise**, **forward to fall**, and thread the glowing gaps.
Packaged for Android as an installable APK using [Capacitor](https://capacitorjs.com/).

The whole game lives in a single file: [`www/index.html`](www/index.html).

## Controls

- **Gyro only.** However you're holding the phone when you tap **START** becomes
  "level." Tilt back to go up, forward to go down; tilt further to drift faster.
- **Re-center** button — re-captures "level" if your grip drifts.
- **Invert** button — flips the up/down direction if it feels backwards.
- No gyroscope on the device? The game shows a message instead of starting —
  it needs motion sensors to play.

## Getting the APK (no tools to install)

The APK builds automatically on GitHub Actions.

1. Push this repo to GitHub (already done if you're reading this there).
2. Open the **Actions** tab → **Build Android APK** → the latest run.
3. Download **`prism-drift-apk`** from the run's **Artifacts** section.
4. Unzip it, copy `prism-drift.apk` to your phone, and open it to install.
   You'll need to allow "install from unknown sources" — this is a debug/side-load
   build, not a Play Store listing.

### Tagged releases

Push a tag to also attach the APK to a GitHub Release:

```bash
git tag v1.0.0
git push origin v1.0.0
```

The APK then appears under **Releases**.

## Building locally (optional)

Requires Node.js 20+, JDK 17, and the Android SDK (Android Studio is easiest).

```bash
npm install
npx cap add android      # generates the native android/ project
npx cap sync android
cd android && ./gradlew assembleDebug
# APK: android/app/build/outputs/apk/debug/app-debug.apk
```

Or open it in Android Studio with `npx cap open android` and press Run.

## Notes

- App is locked to **portrait** (CI patches the Android manifest) so the tilt
  axis stays predictable.
- The `android/` folder is intentionally **not** committed — Capacitor
  regenerates it from `www/` + `capacitor.config.json`. Edit the game in
  `www/index.html`; everything else is derived.
- This is a **debug** APK: fine for playing and sharing, but unsigned for the
  Play Store. Releasing there needs a signing key and a `release` build.
