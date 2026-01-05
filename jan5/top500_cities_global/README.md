# Top 500 Cities by 2025 Population

This directory contains data on the world's largest cities by population, extracted from the UN World Urbanization Prospects 2025.

## Data Source

**United Nations, Department of Economic and Social Affairs, Population Division (2025)**  
World Urbanization Prospects: The 2025 Revision, Online Edition.

- **File**: `WUP2025-F21-DEGURBA-Cities_Pop.xlsx`
- **Description**: Population Residing in Cities with 50,000+ Inhabitants by Degree of Urbanization
- **Download URL**: https://population.un.org/wup/assets/Download/Cities/WUP2025-F21-DEGURBA-Cities_Pop.xlsx
- **Official Download Page**: https://population.un.org/wup/downloads (select "Cities" tab)

## Output

- **File**: `top500_wup2025_degurb_cities_pop2025.csv`
- **Contents**: Top 500 cities ranked by 2025 population
- **Columns**:
  - `city_name`: Original name of the city (from UN data)
  - `pop_2025`: Population in thousands (2025 estimate)
  - `normalized`: Lowercase a-z only version of the city name

## How to Reproduce

### 1. Download the source data

```bash
curl -L -o "WUP2025-F21-DEGURBA-Cities_Pop.xlsx" \
  "https://population.un.org/wup/assets/Download/Cities/WUP2025-F21-DEGURBA-Cities_Pop.xlsx"
```

### 2. Set up Python environment

```bash
python3 -m venv venv
source venv/bin/activate
pip install pandas openpyxl
```

### 3. Run the extraction script

```python
import pandas as pd

path = "WUP2025-F21-DEGURBA-Cities_Pop.xlsx"
xl = pd.ExcelFile(path)
df = xl.parse("Data")

# Extract city name and 2025 population
out = (
    df[["City_Name", "2025"]]
    .rename(columns={"City_Name": "city_name", "2025": "pop_2025"})
    .dropna(subset=["pop_2025"])
)

# Coerce population to numeric
out["pop_2025"] = pd.to_numeric(
    out["pop_2025"].astype(str).str.replace(",", ""), 
    errors="coerce"
)
out = out.dropna(subset=["pop_2025"])

# Get top 500 and save
top500 = out.sort_values("pop_2025", ascending=False).head(500).reset_index(drop=True)
top500.to_csv("top500_wup2025_degurb_cities_pop2025.csv", index=False)

print(top500.head(20))
```

### 4. Normalize city names to a-z

```python
import unicodedata
import re

# Special cases: metro areas with compound names
SPECIAL_CASES = {
    "Sri Jayawardenepura Kotte - Colombo": "colombo",
    "Macau - Zhuhai": "macau",
}

def normalize_to_az(name):
    """
    Normalize city name to lowercase a-z only.
    
    Steps:
    0. Check special cases first
    1. Extract English name from parentheses if present
    2. Replace special characters (Đ → D)
    3. Transliterate diacritics to ASCII via NFD decomposition
    4. Remove everything except a-z
    5. Lowercase
    """
    # Step 0: Special cases
    if name in SPECIAL_CASES:
        return SPECIAL_CASES[name]
    
    # Step 1: Extract parenthetical English name if present
    paren_match = re.search(r'\(([^)]+)\)$', name)
    if paren_match:
        name = paren_match.group(1)
    
    # Step 2: Replace special characters not handled by NFD
    name = name.replace('Đ', 'D').replace('đ', 'd')
    
    # Step 3: NFD decomposition removes diacritics
    name = unicodedata.normalize('NFD', name)
    name = ''.join(c for c in name if unicodedata.category(c) != 'Mn')
    
    # Step 4: Keep only a-z (removes spaces, punctuation, etc.)
    name = re.sub(r'[^a-zA-Z]', '', name)
    
    # Step 5: Lowercase
    return name.lower()

# Add normalized column
top500['normalized'] = top500['city_name'].apply(normalize_to_az)
top500.to_csv("top500_wup2025_degurb_cities_pop2025.csv", index=False)
```

## Verification

The source Excel file contains:
- **Sheet**: "Data"
- **Total cities with 2025 data**: 12,138
- **Column used for city name**: `City_Name`
- **Column used for population**: `2025` (population in thousands)

Top 5 cities should be:

| city_name | pop_2025 | normalized |
|-----------|----------|------------|
| Jakarta | 41913.860 | jakarta |
| Dhaka | 36585.479 | dhaka |
| Tōkyō (Tokyo) | 33412.512 | tokyo |
| New Delhi | 30222.405 | newdelhi |
| Shanghai | 29558.908 | shanghai |

### Normalization examples

| Original | Normalized | Rule Applied |
|----------|------------|--------------|
| São Paulo | saopaulo | Diacritic removal |
| Al-Qahirah (Cairo) | cairo | Parenthetical extraction |
| Đà Nẵng | danang | Đ→D + diacritic removal |
| Xi'an | xian | Apostrophe removal |
| Washington, D.C. | washingtondc | Punctuation removal |
| Sri Jayawardenepura Kotte - Colombo | colombo | Special case |
| Macau - Zhuhai | macau | Special case |

## Date Retrieved

2026-01-02

