# Jenga Football Super-Model V3.0 — AI Council Build

A mobile-first Android/web app project for the user's daily football V3.0 workflow. The goal is disciplined, reviewable analysis, not guaranteed predictions.

## V3.0 workflow included

- Official fixture verification fields, date, kick-off, senior/youth and cup/league status.
- Opponent-adjusted recent-five inputs for both teams, xG/xGA and optional npxG.
- Context inputs: standings/PPG, verified team news, goalkeeper and centre-backs, player ratings, tactics, motivation, rest and rotation.
- Pass A → independent Pass B → Pass C debate; calculations use an explicit Poisson expected-goals model.
- Model-implied Home/Draw/Away probabilities, Over/Under 2.5 probabilities, BTTS Yes/No probabilities and top three correct scores.
- Separate Over/Under 2.5 and BTTS audit notes, uncertainty fields, a step-by-step checklist, exclusions log and strongest-picks funnel.
- Strongest 10 display that does not force ten selections when fewer fixtures qualify.
- **Four-AI Council:** ChatGPT (lead analyst), Gemini (independent challenger), Claude (tactical/squad analyst), DeepSeek (quantitative skeptic). Each gets an independently generated prompt using the same entered match packet; responses are pasted back, parsed, stored and compared. A Round 2 cross-examination prompt then puts the reports into a debate. At least 3 valid AI reports plus a saved cross-examination are required to save Pass C and qualify a pick.
- Local browser storage, JSON backup/restore and CSV export.

## Critical AI connection note

The current 0.4 build uses a **manual copy/paste bridge** to each provider's web app. This is intentional for the zero-budget phone-first version. It does not automatically invoke four AI APIs, and it cannot call the model powering the current ChatGPT conversation from inside the APK. API access requires provider credentials and a secure backend; never put secret API keys inside an APK or client-side JavaScript. Use each provider's strongest reasoning/search model available to your account, record the model name in its JSON response, and do not assume every free account has identical capabilities.

Provider entry points:
- ChatGPT: https://chatgpt.com/
- Gemini: https://gemini.google.com/
- Claude: https://claude.ai/
- DeepSeek: https://chat.deepseek.com/

## Data and model limitations

- This build does **not** automatically fetch current fixtures, league tables, standings, xG/xGA, lineups, injuries, ratings or suspensions. It provides research shortcuts and evidence fields; verify facts manually and record source URLs and dates.
- The home-advantage +0.20-goal prior, 0.55/0.45 xG/xGA blend and opponent-strength normalization are provisional starting assumptions, not validated backtest results.
- AI consensus is an equal-weight comparison of the forecasts returned by the chosen models. It is not a historically calibrated meta-model; AI systems can share blind spots or repeat bad source claims.
- Probabilities are model estimates and not promises, bookmaker odds or instructions to bet. No selection is guaranteed.
- Match notes and AI responses are stored locally in the app's browser storage. Export backups. Clearing app data or uninstalling can delete them. Avoid entering account credentials or highly sensitive information.

## Building the Android APK

The project includes `.github/workflows/build-apk.yml`. It validates app syntax, runs the model and AI Council smoke tests, then builds an **installable debug APK** in GitHub Actions on a GitHub-hosted Android build environment. This local workspace does not have the Android SDK/Gradle installation required to compile the APK directly.

See `PHONE_BUILD_GUIDE.md` for the phone-only route. The debug APK is for testing and is not a signed Play Store release.

## Files

- `www/index.html` — standalone web app and model logic.
- `capacitor.config.json` — Android app identity.
- `package.json` — Capacitor dependencies.
- `.github/workflows/build-apk.yml` — cloud APK build workflow.
- `PHONE_BUILD_GUIDE.md` — Android-phone upload, build and install steps.
- `AI_COUNCIL_GUIDE.md` — repeatable four-AI analysis/debate procedure.
