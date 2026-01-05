# Top Crypto Names

This directory contains cryptocurrency project names, normalized for ENS name matching.

## Output

- **File**: `names.csv`
- **Contents**: 279 cryptocurrency names with `.eth` suffix
- **Columns**:
  - `name`: Normalized project name with .eth appended (e.g., `Bitcoin.eth`)

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
- Remove names with fewer than 3 characters
- **Result**: 303 → 279 names

### 4. Name Normalization

Names are cleaned to contain only alphanumeric characters:

| Transformation | Example |
|----------------|---------|
| Remove spaces | `Bitcoin Cash` → `BitcoinCash` |
| Strip parentheses | `Polygon (prev. MATIC)` → `Polygon` |
| Strip brackets | `BitTorrent [New]` → `BitTorrent` |
| Remove dots | `Pump.fun` → `Pumpfun` |
| Remove hyphens | `Non-Playable Coin` → `NonPlayableCoin` |
| Fix Cyrillic chars | `GoМining` → `GoMining` |
| Remove Chinese | `币安人生` → (removed) |

### 5. ENS Suffix
- Append `.eth` to each name

## Sample Output

```
name
Bitcoin.eth
Ethereum.eth
BNB.eth
XRP.eth
TRON.eth
Cardano.eth
BitcoinCash.eth
Chainlink.eth
UNUSSEDLEO.eth
Zcash.eth
```

## Date Processed

2026-01-05

