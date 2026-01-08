# English Most Used Words (NGSL) - ENS Format

## Source
New General Service List (NGSL) 1.2 - a research-based list of the most frequently used words in English, compiled from a 273 million word corpus.

Original source: [newgeneralservicelist.com](https://www.newgeneralservicelist.com/)

## Files

### `NGSL_1.2_stats.csv`
Original source data with columns:
- Lemma (base word form)
- SFI Rank (frequency rank)
- SFI (Standard Frequency Index)
- Adjusted Frequency per Million

### `ngsl_ens.csv`
Cleaned ENS-ready format:
- 2,787 unique entries
- Lowercase only
- No spaces or hyphens
- 3 character minimum
- `.eth` suffix added

## Notes
- Words filtered from original 2,809 to 2,787 (removed entries under 3 characters like "a", "be", "I", "of", "to", etc.)

