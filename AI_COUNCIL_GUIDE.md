# Jenga V3.0 — Four-AI Council operating procedure

## Round 1: independent forecasts

Run the four analysts separately against the same match packet. Do not show any first-round analyst another analyst's output before saving its own forecast.

1. **ChatGPT — lead analyst.** Build the main forecast and state the strongest counterargument.
2. **Gemini — independent challenger.** Produce a separate estimate; test the draw and alternate market case.
3. **Claude — tactical/squad analyst.** Focus on verified team news, goalkeeper/centre-back status, tactics, motivation, rotation and competition context.
4. **DeepSeek — quantitative skeptic.** Check expected goals, probability arithmetic, market consistency and downside scenarios.

Use the app's Copy prompt button, open the named provider, paste the prompt and submit. Use the strongest reasoning/search model actually available in your account; if it cannot browse, tell it to disclose this. Copy its full JSON response into the matching panel and choose Parse & save.

## Probability output contract

The app expects one JSON object with numeric `lambdaHome`, `lambdaAway`; `homeWin`, `draw`, `awayWin`; `over25`, `under25`; `bttsYes`, `bttsNo`; `topScores`; `evidence`; `risks`; `dataGaps`; `bestMarket`; and `verdict`. Probabilities should be decimals from 0 to 1. Percent-style values are accepted and normalized, but decimal form is preferred. If parsing fails, ask the AI to return exactly one valid JSON object without markdown or commentary.

Never accept invented citations. Evidence should name the claim, URL, source date and whether it is verified, estimated or unverified.

## Round 2: cross-examination

After at least three AI forecasts are saved, copy the Round 2 prompt and send it to ChatGPT (or another available model). It includes all saved forecasts and asks the referee to find unsupported claims, source conflicts, bad assumptions, and probability inconsistencies. Do not choose the majority view automatically.

Paste the cross-examination conclusion back into Jenga and save it. Then return to Pass C and separately record:

- the final expected goals and the 1/X/2 interpretation;
- the Over/Under 2.5 audit;
- the BTTS Yes/No audit;
- the top-score sanity check;
- unresolved uncertainty and evidence gaps;
- final verdict and what would change it.

At least three valid AI reports and a saved Round 2 debate record are required before Pass C can be saved. The fourth AI is recommended and can reveal disagreement, but 4/4 is not forced. This makes the process strict without pretending unanimity proves accuracy.
