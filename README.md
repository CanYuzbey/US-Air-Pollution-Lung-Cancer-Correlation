# DSA210: AQI and illustrative lung cancer rates

This repository demonstrates a data analysis workflow that combines observed air-quality data with **illustrative, generated** lung-cancer-rate series. It is a software and methods exercise, not an empirical study of the relationship between air pollution and cancer incidence.

## Data provenance

- **Air quality:** `scripts/fetch_real_data.py` downloads EPA daily county AQI files for 2010–2022 and aggregates the selected states' county readings to state-day means. The committed `data/air/` files appear to come from that process, but the repository has no source manifest that independently verifies them. A state-day mean of county AQI values should not be interpreted as population exposure.
- **Cancer rates:** The same script's `generate_cdc_data()` function writes `data/cancer/` files from approximate state starting values, fixed yearly declines, and random noise. These values are **not observed CDC state-year incidence rates**. The script does not download CDC incidence files. The separate `scripts/generate_synthetic_data.py` can also generate synthetic air and cancer series.
- The generation code does not set a random seed, so regenerated cancer values and downstream metrics may differ from the committed examples.

## What the project demonstrates

The repository includes data loading and cleaning, exploratory plots, a Pearson correlation calculation, and a comparison of linear regression, random forest, and gradient boosting models with cross-validation. These tools illustrate an analysis workflow. The committed plots and metrics describe this mixed observed/generated dataset only.

## Interpretation limits

The reported correlation coefficient, p-value, feature importance, and predictive scores **cannot establish a real-world association or predictive relationship** between air pollution and lung cancer. In addition to the generated outcome variable, any future empirical study would need to address population exposure, smoking, age, occupational exposures, time lags, state-level aggregation, and source-specific data quality. No causal claim is supported here.

## Reproduce the workflow

```bash
python -m pip install -r requirements.txt
python scripts/fetch_real_data.py
python ml_analysis.py
python -m unittest discover tests
```

The first command after installation downloads EPA AQI data and regenerates the illustrative cancer series. It does not retrieve observed CDC cancer rates. The exploratory notebook and figures in this repository should be read with the same data-provenance limitation.

## Next step for an empirical study

Obtain source-linked observed CDC state-year cancer incidence data with a documented license and extraction procedure. Replace the generated cancer CSV files, rerun the notebook, figures, statistics, and models, then review the study design before making any public-health inference.
