# Gamertags

The top 2,000 most commonly used words in gamertags, extracted from 52.2 million gaming usernames across Minecraft, PlayStation, and Xbox.

## Source
- Minecraft usernames: 51.6M
- PlayStation usernames: 357K
- Xbox usernames: 274K
- **Total: 52.2M usernames**

## Processing
1. Usernames segmented using `ekphrasis` (Twitter corpus)
2. Protected gaming terms preserved (fortnite, minecraft, creeper, etc.)
3. Foreign language fragments filtered
4. 3-character terms filtered to whitelist only
5. Frequency counted across all usernames
6. Top 2,000 terms extracted

## Output
- `gamertags.csv`: Top 2,000 single terms with `.eth` suffix
- No header, one name per line
- Example: `king.eth`, `gamer.eth`, `master.eth`

## Date
January 8, 2026

