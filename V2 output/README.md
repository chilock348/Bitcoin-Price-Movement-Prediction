# V2 results: Cross-cryptocurrency feature extension

[Back to the project overview](../README.md) | [Open V2 notebook](../V2.ipynb) | [Compare V1 results](../V1%20output/README.md)

V2 adds returns of **ETH, BNB, XRP, BCH, LTC, ADA, LINK, and DOGE**, increasing the market block from **14 to 22 features**. The on-chain block retains its **8 indicators**. The same three feature configurations and nine model families are considered.

## Saved result tables

| File | What it contains |
| :--- | :--- |
| [Best configuration per model](model_performance_summary_20261017_1147_best_per_model.csv) | Each model's highest-F1 configuration across feature sets, windows, and thresholds |
| [Feature-set summary](model_performance_summary_20261017_1147_by_feature.csv) | Metrics averaged across the nine models' selected configurations for each feature set |
| [Model summary](model_performance_summary_20261017_1147_by_model.csv) | Aggregate metrics grouped by model |
| [Detailed results](model_performance_summary_20261017_1147_detail.csv) | F1-selected window and threshold for each model–feature-set pair |
| [Excel summary](model_performance_summary_20261017_1147.xlsx) | Workbook containing the saved result summaries |

Random Forest ranks first by selected F1 (**0.8604**) with combined features. Eight of nine models select market-only features; the market-only average F1 is **0.8293**.

## Figures

| Analysis | Figure |
| :--- | :--- |
| Model and feature-set ROC-AUC comparison | [auc_bar.png](auc_bar.png) |
| Exploratory feature importance and target correlation | [feature_importance_ranking.png](feature_importance_ranking.png) |
| Feature correlations | [correlation_heatmap.png](correlation_heatmap.png) |
| Accuracy by month | [accuracy_all_models_single_plot.png](accuracy_all_models_single_plot.png) |
| Monthly accuracy heatmaps | [model_best_accuracy_heatmap.png](model_best_accuracy_heatmap.png); [model_best_accuracy_heatmap_v2.png](model_best_accuracy_heatmap_v2.png) |
| F1 versus threshold at each model's selected window | [bestwindow_f1_vs_threshold.png](bestwindow_f1_vs_threshold.png) |
| Threshold sensitivity | [threshold_sensitivity_F1.png](threshold_sensitivity_F1.png) |
| Window sensitivity | [window_sensitivity_F1.png](window_sensitivity_F1.png) |

The output filename timestamp is **17 October 2026, 11:47**; it identifies the saved export rather than the historical evaluation dates. Interpretation of selected scores is described in the [project overview](../README.md#interpreting-the-scores).
