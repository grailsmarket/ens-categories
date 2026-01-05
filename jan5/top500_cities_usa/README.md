# Top 500 Cities USA

This directory contains the largest cities in the United States, normalized for ENS name matching.

## Output

- **File**: `top500_cities_usa.csv`
- **Contents**: US cities with normalized names
- **Columns**:
  - `city_name`: Original name of the city
  - `normalized`: Lowercase a-z only version of the city name

- **File**: `top500_cities_usa_ens.txt`
- **Contents**: 476 ENS names (one per line)

## Normalization Process

### Special Cases

Cities with compound names or unusual formatting are mapped to their common English name:

```python
SPECIAL_CASES = {
    # City-County combos
    "Nashville-Davidson": "nashville",
    "Lexington-Fayette": "lexington",
    "Augusta-Richmond County": "augusta",
    "Athens-Clarke County": "athens",
    "Louisville/Jefferson County": "louisville",
    # Parenthetical
    "San Buenaventura (Ventura)": "ventura",
}
```

### Normalization Function

```python
import re

def normalize_to_az(name):
    """
    Normalize city name to lowercase a-z only.
    
    Steps:
    0. Check special cases first
    1. Replace St. with St (no period)
    2. Remove apostrophes and other punctuation
    3. Remove everything except a-z
    4. Lowercase
    """
    # Step 0: Special cases
    if name in SPECIAL_CASES:
        return SPECIAL_CASES[name]
    
    # Step 1: Handle "St." abbreviation
    name = name.replace('St.', 'St')
    
    # Step 2: Remove apostrophes (Lee's → Lees, O'Fallon → OFallon)
    name = name.replace("'", "")
    
    # Step 3: Keep only a-z (removes spaces, hyphens, punctuation, etc.)
    name = re.sub(r'[^a-zA-Z]', '', name)
    
    # Step 4: Lowercase
    return name.lower()
```

### Duplicate Removal

The original list contained 500 cities, but 24 city names appeared multiple times (cities with the same name in different states). 

**Policy**: Keep only the first occurrence of each normalized name.

| City Name | Occurrences | Kept |
|-----------|-------------|------|
| Springfield | 3 | First only |
| Bloomington | 3 | First only |
| Jacksonville | 2 | First only |
| Columbus | 2 | First only |
| Richmond | 2 | First only |
| Kansas City | 2 | First only |
| ... | ... | ... |

**Result**: 500 → 476 unique cities

## Normalization Examples

| Original | Normalized | Rule Applied |
|----------|------------|--------------|
| New York | newyork | Space removal |
| Los Angeles | losangeles | Space removal |
| St. Louis | stlouis | St. → St + punctuation removal |
| St. Petersburg | stpetersburg | St. → St + punctuation removal |
| O'Fallon | ofallon | Apostrophe removal |
| Lee's Summit | leessummit | Apostrophe removal |
| Nashville-Davidson | nashville | Special case |
| San Buenaventura (Ventura) | ventura | Special case |
| Winston-Salem | winstonsalem | Hyphen removal (real city name) |

## Date Processed

2026-01-02

