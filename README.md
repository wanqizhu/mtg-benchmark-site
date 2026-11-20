# MTG LLM Benchmark

Public static site for the Puzzle and Draft Predictions benchmarks. Generated from the private `mtg-benchmark` harness; this repo is the GitHub Pages source.

## Local preview

```bash
python -m http.server 8000
```

Then open http://localhost:8000.

## Draft Predictions tab

Open `/#/draft-predictions` to compare Reality Fracture and Star Trek.
The overall table shows one Pearson correlation per prediction source and set.
Each score uses that source's rated main-set cards with a reported 17Lands
Premier Draft GIH win rate and at least 500 games in hand. The original
internet-enabled Reality Fracture runs are archived under Methodology.

The public Star Trek export includes per-card predictions and aggregate scores.
It links to 17Lands for observed card rates. A full local Star Trek export, when
available, supplies the observed rates and scatter plot as well.

To regenerate the data, see
`evaluations/historical-creators-2026-10-09/preview-inputs/README.md` in
`mtg-benchmark`. Use the `--public-summary` option to build the public Star Trek
export without per-card results.

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
