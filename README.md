# MTG Puzzle Bench

Public static site for the MTG Puzzle Bench leaderboard. Generated from the private `mtg-benchmark` harness; this repo is the GitHub Pages source.

## Local preview

```bash
python -m http.server 8000
```

Then open http://localhost:8000.

## Update from eval results

From the `mtg-benchmark` repo:

```bash
bench site --output-dir ../mtg-benchmark-site
```

That rewrites `data/` and `assets/`, and refreshes the frontend files. Incremental evals mostly add small JSON files under `data/runs/<run>/<model>/`.

To keep scores for every problem in a range but only publish a few puzzle pages:

```bash
bench site --output-dir ../mtg-benchmark-site --problems 1-39 --detail-problems 1-20
```

## GitHub Pages

In the GitHub repo: Settings → Pages → Deploy from a branch → `main` / `/ (root)`.
`.nojekyll` is included so `data/` is served as-is.
