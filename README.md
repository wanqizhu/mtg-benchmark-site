# MTG Puzzle Bench

Public static site for the MTG Puzzle Bench leaderboard. Generated from the private `mtg-benchmark` harness; this repo is the GitHub Pages source.

## Local preview

```bash
python -m http.server 8000
```

Then open http://localhost:8000.

## Draft Predictions tab

Open `/#/draft-predictions` for the FRA prediction comparison. It contains six
original AI forecasts and four creator models calibrated using historical data.
The opening score table and scatter plot use the same 266 cards; the expandable
table contains the complete 295-card catalog. Source names use distinct colors
for AI models and creators. The plot shows predicted versus observed GIH;
the x axis is predicted GIH and the y axis is observed GIH. Hover gives rates
and errors, and clicking opens a Scryfall image with prediction stats. The card
table defaults to observed GIH descending. Methodology
includes the full shared prediction prompt. Creator collection, fitting and
coefficients are grouped in one expandable section. Draftsim source timing is
provisional.

The outcome is the frozen October 7, 2026 PremierDraft GIH snapshot. The AI
forecasts are not recalibrated against FRA outcomes. The creator mappings use
historical fitting, with retrospective policy choices disclosed in the page.

Refresh the comparison from the analysis branch of `mtg-benchmark`:

```sh
python evaluations/historical-creators-2026-10-09/export_benchmark_tab.py \
  --model-data evaluations/fra-week-one-2026-10-07/results/dashboard_data.json \
  --output ../mtg-benchmark-site/data/draft-predictions.json
```

This exports analyzed card predictions and model metadata without live response
envelopes or outcome refitting. The benchmark's static generator includes the
tab assets and preserves this data file when puzzle results are refreshed.

## Update from eval results

From the `mtg-benchmark` repo:

```bash
bench site --output-dir ../mtg-benchmark-site
```

That publishes the **grep-rules** run by default, rewrites `data/` and `assets/`, and refreshes the frontend. Visible attempt pages include sanitized rollout transcripts. Incremental evals mostly add JSON files under `data/runs/<run>/<model>/`.

To keep scores for every problem in a range but only publish a few puzzle pages:

```bash
bench site --output-dir ../mtg-benchmark-site --problems 1-39 --detail-problems 1-20
```

## GitHub Pages

In the GitHub repo: Settings → Pages → Deploy from a branch → `main` / `/ (root)`.
`.nojekyll` is included so `data/` is served as-is.
