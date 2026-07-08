---
title: "Kairos: Statistical Arbitrage Trading System"
order: 1
excerpt: "A pairs-trading system combining cointegration testing, Kalman filtering, and an AI agent risk layer to trade US equities on Alpaca's paper trading platform."
---
## Overview
Kairos is an ongoing personal project exploring statistical arbitrage: finding pairs of stocks whose prices historically move together, detecting when they've drifted apart, and betting on that relationship reverting.
The project is built around a specific problem with pure statistical approaches: a cointegration test has no way of knowing when the underlying relationship between two companies has permanently changed (a merger, a guidance shock, a regulatory event). Kairos pairs the statistical signal with an AI research agent designed to catch exactly that failure mode before a trade is placed.
> **NB:** All trading runs against Alpaca's paper trading API. No real capital is involved.

## Approach
The project is structured around three pillars:
- **Time-series statistics** — Engle-Granger cointegration testing (ADF, OLS regression) to identify mean-reverting pairs, filtered against a plausible economic rationale rather than statistics alone.
- **Machine learning** — a Kalman filter estimating a time-varying hedge ratio, benchmarked against a static OLS baseline.
- **AI agents** — a LangGraph-based research agent embedded in the trading pipeline itself, acting as a fundamental risk gate between signal and execution rather than as a tool used to build the system.

## Dataset
Two years of daily price bars for a curated universe of ~20 tickers across energy and consumer staples, pulled via the Alpaca Market Data API.

## Architecture

Kairos is organized as a modular statistical arbitrage workflow that moves from market data ingestion to pair screening, signal generation, backtesting, and eventually paper trading execution.

The current architecture includes:

- **Market data ingestion**  
  Historical daily price bars are pulled from the Alpaca Market Data API for a curated universe of equities.

- **Stationarity testing**  
  Individual price series are screened using Augmented Dickey-Fuller tests to evaluate whether they are stationary or require pair-based mean-reversion analysis.

- **Pairwise cointegration screening**  
  Stock pairs are tested using Engle-Granger cointegration logic to identify relationships that may exhibit long-run mean reversion.

- **Economic filtering**  
  Statistically valid pairs are filtered further based on whether the relationship makes economic sense, reducing reliance on purely statistical correlations.

- **Hedge ratio estimation**  
  Approved pairs are modeled using both a static OLS hedge ratio and a dynamic Kalman filter hedge ratio, allowing comparison between fixed and time-varying pair relationships.

- **Spread and signal generation**  
  Pair spreads are calculated and converted into rolling z-score signals to identify potential entry and exit opportunities.

- **Backtesting engine**  
  Generated signals are evaluated through a backtesting framework that tracks cumulative P&L, Sharpe ratio, maximum drawdown, and equity curves.

- **Risk and execution layer**  
  The planned production architecture adds a LangGraph-based research agent as a fundamental risk gate before trades are sent to Alpaca's paper trading API.

## Current Status
- Cointegration screening across 150+ ticker pair combinations
- Rolling z-score signal generation and a backtesting engine reporting Sharpe ratio, max drawdown, and cumulative P&L
- Kalman filter for dynamic hedge ratio estimation, compared directly against the static baseline
- MySQL persistence for pair statistics and trade decisions *(in progress)*

<figure style="text-align: center; margin: 2em 0;">
  <img src="/assets/images/projects/kairos_project/equity_curves.png"
       alt="Equity curves from statistical arbitrage backtests"
       style="max-width: 100%; border-radius: 6px;">
  <figcaption>
    <strong>Figure.</strong> Portfolio equity curves generated from multiple cointegrated trading pairs during statistical arbitrage backtesting.
  </figcaption>
</figure>

## Roadmap
- LangGraph research agent screening news/filings for fundamental breaks before trade execution
- Live paper-trading loop against Alpaca
- Daily reporting agent summarizing trades taken, trades skipped, and why
- FastAPI service layer, containerized and deployed on Azure

## Repository
[View Code](https://github.com/joe-ledford-04/kairos)
