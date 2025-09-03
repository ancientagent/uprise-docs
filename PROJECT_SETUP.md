# 🛠 UPRISE Development Project (Project Setup)

## 🎯 Project Goal
We are developing **Uprise Mobile (`uprise_mob`)**, a React Native app (0.66.x) targeting **Android first**, as part of the larger **UPRISE platform**. The immediate goal is to achieve a **stable build + run loop** on Android, with Firebase integrated, and keep documentation + changelogs updated as we progress.

---

## 👥 Team Mode
- This is a **collaborative team project**.
- ChatGPT acts as **technical co-pilot** for debugging, documentation, and system planning.
- **Agents in play:**
  - **Cursor + Claude Code (100cc subagents)** → local repo editing and code refactors.
  - **Gemini 2.5** → Firebase Console tasks.
  - **Google Jules 2** → additional backend/cloud assistance.
  - **ChatGPT (GPT-5)** → coordination, debugging, documentation, and planning.
- Human + AI = one dev team.

---

## 🔧 Technical Baseline
- **OS/Shell**: Windows 11, PowerShell preferred.
- **JDK**: Eclipse Adoptium 11.0.28 (Temurin).
- **Node.js**: Portable 20.19.0 at `C:\tools\node-v20.19.0-win-x64`.
- **Gradle**: 7.0.2 (bundled).
- **React Native**: 0.66.x (Hermes enabled).
- **Firebase**: Integrated (Analytics, Crashlytics, Messaging, Core). Debug/release `google-services.json` configured. ADR-0002 finalized.
- **App IDs**:
  - Release: `com.app.uprise`
  - Debug: `com.app.uprise.dev` (with `applicationIdSuffix ".dev"`)
- **Android SDK**: `C:\Users\<username>\AppData\Local\Android\Sdk`.
- **ADB**: `platform-tools` on PATH.
- **Symlinks**: 🚫 Not allowed. Use vendored Gradle subprojects instead.

---

## 📂 Repositories
- **`uprise_mob`** → React Native mobile (primary active repo).
- **`webapp_ui`** → React web app (rewrite of old Angular version). Currently not developed in parallel with mobile.
- **`webapp_api`** → Firebase backend.
- **`uprise_docs`** → Documentation repo (source of truth).

⚠️ **Note:**
The webapp is a **rewrite from Angular → React**. It was not developed alongside the mobile build, so **when we’re ready to resume webapp work (or at any time)** we should conduct a **full archeological investigation**:
- Audit the Angular → React rewrite.
- Compare webapp vs mobile feature parity.
- Document **gaps + inconsistencies** between mobile and webapp.
- Plan unification + integration path with backend (`webapp_api`).

---

## 📂 Core Documents to Seed Project Memory
- `RUNBOOK_ANDROID.md` → Step-by-step build/run/debug guide.
- `BUILD_LOG.md` → Rolling log of build/test runs.
- `CHANGELOG.md` → Dev progress across versions.
- `ADR-0002` → Firebase integration decision.
- `# UPRISE early Platform Overview.txt` → Strategic vision & context.
- `home scene distinctions and more.md` → Product framing & UX concepts.

---

## 📌 Workflow Rules
- Always suggest PowerShell commands (never Bash).
- Keep changes **reproducible + documented** (update RUNBOOK/CHANGELOG/ADRs).
- If a build fails, analyze logs step by step → propose fixes, not just guesses.
- Assume **multi-agent teamwork**: Cursor/Claude for code, Gemini for Firebase, Jules for backend/cloud, ChatGPT for coordination.
- No committing secrets (API keys, JSON configs). Rotate + purge if any leak.

---

## 🤖 Models/Tools Available
- **ChatGPT (GPT-5)** → debugging, planning, docs, strategy.
- **Cursor + Claude Code (100cc subagents)** → repo editing, refactor, code completion.
- **Gemini 2.5** → Firebase Console tasks.
- **Google Jules 2** → backend/cloud alignment.
- **Image Gen** → visual assets (diagrams, app flows, promo imagery).
- **Python sandbox** → data analysis + docs (PDF, RTF, charts).
- **File search / retrieval** → instant reference of uploaded docs (RUNBOOK, ADRs, etc).

---

## ✅ Immediate Next Steps
1. Ensure stable **debug build + Metro bundler** runs cleanly on emulator/device.
2. Confirm **app launches correctly** (`com.app.uprise.dev`).
3. Verify **Firebase events (Analytics, Crashlytics)** reporting.
4. Keep all fixes + discoveries synced into `RUNBOOK_ANDROID.md` and `CHANGELOG.md`.
5. Begin planning **webapp archeological investigation** when mobile build loop is stable.

