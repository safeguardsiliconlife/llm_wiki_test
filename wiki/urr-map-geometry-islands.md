---
title: "URR 0.11 Update #57: Map Geometry and Island Prevention"
type: summary
tags: [game-dev, procedural-generation, ultima-ratio-regum, algorithms, map-generation]
created: 2026-04-20
updated: 2026-04-20
sources: [https://www.markrjohnsongames.com/2026/04/11/ultima-ratio-regum-0-11-update-57-interesting-map-geometry-and-mathematics/]
---

# URR 0.11 Update #57: Map Geometry and Island Prevention

Dev blog post by [[Mark R Johnson]] (2026-04-10) documenting how he solved floating-island generation in [[Ultima Ratio Regum]]'s world map clue damage system. A rare under-the-hood post focusing on the problem-solving process rather than design outcomes.

## The Problem

World map clues (paper notes with map fragments) have organic damage applied — the game selects spread-start points and grows damage outward over iterations. This creates rich, varied-looking damage but could produce **floating islands**: regions of undamaged map entirely surrounded by damage, with no connection to the rest of the clue. Suspension-of-disbelief problem: the player character would have no way to know where a floating piece should be positioned.

## Why Flood-Fill Was Rejected

The obvious fix — run a flood-fill connectivity check after each damage addition, reverting if disconnection is detected — was ruled out:
- Flood-fill is computationally expensive, especially at scale
- Hard/Ultra difficulty maps already require multiple discard-and-retry generation attempts
- The check would need to run after every single damage tile addition

## The Solution: [[Anchor Grid Island Prevention]]

A hidden grid of "anchor tiles" — tiles that **can never become damage** — precomputed so that:
1. Every non-edge inner tile is orthogonally or diagonally adjacent to at least one anchor tile
2. All anchor tiles connect back to the outer two rings of the map (which are already immune to the island problem due to a separate existing rule: at most one edge tile can be damaged)

Because anchor tiles can never be damaged, any tile adjacent to one is structurally grounded — it cannot become an isolated island. The check per damage-tile addition is a single lookup: "is this tile an anchor?" — computationally trivial.

## Implementation Details

- **9×9 maps:** 20 hidden grids (9 anchor tiles each is the minimum found; 8 may be possible)
- **7×7 maps:** 16 hidden grids
- **5×5 maps:** 8 hidden grids (only one anchor tile needed, at a corner or edge of the second-outermost ring)
- All grids implemented in all rotations and reflections for variety
- Preference for orthogonal anchor connections over diagonal — orthogonal looks visually cleaner; diagonal connections between map fragments are valid but less appealing
- Cost: ~1/1000th of a second per note generation

## Design Insight

The two outermost tile rings of any map are already immune to island formation (the existing "only one edge tile can be damaged" rule covers this), so anchor tiles only need to serve the inner region and connect back to those outer rings. This insight significantly reduced the required anchor tile count.

## Related
- [[Ultima Ratio Regum]]
- [[Mark R Johnson]]
- [[Anchor Grid Island Prevention]]
