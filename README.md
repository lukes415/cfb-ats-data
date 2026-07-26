# College Football Against the Spread Picker
This repo is for producing datasets and machine learning models to pick college football games against the spread

# Understanding
The primary file is [here](/data/notebooks/hate_watch_ATS_data_file.ipynb)

# Current Status
The model is trained, exported, and wired end-to-end into [cfb-ats-api](https://github.com/lukes415/cfb-ats-api), which serves picks to [hate-watch-ios](https://github.com/lukes415/hate-watch-ios). This repo now focuses on feature engineering and retraining to improve accuracy.

# Data Source
We pull, clean, and manipulate data from:
- [College Football Data](https://collegefootballdata.com)

# Goal
- [x] Engineer features to predict ATS outcomes using ingested CFB data
- [x] Create baseline models, evaluate vs. obvious heuristics and try to improve upon them
- [x] Integrate dataset and models with an iOS app to help users enjoy college football weekends more
- [ ] See if my model can outperform me in my pickem league. I usually come in the top third of the league
- [ ] Have fun :grin:

# Completed
- [x] Update the dataset to include conference flags, timezone deltas, and coaching tenure deltas
- [x] Check how many records are missing specific datapoints and try to decide on reasonable substitutions
- [x] Drop the 2020 (COVID) season from training data
- [x] Add `rest_diff` and `home_ats_last4` / `away_ats_last4` features
- [x] Retrain and export the model (`models/cfb_ats_model.joblib`) and `models/feature_columns.json` for the API to load

# In Progress
- [ ] Further interrogate feature importances and keep iterating on feature engineering to push accuracy past the current baseline

# Updates
Retrained after adding rest differential, ATS streak features, and dropping the COVID year. See `data/notebooks/hate_watch_ATS_data_file.ipynb` for the latest training run and metrics.
