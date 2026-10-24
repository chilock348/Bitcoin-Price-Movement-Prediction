# Data guide

[Back to the project overview](../README.md)

These Excel workbooks are prepared project inputs used by the existing notebooks. Both combine observations from several sources.

## Workbooks

| File | Worksheet | Purpose |
| :--- | :--- | :--- |
| [CLEAN_blockchain_dot_com_daily_data.xlsx](CLEAN_blockchain_dot_com_daily_data.xlsx) | `base_v3` | Historical V1 and V2 experiments; saved notebook outputs show 2,071 daily records from 1 January 2018 to 2 September 2023 and 2,063 usable modelling rows |
| [today_data.xlsx](today_data.xlsx) | `today_data` | Updated observations used by the recent retrospective case at the end of V2 |

The main historical rolling evaluation covers **1 January 2020–31 August 2023**. Earlier observations supply training history. The notebooks reconstruct the target from the Bitcoin price series rather than using the workbook's precomputed label column.

## Feature groups

| Group | Contents |
| :--- | :--- |
| Bitcoin-specific market features | One-day return, seven-day sum of returns, seven-day return volatility, log change in exchange volume, and market-capitalisation return |
| Traditional markets | Returns derived from S&P 100, S&P 500, Nasdaq 100, Dow Jones, Russell 2000, VIX, US Dollar Index, US 10-Year Treasury Yield Index, and gold futures |
| Other cryptocurrencies · V2 | Returns of ETH, BNB, XRP, BCH, LTC, ADA, LINK, and DOGE |
| On-chain indicators | Mempool size, transaction rate, average block size, average confirmation time, hash rate, difficulty, miners' revenue in USD, and total transaction fees in BTC |

Traditional-market features use the workbook's forward-filled closing-price columns to align with calendar-day crypto observations. Predictor columns are shifted by one row in the modelling notebooks.

## Provenance

- **Historical Bitcoin data:** [aleexharris, Bitcoin Network On-Chain Blockchain Data, Kaggle](https://www.kaggle.com/datasets/aleexharris/bitcoin-network-on-chain-blockchain-data), with underlying indicators from Blockchain.com.
- **Bitcoin series and updates:** [Blockchain.com Charts API](https://www.blockchain.com/explorer/api/charts_api). Intraday mempool-size and transaction-rate observations were aggregated using daily medians during data preparation.
- **Other asset prices:** [Yahoo Finance](https://finance.yahoo.com/).
- **Selected missing cryptocurrency observations:** completed UTC daily candles from [Binance USDT trading pairs](https://developers.binance.com/docs/binance-spot-api-docs/rest-api/market-data-endpoints#klinecandlestick-data).

## Using the files

The current notebooks expect these filenames in their working directory. Copy the relevant workbook beside a local working copy of the notebook, following the [run instructions](../README.md#running-the-notebooks).

The case-study code substitutes Bitcoin price return for `mcap_ret` if market capitalisation is unavailable in the updated workbook. Daily labels from different providers also need timestamp alignment before a strict real-time prediction interpretation is justified.
