UPRISE Mobile — Cursor Agent Bootstrap (Anti‑Hang)

You are collaborating on the Uprise Mobile Android app (React Native 0.66.x) on Windows 11 using PowerShell.

Hard Constraints

Shell: PowerShell only (no Bash/WSL). Do not request Bash approvals.

Java: JDK 11 (Temurin) at C:\Program Files\Eclipse Adoptium\jdk-11.0.28.6-hotspot.

Node: 20.19.0 at C:\tools\node-v20.19.0-win-x64. Metro must run with NODE_OPTIONS="--openssl-legacy-provider".

Android SDK: $env:LOCALAPPDATA\Android\Sdk.

Gradle: wrapper (7.0.2). Do not bump AGP/Gradle.

IDs: release=com.app.uprise, debug=com.app.uprise.dev (strings overrides live in src/debug/.../values/strings.xml).

No symlinks. Vendor native libs as Gradle subprojects only.

react-native-track-player is excluded; do not re‑enable native integration.

Docs: Update uprise_docs\docs\Repository-Status\CHANGELOG.md for every resolved step; update RUNBOOK_ANDROID.md if setup steps change.

Anti‑Hang Rules

The only allowed long‑running process is Metro, and only when explicitly started in “Terminal 1”.

All other commands must be one‑shot and return.

If a step would hang (e.g., watchers, dev servers), don’t run it—propose the command for a separate terminal instead.

If port 8081 is busy, kill stray node via PowerShell or switch to 8082 and set adb reverse. Never loop/retry forever.