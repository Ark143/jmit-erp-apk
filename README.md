# JMIT ERP — Android APK

Offline Android wrapper for the JMIT ERP web app (vanilla-TS SPA). The compiled
SPA is bundled in `app/src/main/assets/` and served inside a WebView over a
virtual https origin (`jmit-erp.local`) so ES2020 modules load and
localStorage (`jmit_erp_state`) persists on the phone. 100% offline, no backend.

- Package: `com.jmit.erp` — label **JMIT ERP** — minSdk 26, target 34
- Login: same seeded users as the web app (`admin` / `jmit2026`)
- Zero dependencies, ~90 KB release APK

## Build

Requires JDK 17, Android SDK (build-tools 34), Gradle 8.x. Create
`local.properties` with `sdk.dir=<path-to-Android-Sdk>`, then:

```bash
gradle assembleRelease
# -> app/build/outputs/apk/release/app-release.apk (signed)
```

## Update the bundled web app

In the web repo (`jmit-erp`):

```bash
npm run build
```

then re-copy `index.html`, `favicon.svg`, `css/styles.css`, `dist/` (drop
`*.map`) into `app/src/main/assets/`, bump `versionCode`/`versionName` in
`app/build.gradle`, rebuild. Same keystore (`erp-release.keystore`, alias
`erp`) ⇒ installs as an update over the previous version, phone data preserved.
