# World Cup 2026 Scoreboard Prediction

Predicting the final scoreline of international football matches from historical
data, with the 2026 FIFA World Cup as the live evaluation target.

## Problem

**Task:** Given only information available before kickoff, predict the final
scoreline — home goals and away goals — for a match.

**Evaluation metric:** Poisson deviance / log-likelihood on the predicted goal
counts (primary), since goals are counts, not a continuous quantity. Accuracy of
the derived match outcome (home win / draw / away win) is reported as a secondary,
more interpretable metric.

**Why this metric was chosen before modeling:** picking the metric after seeing
results invites choosing whichever one flatters the model.

## Approach

**Key design decision — what to train on.** World Cup matches alone are far too few
to learn from (a few hundred across decades, with squads that change completely
between tournaments). Training only on them would produce a model that looks strong
on a tiny test set and is worthless in practice.

Instead: **train on all international matches** (friendlies, qualifiers, continental
cups — thousands of matches), and use the **World Cup as the prediction target and
showcase**.

**Avoiding data leakage.** Every engineered feature uses only information available
*before* kickoff. Evaluation uses **time-based splits** — train on earlier matches,
test on later ones — never random splits, since in reality you predict the future
from the past.

## Data

- International football results, 1872–present, including historical team
  name changes — [martj42/international_results](https://github.com/martj42/international_results)
- Elo ratings for 2026 World Cup squads — [Kaggle: 2026 FIFA World Cup Historical Elo Ratings](https://www.kaggle.com/datasets/afonsofernandescruz/2026-fifa-world-cup-historical-elo-ratings)
- EA FC 26 player ratings, for aggregating into squad-strength features —
  [Kaggle: FC 26 (FIFA 26) Player Data](https://www.kaggle.com/datasets/rovnez/fc-26-fifa-26-player-data)

Raw data is committed under `datasets/` (see `dataset_source.txt` for links).

## Results

*(To be filled in.)*

| Model                              | Poisson deviance | Outcome accuracy |
| ----------------------------------- | ----------------- | ----------------- |
| Baseline (average goals per team)   | —                 | —                 |
| Baseline (Elo-implied)              | —                 | —                 |
| Poisson regression                  | —                 | —                 |
| Gradient-boosted (XGBoost, Poisson) | —                 | —                 |

## Project structure

```
datasets/        raw data (results, Elo ratings, EA FC player ratings)
notebook.ipynb   loading, cleaning, feature engineering, modeling, evaluation
```

## Running it

```bash
conda create --name worldcup python=3.11
conda activate worldcup
pip install -r requirements.txt
```

## Limitations

*(To be filled in.)*

## Next steps

*(To be filled in.)*
