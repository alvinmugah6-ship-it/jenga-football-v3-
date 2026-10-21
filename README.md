# Jenga Football V3.0 — automation-ready client + backend

This project retains the existing manual V3.0 research workflow and adds an **Auto AI** tab. The tab calls the separate server-side backend for official league/fixture data, provider connection tests, and a four-provider / three-round analysis workflow.

## What is included

- `index.html` and `www/index.html`: the app page, including the existing research/council/report workflow and new Auto AI tab.
- `backend/server.js`: Node 20+ server for API-Sports football data, Tavily source discovery, and OpenAI/Gemini/Anthropic/DeepSeek calls.
- `render.yaml`: deployment blueprint for Render.
- `.github/workflows/build-apk.yml`: GitHub Actions workflow to compile a debug APK.
- `capacitor.config.json`, `package.json`: Android wrapper configuration.
- `backend/.env.example`: required server secrets and model settings (blank credentials only).

## Critical: the Auto AI tab needs a deployed backend

The APK package ID is `com.jenga.footballv3a` and its launcher label is `Jenga Football Auto`, so it is designed to install alongside the older `Jenga Football V3.0` app without deleting its local browser data. The APK must not contain AI provider secrets. First deploy `backend` as a web service, set its environment variables in the host's private secret panel, and then enter the service's HTTPS URL and the same `JENGA_ACCESS_TOKEN` into the Auto AI tab in the app.

Suggested hosting route: import this repository into Render using `render.yaml`. When the blueprint asks for secret values, set **a unique, long JENGA_ACCESS_TOKEN** and provide API keys you have obtained directly from the providers. Never paste provider keys into ChatGPT, the app's HTML, or a public GitHub repository. The `/health` endpoint is public for the hosting health check, while other API endpoints require the token in production.

Required server secrets:
- `JENGA_ACCESS_TOKEN`
- `OPENAI_API_KEY`
- `GEMINI_API_KEY`
- `ANTHROPIC_API_KEY`
- `DEEPSEEK_API_KEY`
- `APISPORTS_KEY`
- `TAVILY_API_KEY`

API usage may be charged by the providers. A single fixture can invoke four AI models up to three times each (up to 12 analysis calls), in addition to football-data and web-research requests. Test with one fixture first and check your provider usage dashboard. Provider subscriptions for chat websites do not automatically include API credit.

## Model defaults

This build requests strong current API model settings by default: OpenAI `gpt-5.6-sol` with `max` reasoning and `pro` mode; Gemini `gemini-3.1-pro-preview` with high thinking; Anthropic `claude-fable-5-1` with `max` effort; and DeepSeek `deepseek-v4-pro` with `max` effort. Provider access and parameter availability can vary by account. The **Test all 6 connections** action must confirm actual access. A failed model remains visibly failed; it is not silently replaced.

## Qualification rules and limitations

- The server returns `NOT QUALIFIED` unless all four providers complete the required three rounds and every coded evidence gate passes.
- Current search results are source leads, not proof of an injury, lineup, player rating, or press-conference statement.
- This implementation still does **not** contain a validated opponent-strength model, dedicated verified xG/xGA/npxG ingestion, verified position/player ratings and depth feed, historical backtest, or market-odds value model. Those gaps are explicit hard gates, so results must not be treated as fully qualified while these feeds are absent.
- The fixed Poisson baseline is uncalibrated and cannot qualify a match. Four-model consensus is an untrained mean, not a validated ensemble.
- Job state is in memory. A backend restart can lose an in-progress job; run one fixture at a time.

## Build the APK

Push these files to a GitHub repository's `main` branch. GitHub Actions will build an installable **debug APK** and attach it as an artifact to the workflow run. Debug APKs are for testing, not signed Play Store releases. Depending on the signing key used for a build, it may not install as an in-place update over an earlier APK built by a different runner/key; export any in-app data first.

## Local checks

```bash
node --check backend/server.js
node --check /path/to/extracted-client-script.js
```

The backend JavaScript syntax and local health/auth routes were checked in this environment. The APK delivered separately is a test package derived from the previously successful GitHub APK and was repacked to include the Auto AI view; it was not compiled from scratch with Android SDK tools or installed on a physical Android device in this environment. Live provider calls have not been tested because no API credentials are configured.
