# V1 results · Baseline features

[Back to the project overview](../README.md) · [Open V1 notebook](../V1.ipynb) · [Compare V2 results](../V2%20output/README.md)

V1 uses **14 market features** drawn from Bitcoin-specific and traditional-market series, plus **8 on-chain indicators**. Returns of other cryptocurrencies are excluded from the model inputs. The experiment compares market-only, on-chain-only, and combined configurations.

## Saved result tables

| File | What it contains |
| :--- | :--- |
| [Best configuration per model](model_performance_summary_20261017_1726_best_per_model.csv) | Each model's highest-F1 configuration across feature sets, windows, and thresholds |
| [Feature-set summary](model_performance_summary_20261017_1726_by_feature.csv) | Metrics averaged across the nine models' selected configurations for each feature set |
| [Model summary](model_performance_summary_20261017_1726_by_model.csv) | Aggregate metrics grouped by model |
| [Detailed results](model_performance_summary_20261017_1726_detail.csv) | F1-selected window and threshold for each model–feature-set pair |
| [Excel summary](model_performance_summary_20261017_1726.xlsx) | Workbook containing the saved result summaries |

Logistic Regression has the highest selected F1 (**0.7519**). All nine models' best-F1 configurations use market-only features.

## Figures

| Analysis | Figure |
| :--- | :--- |
| Model and feature-set ROC-AUC comparison | [auc_bar.png](auc_bar.png) |
| Exploratory feature importance and target correlation | [feature_importance_ranking.png](feature_importance_ranking.png) |
| Feature correlations | [correlation_heatmap.png](correlation_heatmap.png) |
| Accuracy by month | [accuracy_all_models_single_plot.png](accuracy_all_models_single_plot.png) |
| Monthly accuracy heatmaps | [model_best_accuracy_heatmap.png](model_best_accuracy_heatmap.png) · [model_best_accuracy_heatmap_v2.png](model_best_accuracy_heatmap_v2.png) |
| F1 versus threshold at each model's selected window | [bestwindow_f1_vs_threshold.png](bestwindow_f1_vs_threshold.png) |
| Threshold sensitivity | [threshold_sensitivity_F1.png](threshold_sensitivity_F1.png) |
| Window sensitivity | [window_sensitivity_F1.png](window_sensitivity_F1.png) |

The output filename timestamp is **17 October 2026, 17:26**; it identifies the saved export rather than the historical evaluation dates. Interpretation of selected scores is described in the [project overview](../README.md#interpreting-the-scores).
