# cfb-ats-data

Data pipeline and ML modeling project for predicting college football ATS (against the spread) outcomes. Feeds trained model artifacts into `cfb-ats-api`.

## Structure

- `data/notebooks/hate_watch_ATS_data_file.ipynb` — primary notebook; ingests CFBD data, engineers features, trains and evaluates models
- `models/latest/cfb_ats_model_latest_colab.ipynb` — Colab version of the modeling notebook
- `models/cfb_ats_model.joblib` — exported sklearn Pipeline (TargetEncoder + RandomForest), consumed directly by `cfb-ats-api`
- `models/feature_columns.json` — ordered feature list + human-readable top factors, read by `cfb-ats-api`'s `model_loader.py`
- `src/cfbdata/` — Python package stubs (currently empty); intended to extract notebook logic into importable modules for use by the API
- `data/features/` — engineered feature datasets (gitignored)
- `data/processed/` — cleaned/processed data (gitignored)

## Current status

All active work lives in the notebooks. The `src/cfbdata/` package files (`ingest_cfbd.py`, `features.py`, `model.py`, `utils.py`) are still empty stubs — the goal is to eventually migrate notebook logic there, but `cfb-ats-api` currently consumes the exported `.joblib` + `feature_columns.json` artifacts directly rather than importing this package.

Model retrained after dropping the 2020 (COVID) season and adding `rest_diff` and ATS-streak features. See the notebook for current accuracy metrics — feature engineering is still the main lever to pull.

## Data source

College Football Data API (collegefootballdata.com). Same API key used in `cfb-ats-api`.

## Key features engineered so far

Conference flags, timezone deltas, coaching tenure deltas, pregame ELO, rest differential (`rest_diff`), and ATS record over the last 4 games (`home_ats_last4` / `away_ats_last4`). The 2020 (COVID) season is now dropped from training.

## Related projects

- `../cfb-ats-api` — loads the trained model via `services/model_loader.py`, assembles live feature rows via `featurizer.py`, and serves predictions on `/v1/teams/next-game`
