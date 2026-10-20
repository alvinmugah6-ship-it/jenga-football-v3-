# Build and install Jenga Football V3.0 on an Android phone

This is the phone-only route. The source is prepared, but the actual APK must be compiled with Android SDK/Gradle. Those build tools are not installed in the working environment, so the included free GitHub Actions workflow builds an installable **debug APK** in the cloud.

## What you'll need

- Your Android phone and Chrome.
- A free GitHub account.
- The extracted project files from this ZIP.
- Internet access during the cloud build and APK download.

## 1. Create a GitHub repository

1. Open https://github.com in Chrome and sign in (create a free account if needed).
2. Tap **+ → New repository**.
3. Name it `jenga-football-v30-ai-council`.
4. Choose **Private** if you prefer. Leave “Add a README” unchecked so the repository starts empty.
5. Create the repository.

## 2. Extract the project ZIP on your phone

1. Download `Jenga_Football_V3_0_APK_Project.zip` and open it in Files.
2. Extract it.
3. Check that the extracted folder contains `www/index.html`, `package.json`, `capacitor.config.json`, and `.github/workflows/build-apk.yml`.

## 3. Upload the project files to GitHub

1. Open your new repository and tap **Add file → Upload files**.
2. Select the extracted project contents—not only the ZIP.
3. Keep the folder structure. `www` must be at the repository root; the workflow must live at `.github/workflows/build-apk.yml`.
4. Some Android file pickers hide dot-folders such as `.github`. If the workflow folder is missing, use **Add file → Create new file** on GitHub and create `.github/workflows/build-apk.yml`, then paste the workflow from the extracted file. Do not continue if the workflow is not present.
5. Commit the uploaded files to `main`.

If the mobile website refuses to upload folders with their structure, stop and tell ChatGPT what screen you see; don't flatten the files or upload only the ZIP.

## 4. Build the APK in the cloud

1. In the repository, open the **Actions** tab and enable workflows if GitHub asks.
2. Select **Build Jenga Football V3.0 AI Council APK**.
3. Tap **Run workflow → Run workflow**. A push to `main` should also start the build automatically.
4. Open the run and wait for the green check mark.
5. In the run's **Artifacts** section, download `Jenga-Football-V3.0-AI-Council-debug-APK`.
6. Open the downloaded ZIP and extract `app-debug.apk`.

## 5. Install and test

1. Tap `app-debug.apk` from Downloads.
2. Android may require you to allow installation from that source; only allow installation for the APK you built from this project.
3. Open **Jenga Football V3.0** and add a clearly fictional test fixture first.
4. Test the fixture desk, Pass A, independent Pass B, AI Council, Pass C, checklist, prediction report, Over/Under 2.5 audit, BTTS audit and strongest-picks funnel.
5. Use **Backup / help → Export all data (JSON)** regularly. Uninstalling or clearing app data may erase locally stored analyses.

## What the AI Council actually does in this build

It prepares separate prompts for ChatGPT, Gemini, Claude and DeepSeek and imports their JSON responses for comparison. This first zero-budget version does not call their APIs automatically. Never put API keys into the app source or APK. Automatic multi-provider execution will need a secure backend and provider access.

This debug APK is for testing and isn't a Play Store-signed release. The model itself has provisional assumptions and no validated historic backtest bundled into this app. Treat probabilities as estimates, not guarantees.
