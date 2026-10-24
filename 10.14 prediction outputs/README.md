# Recent retrospective case · 14 October 2026

[Back to the project overview](../README.md) · [Open V2 notebook](../V2.ipynb)

The final case-study cells in V2 retrain each model using its historically selected feature set, window parameter, and threshold, then classify the recorded Bitcoin price direction for **14 October 2026**. These exports were generated on **17 October 2026 at 10:38**.

## Result at a glance

| Item | Saved result |
| :--- | :--- |
| Models used | 9 |
| Individual model directions | All up |
| Observed direction | Up |
| Mean model upward score | 0.9088 |
| Ensemble direction at threshold 0.5 | Up |

This is one shared target date evaluated retrospectively. The mean score is an arithmetic average of model outputs, rather than a separately calibrated probability.

## Output files

| File | Contents |
| :--- | :--- |
| [Individual predictions](prediction_2026-10-14_20261017_1038_predictions.csv) | Model configuration, training count, upward score, predicted label, and observed label |
| [Frozen configurations](prediction_2026-10-14_20261017_1038_best_configs.csv) | Historical V2 configurations used for this case |
| [Model summary](prediction_2026-10-14_20261017_1038_by_model.csv) | Readable model-level summary |
| [Feature-set summary](prediction_2026-10-14_20261017_1038_by_feature.csv) | Case results grouped by selected feature set |
| [Ensemble summary](prediction_2026-10-14_20261017_1038_ensemble.csv) | Average upward score, direction, and observed outcome |
| [Excel summary](prediction_2026-10-14_sum.xlsx) | Combined case-study workbook |

To reproduce this stage, run the earlier cells of V2 first and place `today_data.xlsx` beside the working notebook. See [run instructions](../README.md#running-the-notebooks) and the [data guide](../dataset/README.md).
