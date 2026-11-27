WORDX ANDROID STARTER — READ FIRST

This package preserves the approved WORDX HTML and wires it to Vite + Capacitor 8, Firebase JS SDK, and the Capacitor Firebase Authentication plugin.

IMPORTANT
- Android package ID: com.wordx.app
- Firebase project: wordx-x
- google-services.json is included for the Android app.
- Do not upload a release keystore or signing passwords to GitHub.
- This is the prepared source project, not a built APK. The Android platform must be generated and tested before release.

WINDOWS POWERSHELL — FIRST BUILD
1. Extract this ZIP into a folder such as C:\Users\ELCOT\Downloads\WORDX.
2. Open PowerShell in that folder.
3. Run:
   npm.cmd install
   npm.cmd run build
   npx.cmd cap add android
   npx.cmd capacitor-assets generate --android
4. Copy google-services.json into the generated android\app\ folder.
5. The asset generator creates native Android launcher and splash resources from the supplied WORDX logo.
6. Follow the Android Firebase setup checklist below before building. Do not skip it.

ANDROID FIREBASE SETUP CHECKLIST
- Confirm Firebase Authentication has Google provider enabled.
- Confirm Firebase project wordx-x has Android app com.wordx.app.
- Confirm SHA-1 is registered: BA:28:79:91:B5:E7:69:AE:04:01:2F:5E:9B:14:C1:E7:EA:57:AE:8A
- Confirm the downloaded google-services.json is the latest one for that SHA-1.
- Apply the Google Services Gradle plugin and Capawesome Google provider Gradle variables exactly as described in the current plugin Google setup guide:
  https://github.com/capawesome-team/capacitor-firebase/blob/main/packages/authentication/docs/setup-google.md
- Then run:
   npx.cmd cap sync android
   cd android
   .\gradlew.bat assembleDebug

NATIVE AUTH DESIGN
On Android, the app uses the native Google Credential Manager flow. The returned Google ID token is converted to a Firebase JS credential so the existing Firestore code continues to use the same authenticated user. On desktop/web preview, the original Firebase popup/redirect path remains available.

The plugin's native-to-JS bridge is required because native authentication alone does not automatically authenticate the Firebase JS SDK. See:
https://github.com/capawesome-team/capacitor-firebase/blob/main/packages/authentication/docs/firebase-js-sdk.md

LOGO
- public/assets/wordx-full-logo.png: full splash/brand artwork.
- public/assets/wordx-icon.png: square icon artwork for Android launcher icon generation.

NEXT
After first local Android generation and validation, commit the generated android/ folder and the source files to the public GitHub repository. Do not commit keystores or signing credentials.
