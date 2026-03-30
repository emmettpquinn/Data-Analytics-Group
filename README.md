# UCD Data Analytics Group Project

This repository contains an end-to-end notebook pipeline for data quality analysis, cleaning, feature engineering, and house-price modelling.

Main notebook: `main.ipynb`

## 1) Environment Setup

Recommended Python version: 3.11

Use the first cell in `main.ipynb` to install all required packages:

```python
%pip install -r requirements.txt
```

If prompted, restart the notebook kernel after installation.

## 2) Run Order

1. Open `main.ipynb`.
2. Run all cells from top to bottom.
3. Confirm exported files are created.

## 3) Required Input Files

- `ppr-group-22312913-train.csv`
- `ppr-group-22312913-test.csv`
- `external_datasets/mortgage_interest_by_year_month.csv`
- `external_datasets/new_dwellings_by_area_code.csv`
- `external_datasets/population.csv`

## 4) Generated Outputs

- `train_cleaned_full.csv`
- `train_model_ready.csv`
- `test_cleaned_full.csv`
- `test_model_ready.csv`
- `catboost_info/` (training logs)

## 5) Method Summary

- Deduplicate training records on full raw transaction signature.
- Convert and validate key dtypes (date, price, categories).
- Infer Eircode routing keys from address + county with mismatch checks.
- Exclude ambiguous routing keys from county overwrite logic.
- Add internal trailing features with lag to avoid same-month target leakage.
- Merge external features with time-safe lagged keys.
- Train CatBoost on log(price) with time-aware validation.
- Evaluate on provided holdout test set using RMSE, MAE, R2, and MAPE.

## 6) Academic Integrity and Reproducibility Notes

- Keep model/feature selection based on validation/CV, then report holdout once.
- Ensure report claims match notebook outputs exactly.
- Include all external datasets in submission package so graders can re-run without missing files.

## 7) Known Limitations

- Limited property attributes (for example, no floor area and no bedroom count).
- Heavy-tail prices and outliers increase euro-scale error.
- Routing inference improves coverage but cannot recover all missing location information.
