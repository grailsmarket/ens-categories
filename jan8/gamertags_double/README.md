# Gamertags Double

The top 1,000 most commonly used two-word phrases in gamertags, extracted from 52.2 million gaming usernames across Minecraft, PlayStation, and Xbox.

## Source
- Minecraft usernames: 51.6M
- PlayStation usernames: 357K
- Xbox usernames: 274K
- **Total: 52.2M usernames**

## Processing
1. Usernames segmented using `ekphrasis` (Twitter corpus)
2. Protected gaming terms preserved (fortnite, minecraft, creeper, etc.)
3. 2-word phrases extracted from adjacent segments
4. Grammar filters applied (bad endings, prefix-only rules)
5. Foreign language fragments filtered
6. Phrases with 10+ occurrences kept
7. Top 1,000 phrases extracted
8. Underscores removed for final output

## Output
- `gamertags_double.csv`: Top 1,000 two-word phrases with `.eth` suffix
- No header, one name per line
- Example: `progamer.eth`, `gamergirl.eth`, `dragonslayer.eth`

## Date
January 8, 2026

