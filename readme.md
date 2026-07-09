# World Cup Match Outcome Prediction

Predicting international football match outcomes from historical data, with the
2026 FIFA World Cup as the live evaluation target.

## Problem

**Task:** Given only information available before kickoff, predict the match result
as one of three classes — home win, draw, or away win.

**Evaluation metric:** log-loss (primary). I care about *calibrated probabilities*,
not just whether the top pick is right — a model that says 70% should win ~70% of
the time. Accuracy and a calibration curve are reported as secondary.

**Why log-loss was chosen before modeling:** picking the metric after seeing results
invites choosing whichever one flatters the model.

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

- International football results (1872–present) — [source / link]
- FIFA rankings over time — [source / link]

Raw data is not committed to this repo. Download from the links above into `data/raw/`.

## Results

*(To be filled in.)*

| Model                             | Log-loss | Accuracy |
| --------------------------------- | -------- | -------- |
| Baseline (always home)            | —       | —       |
| Baseline (FIFA ranking favourite) | —       | —       |
| Logistic regression               | —       | —       |
| Gradient-boosted (XGBoost)        | —       | —       |

## Project structure

```
data/          raw (gitignored) and processed datasets
notebooks/     exploration only
src/data/      loading and cleaning
src/features/  feature engineering
src/models/    training and evaluation
api/           FastAPI service
tests/
```

## Running it

```bash
conda create --name worldcup python=3.11
conda activate worldcup
pip install -r requirements.txt
```

## Limitations

*(To be filled in — be honest here.)*

## Next steps

*(To be filled in.)*
