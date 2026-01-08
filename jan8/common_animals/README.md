# Common Animals

A curated list of 516 common animal names formatted as ENS names.

## Source

This list is derived from the **Troyer et al. (1997) Animal Category Norms**, an academic dataset from the American Psychological Association (APA). The original source is:

> **"Appendix 1: Animal Categories Extended from the Troyer et al. (1997) Norms"**  
> Source: https://supp.apa.org/psycarticles/supplemental/a0027373/Appendix1.pdf

This dataset represents animals that people commonly think of when asked to name animals - making it ideal for identifying recognizable, culturally significant animal names.

## Data Processing

The original list was processed as follows:

1. Extracted all animals from 22 categories (African, Arctic, Australian, Birds, Fish, Mammals, Reptiles, etc.)
2. Deduplicated across categories
3. Normalized names: lowercase, a-z only, no spaces
4. Added `.eth` suffix for ENS compatibility

## File

### `common_animals.csv`

Single column CSV (no header) containing 516 ENS-formatted animal names.

**Format:** `{animal}.eth`

**Examples:**
```
aardvark.eth
ant.eth
bear.eth
butterfly.eth
...
whale.eth
wolf.eth
zebra.eth
```

## Stats

- **Total entries:** 516
- **Character range:** 3-12 letters (before .eth)
- **Shortest:** `ant.eth`, `bat.eth`, `bee.eth`, `cat.eth`, etc.
- **Longest:** `hippopotamus.eth`

## Verified Names

This list includes 81 verified animal ENS names that are already registered, including:
- Common pets: cat, dog, hamster, rabbit, fish, parrot
- Farm animals: cow, pig, sheep, goat, chicken, horse, donkey
- Wildlife: lion, tiger, bear, wolf, elephant, giraffe, zebra
- Sea life: whale, dolphin, shark, octopus, jellyfish, lobster
- Birds: eagle, owl, penguin, flamingo, peacock, sparrow

