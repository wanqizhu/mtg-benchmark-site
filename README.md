# MTG Eval Viewer

Public static site for the MTG puzzle eval leaderboard. Generated from the private `mtg-ai` harness; this repo is the GitHub Pages source.

## Local preview

```bash
python -m http.server 8000
```

Then open http://localhost:8000.

## Update from eval results

From the `mtg-ai` repo:

```bash
bench site --output-dir ../mtg-eval
```

That rewrites `data/` and `assets/`, and refreshes the frontend files. Incremental evals mostly add small JSON files under `data/runs/<run>/<model>/`.

To keep scores for every problem but only publish a few puzzle pages:

```bash
bench site --output-dir ../mtg-eval --detail-problems 001,002,003
```

## GitHub Pages

In the GitHub repo: Settings → Pages → Deploy from a branch → `main` / `/ (root)`.
`.nojekyll` is included so `data/` is served as-is.
