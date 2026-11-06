# 📈 Vega — Copy Trading & Trade Analytics Engine

> A Python trading-journal and copy-trading engine that records every trade, analyses performance in real time, visualises strategy effectiveness, and keeps data in sync across local MongoDB, MongoDB Atlas and JSON — with a remote-triggered self-destruct mode for data security.

![Python](https://img.shields.io/badge/Python-3776AB?style=flat-square&logo=python&logoColor=white) ![MongoDB](https://img.shields.io/badge/MongoDB-47A248?style=flat-square&logo=mongodb&logoColor=white) ![Matplotlib](https://img.shields.io/badge/Matplotlib-11557C?style=flat-square) ![License-Apache 2.0](https://img.shields.io/badge/License--Apache%202.0-D22128?style=flat-square)

---

## 📖 Overview

Vega started in **2022** as my first serious attempt at building trading tooling. Traders feed it the details of each trade (entry/bid price, exit price, the technical indicators that triggered the trade, and the stock), and Vega:

1. computes per-trade and per-day P&L, win/loss ratios and running averages,
2. persists everything redundantly to **local MongoDB**, **MongoDB Atlas** and **JSON files** (so it still works fully offline),
3. renders charts that show which indicators actually make money, and
4. listens for a server-side flag that can back up and **wipe the local install** (self-destruct) if a machine is compromised.

It later evolved into the [StockAverage](https://github.com/optimus-node-js/StockAverageUpdatedLastBugFixRequired) line of tools and, eventually, my Angel One–based algo-trading work ([algoFinance](https://github.com/optimus-node-js/algoFinance), [Finance-Algo](https://github.com/optimus-node-js/Finance-Algo)).

## ✨ Features

| Area | What it does |
|---|---|
| **Copy-trade journal** | Interactive CLI to log bid price, closing price, indicators used and stock name for every trade |
| **Real-time analytics** | Total profit/loss, average profit/loss per trade, win/loss ratio, trades per day |
| **Indicator analysis** | Tracks which indicators were used on winning vs. losing trades |
| **Visualisation** | Matplotlib charts for indicator success rate, daily totals and historical trade performance |
| **Triple storage** | Local MongoDB + MongoDB Atlas + JSON (`eachStockData`, `todaySumData`, `averageData`) |
| **Binary backup** | `BinaryBackup.py` snapshots data before destructive operations |
| **Self-destruct mode** | Remote parameter check (`Params.json` / server flag) that backs up and removes local program data |
| **Colourised CLI** | `colorama`-powered prompts and status output |

## 🏗️ Architecture

```
            ┌──────────────────────┐
  trader ──▶│  StockAverage.py CLI │── input validation, P&L engine
            └─────────┬────────────┘
                      │ eachStockData / todaySum / averageData
        ┌─────────────┼──────────────┬───────────────┐
        ▼             ▼              ▼               ▼
  Local MongoDB   MongoDB Atlas   JSON files     plotData.py (charts)
                      ▲
                      │ remote params (self-destruct / backup flags)
              ParamCheck() ──▶ BinaryBackup.py
```

## 📂 Project Structure

```
Vega_CopyTrading_Platform/
├── Body Code/
│   ├── StockAverage.py     # main engine: input loop, analytics, storage
│   ├── plotData.py         # matplotlib visualisations
│   ├── BinaryBackup.py     # backup before self-destruct
│   ├── Params.json         # runtime flags (storage targets, self-destruct)
│   └── *.json              # local JSON data stores
├── test/main.py
├── requirements.txt
└── LICENSE
```

## 🚀 Getting Started

**Prerequisites:** Python 3.10+, MongoDB (local) and/or a MongoDB Atlas cluster.

```bash
git clone https://github.com/optimus-node-js/Vega_CopyTrading_Platform.git
cd Vega_CopyTrading_Platform
```

```bash
pip install -r requirements.txt
```

Configure your MongoDB connection strings in `Body Code/StockAverage.py` (`LocalMongoFunction` / `ServerMongo`) — credentials in this public repo are redacted as `***REDACTED***`; use your own (ideally through environment variables).

```bash
cd "Body Code"
python StockAverage.py
```

Then follow the prompts:

```
Bidding Price >> 512.40
Closing Price >> 530.10
Number of Indicators Used >> 2
Enter the Indicator Number 1 >> RSI
Enter the Indicator Number 2 >> MACD
Enter the Stock Name >> TATAMOTORS
Press 'c' to continue else 'e' to Exit :
```

## 🗺️ Evolution

| Year | Milestone |
|---|---|
| 2022 | Vega CLI copy-trading journal with MongoDB + JSON storage |
| 2023 | StockAverage variants with self-destruct mode and binary backups |
| 2024 | Angel One SmartAPI integrations — portfolio & dividend trackers |
| 2025–26 | Microservice HFT platform and FastAPI paper-trading engine |

## 📄 License

Licensed under the [Apache 2.0 License](LICENSE).

---

## 👤 Author

**Rahul Vishwakarma** — Senior Full Stack Developer · Ahmedabad, India

[![Portfolio](https://img.shields.io/badge/Portfolio-rahul--vishwakarma--portfolio.vercel.app-0A66C2?style=flat-square&logo=vercel&logoColor=white)](https://rahul-vishwakarma-portfolio.vercel.app/)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Rahul%20Vishwakarma-0A66C2?style=flat-square&logo=linkedin&logoColor=white)](https://linkedin.com/in/rahul-vishwakarma-101346192)
[![Email](https://img.shields.io/badge/Email-karmarahul67%40gmail.com-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:karmarahul67@gmail.com)
[![GitHub](https://img.shields.io/badge/GitHub-optimus--node--js-181717?style=flat-square&logo=github)](https://github.com/optimus-node-js)

If you find this project useful, consider giving it a ⭐.
