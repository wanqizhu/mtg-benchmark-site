# MTG Puzzle Bench

Public static site for the MTG Puzzle Bench leaderboard. Generated from the private `mtg-benchmark` harness; this repo is the GitHub Pages source.

## Local preview

```bash
python -m http.server 8000
```

Then open http://localhost:8000.

## Draft Predictions tab

Open `/#/draft-predictions` for the FRA prediction comparison. It contains six
original AI forecasts, five sandbox AI forecasts, and four creator models
calibrated using historical data. Model names carry these markers throughout
the scores, chart, card details, prediction table, and CSV:

- `*`: With internet, so it could see some community tierlists before set release.
- `†`: Without internet; just cards, rules, and historical data.

The sandbox runs were made after release while withholding current-set results
and community reviews. The original model methodology is retained, with its prompt and submission links.
A separate sandbox methodology section links the transcript PR for documentation. Original forecasts and creator fits are preserved. Internet-model labels are blue; sandbox-model labels use a purple dagger (†).
The opening score table and scatter plot use the same 266 cards; the expandable
table contains the complete 295-card catalog. Source names use distinct colors
for AI models and creators. The plot shows predicted versus observed GIH;
the x axis is predicted GIH and the y axis is observed GIH. Hover gives rates
and errors, and clicking opens a Scryfall image with prediction stats. The card
table defaults to observed GIH descending. Methodology
includes the full shared prediction prompt and a current-set creator source
table with links to both LR reviews. Card details link each published grade to
its original rating source. Creator collection, fitting and
coefficients are grouped in one expandable section. Draftsim source timing is
provisional.

Historical 17Lands source rows offer a readable Tier list link and a separately
labeled Snapshot JSON link for the exact dated data used in fitting. Casual
Spike's details identify the community reviewer as Reddit's u/Casual_Spike.

The current outcome is the October 14, 2026 at 12:56:41 UTC PremierDraft ALL_TIME
GIH pull. All 295 card rows use current outcomes; headline scores retain the
same 266-card comparison pool. The methodology date is read from the outcome
metadata. The AI
forecasts are not recalibrated against FRA outcomes. The creator mappings use
historical fitting, with retrospective policy choices disclosed in the page.

To add or restore the frozen sandbox forecasts to an existing export, run from
the benchmark repository:

```sh
python evaluations/historical-creators-2026-10-09/sandbox_predictions.py \
  --input ../mtg-benchmark-site/data/draft-predictions.json \
  --output ../mtg-benchmark-site/data/draft-predictions.json
```

The complete exporter also includes these forecasts automatically. Each source
retains its original branch commit, prediction-file hash, and transcript hash.

Refresh the comparison from `mtg-benchmark`:

```sh
python evaluations/historical-creators-2026-10-09/refresh_benchmark_outcomes.py \
  --input ../mtg-benchmark-site/data/draft-predictions.json \
  --output ../mtg-benchmark-site/data/draft-predictions.json --fetch
```

This pulls only new outcomes and recomputes the evaluation with fixed predictions
and creator fits. It also saves the current normalized outcome snapshot in the
analysis repo's `inputs/fra_outcomes.json`. To reproduce that committed snapshot,
replace `--fetch` with `--snapshot
evaluations/historical-creators-2026-10-09/inputs/fra_outcomes.json`.

To rebuild the complete export from retained local analysis artifacts:

```sh
python evaluations/historical-creators-2026-10-09/export_benchmark_tab.py \
  --model-data evaluations/fra-week-one-2026-10-07/results/dashboard_data.json \
  --output ../mtg-benchmark-site/data/draft-predictions.json
```

This applies the committed current outcomes to analyzed card predictions and
model metadata without live response
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
