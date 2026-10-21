# Jenga Football V3.0 Automation-Ready — Build and Validation Status

## Included
- Android client source with Auto AI backend connection, league pool, fixture list, provider health checks, and match analysis results.
- Node.js backend for API-Sports fixtures/context, Tavily search discovery, and four-provider three-round forecasting/debate.
- Render deployment blueprint and GitHub Actions Android build workflow.
- Blank `.env.example`; no API secrets are included.

## Checks completed in the preparation environment
- `node --check backend/server.js` passed.
- Inline JavaScript in `www/index.html` passed Node syntax checking.
- Root `index.html` and `www/index.html` are identical.
- Backend `/health` returned HTTP 200.
- In production mode, `/api/status` without the access token returned HTTP 401; with the token it returned HTTP 200.
- APK archive integrity and JAR/v1 signature verification passed; `resources.arsc` is stored uncompressed.

## Not yet validated
- Live OpenAI, Gemini, Anthropic, DeepSeek, API-Sports, or Tavily credentials/connections.
- Actual server deployment or device-side installation/launch.
- Full native rebuild from this updated source using Android SDK tools.
- End-to-end match forecast with real credentials and fixture data.

## Important forecasting limitation
The automated backend intentionally marks matches NOT QUALIFIED until its evidence gates are actually met. Dedicated validated xG/npxG ingestion, opponent-strength adjustment, verified player ratings/lineups, historical backtesting and market-odds value analysis are not implemented in this starter. AI agreement is not a calibrated accuracy guarantee.

## API cost warning
One fixture can trigger up to 12 LLM calls (four providers across three rounds), plus sports-data and search calls. Configure spend limits where available and test one fixture first. API access may be separately billed from chat subscriptions.
