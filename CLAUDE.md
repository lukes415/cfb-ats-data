# cfb-ats-data

Data pipeline and ML modeling project for predicting college football ATS (against the spread) outcomes. Feeds trained model artifacts into `cfb-ats-api`.

## Structure

- `data/notebooks/hate_watch_ATS_data_file.ipynb` — primary notebook; ingests CFBD data, engineers features, trains and evaluates models
- `models/latest/cfb_ats_model_latest_colab.ipynb` — Colab version of the modeling notebook
- `src/cfbdata/` — Python package stubs (currently empty); intended to extract notebook logic into importable modules for use by the API
- `data/features/` — engineered feature datasets (gitignored)
- `data/processed/` — cleaned/processed data (gitignored)

## Current status

All active work lives in the notebooks. The `src/cfbdata/` package files (`ingest_cfbd.py`, `features.py`, `model.py`, `utils.py`) are empty stubs — the goal is to eventually migrate notebook logic there so the API can import the featurizer and model directly.

Model performance: ~50% accuracy with random forest + encoded team IDs, roughly matching naive baselines. Feature engineering is the main lever to pull.

## Data source

College Football Data API (collegefootballdata.com). Same API key used in `cfb-ats-api`.

## Key features engineered so far

Conference flags, timezone deltas, coaching tenure deltas, pregame ELO. COVID year (2020) is a known wildcard in the dataset.

## Related projects

- `../cfb-ats-api` — consumes the trained model via `services/model_loader.py` and `featurizer.py` (stubs, not yet wired up)
