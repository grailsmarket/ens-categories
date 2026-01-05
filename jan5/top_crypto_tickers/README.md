# Top Crypto Tickers

This directory contains cryptocurrency ticker symbols, normalized for ENS name matching.

## Output

- **File**: `tickers.csv`
- **Contents**: 279 cryptocurrency tickers with `.eth` suffix
- **Columns**:
  - `ticker`: Ticker symbol with .eth appended (e.g., `BTC.eth`)

## Data Sources

This list is the **intersection** of two major cryptocurrency ranking sources:

1. **CoinGecko** - Top ~500 cryptocurrencies by market cap
2. **CoinMarketCap** - Top ~500 cryptocurrencies by market cap

Only tokens that appear in **both** lists are included, ensuring high-confidence coverage of established cryptocurrencies.

## Processing Steps

### 1. Source Intersection
- Read both source files
- Match by ticker symbol
- Keep only tokens present in both lists

### 2. Ranking
- Calculate average position across both sources
- Sort by average rank (highest market cap first)

### 3. Filtering
- Remove tickers with fewer than 3 characters (e.g., `AB`, `CC`, `M`)
- **Result**: 303 → 279 tickers

### 4. ENS Suffix
- Append `.eth` to each ticker

## Sample Output

```
ticker
BTC.eth
ETH.eth
BNB.eth
XRP.eth
TRX.eth
ADA.eth
BCH.eth
LINK.eth
LEO.eth
ZEC.eth
```

## Date Processed

2026-01-05

