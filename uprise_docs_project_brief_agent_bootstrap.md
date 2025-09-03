# uprise_docs/PROJECT_BRIEF.md

## Uprise Mobile — Assistant Operating Brief

### Mission & Scope
- Get **uprise_mob** (React Native Android) reliably building/running on Windows.
- Next phase: **Firebase** integration (Analytics, Crashlytics, Messaging, Google Sign-In).
- Keep **webapp_ui** and **webapp_api** separate; **monorepo is abandoned**.

### Repositories
- `uprise_mob` — mobile app (current focus)
- `webapp_ui` — React web UI
- `webapp_api` — backend API
- `uprise_docs` — runbooks, ADRs, changelogs, prompts

### Platform & Tooling (Windows)
- **Shell:** PowerShell (no WSL/Bash for build steps)
- **JDK:** Java 11 (Temurin)
- **Node:** 20.x at `C:\tools\node-v20.19.0-win-x64` (Gradle `nodeExecutableAndArgs` points here)
- **React Native:** 0.66.x (Hermes enabled)
- **Android SDK:** `compileSdkVersion 30`, `targetSdkVersion 30`, `minSdkVersion 21`, `multiDexEnabled true`

### Android App IDs & Build Behavior
- **Release** `applicationId`: `com.app.uprise`
- **Debug** uses `applicationIdSuffix ".dev"` → `com.app.uprise.dev`
- **Resource overrides:** Use `app/src/debug/res/values/strings.xml` for debug-only names (e.g., `app_name`), not `resValue` to avoid merge duplicates.
- **Install tips:** Keep `.dev` suffix to install alongside any existing `com.app.uprise`. Otherwise `adb uninstall com.app.uprise` first.

### Firebase (Required Layout)
Place **two** configs:
- `app/src/debug/google-services.json` → must contain **package_name** `com.app.uprise.dev`
- `app/src/release/google-services.json` → must contain **package_name** `com.app.uprise`
Other notes:
- Enable `apply plugin: 'com.google.gms.google-services'` in `app/build.gradle` (already present).
- Add the **debug keystore** SHA‑1 from `:app` (path shows `D:\uprise_mob\android\app\debug.keystore`) to the **debug** app in Firebase.
- Optional: Add SHA‑256 as well.

### Locked Architectural Decisions
- **No symlinks** (caused infinite nesting previously).
- Prefer **vendoring** and **Gradle subprojects** for native libs.
- **ScalableVideoView** vendored as `android/external/scalableviewer/` and wired in `settings.gradle` + `app/build.gradle`.
- **react-native-track-player** currently excluded (pending ExoPlayer alignment) — don’t re‑enable without a dependency plan.

### Current Status Snapshot
- Builds with Java 11; debug duplicate `app_name` fixed by using `src/debug/res/values/strings.xml`.
- ScalableVideoView ✅ integrated locally.
- APK installs as `.dev` alongside release app (no uninstall needed).
- **Blocking for Firebase:** must place both `google-services.json` files with matching package names.

### Day‑to‑Day Commands (PowerShell)
```powershell
cd D:\uprise_mob\android
.\n
# Clean & build
.\n
# Install debug APK (side-by-side via .dev suffix)
adb install -r app\build\outputs\apk\debug\app-debug.apk

# If you ever switch back to single ID and get signature mismatch
adb uninstall com.app.uprise
```

### Firebase Setup Checklist
- [ ] Register **Android app (debug)** `com.app.uprise.dev` in your Firebase project
- [ ] Upload SHA‑1 from `:app` debug keystore (`signingReport`) to this debug app entry
- [ ] Download its `google-services.json` → place at `app/src/debug/`
- [ ] Register **Android app (release)** `com.app.uprise`
- [ ] (Optional) Upload SHA‑1 for your release keystore once you have it
- [ ] Download its `google-services.json` → place at `app/src/release/`
- [ ] Confirm `apply plugin: 'com.google.gms.google-services'` remains at bottom of `app/build.gradle`
- [ ] `.\n
### Documentation Workflow
Update `uprise_docs` with small, frequent notes:
- `RUNBOOK_ANDROID.md` — reproducible build & env steps
- `CHANGELOG.md` — what changed & why
- `ADR/` — decisions (e.g., `0001-no-symlinks.md`)
- `BUILD_LOG.md` — relevant excerpts that speed up future debugging

---

# uprise_docs/prompts/AGENT_BOOTSTRAP.md

```
You are collaborating on the Uprise Mobile Android app (React Native 0.66.x) on Windows using PowerShell.

Constraints & decisions:
- JDK 11 (Temurin); Node at C:\tools\node-v20.19.0-win-x64 (use Gradle project.ext.react nodeExecutableAndArgs).
- No symlinks. Vendor native libs as Gradle subprojects.
- App IDs: release = com.app.uprise, debug suffix .dev → com.app.uprise.dev.
- Firebase requires two google-services.json files: app/src/release and app/src/debug with matching package names.
- Android SDK: compileSdk/targetSdk 30, minSdk 21, multidex on.
- ScalableVideoView is vendored at android/external/scalableviewer/ and already wired up.
- react-native-track-player is temporarily excluded; do not re-enable without a clear ExoPlayer pinning plan.

Deliverables:
1) A short plan first. 2) Exact PowerShell commands. 3) Minimal diffs with why they’re needed. 4) Update notes for uprise_docs (runbook/changelog/ADRs).

Do NOT use Bash/WSL commands. Do NOT introduce symlinks. Prefer reproducible Gradle/PowerShell flows.
```

