# Apparent Temperature Estimation

Estimate how warm or cold conditions feel using contemporaneous temperature, humidity, wind speed, precipitation type and pressure.

## Task

The original repository called this forecasting, but its inputs describe the same observation as the target. This refreshed experiment presents it as supervised regression. Its original single-timestep BiLSTM remains in `legacy/`; the new notebook compares Ridge regression and histogram gradient boosting with a median baseline.

## Evaluation

Observations are sorted by timestamp and duplicate timestamps removed. The earliest 80% train the models; the latest 20% form the test partition. Imputation, scaling and category encoding fit only training data. Metrics are MAE and RMSE in degrees Celsius. Invalid nonpositive pressure values are treated as missing.

## Setup

Use Python 3.10 or 3.11. From the repository root:

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
jupyter lab
```

Open the notebook under `notebooks/` and run its cells in order. Data belongs in `data/`; generated results go to `artifacts/`.

Open `notebooks/temperature_estimation.ipynb`. See [input instructions](data/README.md).

## Outputs

| File | Purpose |
|---|---|
| `artifacts/metrics.json` | Baseline and model errors |
| `artifacts/predicted_vs_observed.png` | Test-set prediction plot |
| `artifacts/*.joblib` | Models with fitted preprocessing |

## Results and limits

No new benchmark scores are claimed until the notebook is run on the external dataset. Contemporary temperature is strongly related to apparent temperature; good fit does not imply future weather forecasting skill. A forecast would need a defined future horizon and only inputs available at prediction time.

The original notebook and saved model are retained as historical artifacts. They are not compatible with the new regression pipeline.
