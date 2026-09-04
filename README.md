# SPY Options Data Exploration

Exploratory analysis of the full SPY option chain over five trading days (Aug 1–5, 2022): data cleaning, liquidity, the implied-volatility surface, Greeks, implied forwards, and straddle outcomes. Everything is reproducible from the included CSV using only pandas, numpy, and matplotlib.

The full analysis is in [options_notebook.ipynb](options_notebook.ipynb); figures are embedded, so it renders directly on GitHub.

## Dataset

`spy_options_data.csv` (6.3 MB) contains end-of-day (16:00 ET) snapshots of the SPY option chain:

- 22,962 rows, one per (trade date, expiry, strike)
- 36 expiries out to Dec 2024; strikes 85–720
- Columns: underlying price, expiry, DTE, strike, and call/put delta, gamma, vega, theta, rho, IV, volume, last, bid, ask, and quote size
- No open interest and no intraday data

## Notebook contents

| # | Section | Contents |
|---|---------|----------|
| 1 | Data cleaning | Header/text normalization, numeric coercion, quote-size parsing, an IV sanity screen with a reproducible audit of masked values |
| 2 | Market overview | Daily closes and the put/call volume ratio |
| 3 | Volume concentration | 41% of volume expires within one day; ±12% moneyness captures 93% of volume |
| 4 | Liquidity | Relative bid–ask spread and quoted depth by moneyness × DTE bucket |
| 5 | IV term structure | ATM IV by expiry across the week; Friday ended below Monday at 28 of 30 common expiries |
| 6 | Trading-day and forward volatility | Trading-day normalization of the weekend sawtooth; forward vol between adjacent expiries |
| 7 | Smile and skew | OTM smile and 25Δ risk reversal for all five dates |
| 8 | Greeks near the money | ATM gamma and theta by maturity; delta/gamma across a ±6% strike window |
| 9 | Implied forwards | Forward curve from put–call parity, with a zoom on the Aug–Oct carry adjustment |
| 10 | Straddle break-evens | Exact asymmetric break-even ranges and the realized expiration payoff |
| 11 | Conclusions | Summary of the results |

## Running it

```bash
pip install -r requirements.txt
jupyter notebook options_notebook.ipynb
```

Tested with Python 3.9+, pandas, numpy, and matplotlib; no other dependencies.
