# Predicting Bitcoin Price Direction

### Model comparison and feature extension with market and on-chain data

**MH6805 Machine Learning in Finance · Group 7**  
Zhou Yan · Chen Xixi · Chen Liuchi

How do model choice and input features affect Bitcoin price-direction classification? This project follows an experimental progression: establish a baseline, add information from other cryptocurrencies, and examine whether on-chain indicators contribute further value.

[Research design](#research-design) · [Results](#results) · [Repository guide](#repository-guide) · [Running the notebooks](#running-the-notebooks) · [Data sources](#data-sources)

## Research design

The task is binary classification of Bitcoin's recorded daily price direction. For a date D, the notebooks assign **1 (up)** if the recorded Bitcoin price exceeds its value on the preceding date, and **0 (non-up)** otherwise. Predictor features are shifted by one row before modelling.

| Stage | Question | Market features | On-chain features | Notebook |
| :--- | :--- | :--- | :--- | :--- |
| **V1 · Baseline** | How do the models perform with Bitcoin and traditional-market information? | 14 Bitcoin-specific and traditional-market features | 8 | [V1.ipynb](V1.ipynb) |
| **V2 · Feature extension** | How do results change after adding other cryptocurrency returns? | 22 features: V1 market features plus returns of 8 other cryptocurrencies | 8 | [V2.ipynb](V2.ipynb) |
| **Recent case** | Can the workflow be applied to an updated dataset? | Each model's selected V2 feature configuration | Where selected | Final case-study cells in [V2.ipynb](V2.ipynb) |

Both historical experiments compare **market-only**, **on-chain-only**, and **market + on-chain** configurations. V2 adds daily returns of **ETH, BNB, XRP, BCH, LTC, ADA, LINK, and DOGE**.

### Models and evaluation

Nine classifiers are included: KNN, Logistic Regression, Linear Discriminant Analysis (LDA), Linear SVM, Decision Tree, Random Forest, AdaBoost, XGBoost, and a Multi-Layer Perceptron (MLP) neural network.

| Component | Experimental setting |
| :--- | :--- |
| Historical observations | 1 January 2018–2 September 2023; 2,071 records before feature construction |
| Complete modelling observations | 2,063 after feature construction and predictor lagging |
| Rolling evaluation | 1 January 2020–31 August 2023; 1,339 prediction dates in the reported selected configurations |
| Rolling-window parameter | 7, 15, 30, 45, 60, 90, 120, or 150 calendar days |
| Decision thresholds | 0.30, 0.35, 0.40, 0.45, 0.50, or 0.55 |
| Configuration selection | Highest F1 for each model and feature set |
| Reported metrics | Accuracy, F1, and ROC-AUC |

The training slice for date D is **[D − w − 1, D − 1]**, inclusive: a complete slice contains **w + 1 observations**. The minimum training count is `max(3, int(0.8 * w))`. Median imputation and, where applicable, standardization are fitted within each rolling training window. Full-sample feature-importance plots are exploratory; the Top-K settings retain all 14/22 market and 8 on-chain features.

## Results

### Adding cryptocurrency returns changes both performance and model rankings

The table below averages the F1-selected configurations across the nine models. It is an **average of model metrics**, not the performance of an ensemble.

| Feature configuration | V1 Accuracy | V2 Accuracy | V1 F1 | V2 F1 | V1 ROC-AUC | V2 ROC-AUC |
| :--- | ---: | ---: | ---: | ---: | ---: | ---: |
| **Market only** | **65.53%** | **81.79%** | **0.7131** | **0.8293** | **0.7271** | **0.8882** |
| Market + on-chain | 63.07% | 80.23% | 0.6927 | 0.8171 | 0.6839 | 0.8687 |
| On-chain only | 50.72% | 50.74% | 0.6390 | 0.6383 | 0.4859 | 0.4852 |

Source tables: [V1 feature-set summary](V1%20output/model_performance_summary_20261017_1726_by_feature.csv) · [V2 feature-set summary](V2%20output/model_performance_summary_20261017_1147_by_feature.csv)

- **V1:** Logistic Regression ranks first by selected F1 (**0.7519**), followed by LDA and Linear SVM. All nine models select market-only features for their best F1.
- **V2:** Random Forest ranks first (**F1 0.8604; accuracy 85.59%; ROC-AUC 0.9270**) with combined features. XGBoost and Logistic Regression follow.
- **On-chain contribution:** Eight of nine V2 models select market-only features. Random Forest's combined-feature F1 exceeds its market-only F1 by only **0.0008**; the configurations also use different training windows.

These observations motivate the project's central discussion: richer inputs can change which models perform best, while adding more variables does not guarantee an improvement.

### Compare the experiments visually

**V1 · Bitcoin-specific and traditional-market features**

![V1 ROC-AUC comparison across nine models and three feature configurations](V1%20output/auc_bar.png)

**V2 · Additional cross-cryptocurrency returns**

![V2 ROC-AUC comparison across nine models and three feature configurations](V2%20output/auc_bar.png)

The red dashed line marks ROC-AUC = 0.5. More plots—including feature importance, monthly accuracy, and threshold/window sensitivity—are linked in the [V1 results guide](V1%20output/README.md) and [V2 results guide](V2%20output/README.md).

### Recent retrospective case

For **14 October 2026**, all nine models classify the recorded direction as **up**, matching the observed label. Their mean upward score is **0.9088**. The saved output was generated on 17 October 2026, so this is a retrospective workflow demonstration. The mean score is an arithmetic average of model outputs, and the nine predictions concern one shared target date.

[View the case-study outputs](10.14%20prediction%20outputs/README.md)

### Interpreting the scores

These are exploratory rolling-evaluation results: window lengths and thresholds were selected on the same period used to report performance. Cross-source daily-price timestamps also require a common availability cutoff before the scores can be interpreted as strict real-time next-day forecasting performance. The V1–V2 comparison describes the saved experimental pipelines, rather than an isolated causal effect of adding a single variable.

## Repository guide

| Location | Contents | Start here for |
| :--- | :--- | :--- |
| [V1.ipynb](V1.ipynb) | Baseline experiment with saved cell outputs | Initial feature set, models, and rolling evaluation |
| [V2.ipynb](V2.ipynb) | Extended-feature experiment and recent-case cells | V2 comparison and the recent retrospective case |
| [dataset/](dataset/README.md) | Historical and updated Excel workbooks | Input files, worksheet names, and provenance |
| [V1 output/](V1%20output/README.md) | V1 CSV/Excel summaries and figures | Baseline results and sensitivity plots |
| [V2 output/](V2%20output/README.md) | V2 CSV/Excel summaries and figures | Extended-feature results and sensitivity plots |
| [10.14 prediction outputs/](10.14%20prediction%20outputs/README.md) | Saved results for 14 October 2026 | Individual model outputs and aggregate scores |
| [requirements.txt](requirements.txt) | Packages used by the notebooks | Environment setup |

The notebooks already contain saved outputs and can be read on GitHub without rerunning the experiments.

## Running the notebooks

The saved notebook metadata records **Python 3.11.7**. The dependency list is inferred from imports and Excel I/O; it is not a lockfile for the original environment, so package-version differences can affect rerun results.

1. Download or clone the repository and open a terminal in its root folder.
2. Install the dependencies and start JupyterLab:

   ```bash
   python -m pip install -r requirements.txt
   python -m jupyterlab
   ```

3. Create two separate local working folders, one for each experiment. Copy the following files into them:

   | Working folder | Files to copy |
   | :--- | :--- |
   | V1 working folder | `V1.ipynb` and `dataset/CLEAN_blockchain_dot_com_daily_data.xlsx` |
   | V2 working folder | `V2.ipynb`, `dataset/CLEAN_blockchain_dot_com_daily_data.xlsx`, and `dataset/today_data.xlsx` |

   Place each workbook **beside the copied notebook**, keeping its original filename. The existing notebooks read bare filenames and save several figures under identical names; separate working folders keep the two experiments' generated files apart.

4. Open each copied notebook and run its cells in order from the top. V1 and V2 are separate runs. The recent-case cells at the end of V2 depend on variables created by its earlier historical-experiment cells.
5. The full rolling grid retrains models repeatedly and can take considerable time. Install XGBoost to include all nine models; otherwise the notebook skips it. Some short-window configurations may fail because of model-specific sample requirements.

The historical worksheet is **`base_v3`**; the recent-case worksheet is **`today_data`**. See the [data guide](dataset/README.md) for input details.

## Data sources

- [Kaggle — Bitcoin Network On-Chain Blockchain Data](https://www.kaggle.com/datasets/aleexharris/bitcoin-network-on-chain-blockchain-data): historical Bitcoin data downloaded for the project, with underlying Blockchain.com indicators.
- [Blockchain.com Charts API](https://www.blockchain.com/explorer/api/charts_api): Bitcoin-specific market and network series, including subsequent data updates.
- [Yahoo Finance](https://finance.yahoo.com/): other cryptocurrency prices, US equity benchmarks, and additional financial-market series.
- [Binance Spot API — Kline/candlestick data](https://developers.binance.com/docs/binance-spot-api-docs/rest-api/market-data-endpoints#klinecandlestick-data): completed UTC cryptocurrency candles used to supplement selected missing observations.

The workbooks are project-prepared inputs combining these sources; they are not unmodified provider downloads. Attribution and source context are documented in the [data guide](dataset/README.md).

## Project team

**Zhou Yan · Chen Xixi · Chen Liuchi**  
MH6805 Machine Learning in Finance · Group 7
