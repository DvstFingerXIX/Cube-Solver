# Cube Solver: gabay para gawing Android at iOS app

Ang `www/` ay ang mismong app. Gumagamit ng Capacitor para ilagay ito sa loob ng totoong Android at iOS app.
Kailangan mo ang Node.js (https://nodejs.org). Palitan muna ang `appId` sa `capacitor.config.json` ng sarili mong ID, halimbawa `com.pangalan.cubesolver`.

## Mga hakbang
1. `npm install @capacitor/core @capacitor/cli @capacitor/android @capacitor/ios`
2. `npx cap add android` at/o `npx cap add ios`
3. **Camera permission** (kailangan para sa live scan):
   - Android: sa `android/app/src/main/AndroidManifest.xml`, idagdag sa loob ng `<manifest>`:
     `<uses-permission android:name="android.permission.CAMERA" />`
   - iOS: sa `ios/App/App/Info.plist`, idagdag:
     `<key>NSCameraUsageDescription</key><string>Gagamitin ang camera para i-scan ang kulay ng Rubik's cube.</string>`
4. `npx cap sync`
5. Android: `npx cap open android`, tapos Build > Generate Signed Bundle/APK sa Android Studio.
6. iOS: `npx cap open ios` (Mac lang), piliin ang Team mo sa Signing, tapos Run o Archive sa Xcode.
7. Icon at splash: `npm i -D @capacitor/assets`, ilagay ang `icon-512.png` (mas mabuting 1024x1024) sa `assets/icon.png`, tapos `npx capacitor-assets generate`.

## Kailangan para ma-publish
- Google Play: Google Play Developer account (isang beses na bayad, mga $25).
- App Store: Apple Developer Program (mga $99 kada taon) at Mac na may Xcode.
- Para sa testing lang, pwedeng i-install ang debug APK sa Android nang walang bayad.

## Mga tala
- Nakaayos ang `www/` bilang installable na web app din (`manifest.webmanifest` at `sw.js` para sa offline). Pwede mo itong i-host sa kahit anong https na hosting at i-"Add to Home Screen".
- Hindi ko pa nasubukan ang pag-build, ang camera sa loob ng app, o ang itsura sa totoong phone. Subukan muna sa device bago i-publish.

## Pinakamadaling paraan para sa Android APK (walang ini-install sa computer)
1. Gumawa ng libreng account sa https://github.com at gumawa ng bagong repository (branch na `main`).
2. I-upload ang **lahat ng laman** ng zip na ito, kasama ang nakatagong folder na `.github`. Kung drag-and-drop ang gamit mo, siguraduhing kasama ito.
3. Pumunta sa tab na **Actions** > **Build Android APK** > **Run workflow**.
4. Pagkatapos ng ilang minuto, buksan ang natapos na run at i-download ang **CubeSolver-debug-apk** sa ilalim ng Artifacts. I-unzip ito para makuha ang `app-debug.apk`.
5. Ilipat sa phone, buksan, at payagan ang "Install unknown apps" kapag tinanong.

Ang debug APK ay para sa personal na paggamit at pagsubok. Para sa Google Play, kailangan ng signed release build (AAB), at hindi ito saklaw ng workflow na ito.
