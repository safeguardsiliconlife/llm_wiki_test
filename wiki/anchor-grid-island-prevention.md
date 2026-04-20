---
title: Anchor Grid Island Prevention
type: concept
tags: [procedural-generation, algorithms, game-dev, map-generation, connectivity]
created: 2026-04-20
updated: 2026-04-20
sources: [https://www.markrjohnsongames.com/2026/04/11/ultima-ratio-regum-0-11-update-57-interesting-map-geometry-and-mathematics/]
---

# Anchor Grid Island Prevention

A technique for guaranteeing topological connectivity in procedural tile-based map generation without runtime connectivity checks. Trades precomputed geometric constraint for zero per-step computational cost at generation time.

## The Problem It Solves

Organic damage/erosion algorithms (start-point spreading) can accidentally create isolated "islands" of tiles — regions entirely surrounded by damaged/removed tiles, disconnected from the rest of the map. Detecting this with flood-fill is expensive and must run after every tile modification.

## The Technique

Precompute a hidden set of **anchor tiles** — tiles that are permanently exempt from damage/removal. These are geometrically arranged so that:

1. **Coverage:** every non-immune inner tile is orthogonally or diagonally adjacent to at least one anchor tile
2. **Connectivity:** all anchor tiles chain back to a structurally immune boundary (e.g., the outer two rings of a map, protected by a separate existing rule)

Because anchors can never be removed, any tile adjacent to one is permanently grounded — it cannot become isolated regardless of what surrounding tiles are removed. The per-tile check during generation reduces to a single lookup: "is this tile an anchor?"

## Geometry Tradeoffs

- **Diagonal anchors** cover more area per tile (closer to √2 spacing vs 1.0 for orthogonal), so require fewer anchor tiles to achieve full coverage
- **Orthogonal anchors** produce visually cleaner results when the anchor pattern influences the generated output's aesthetics
- The outermost tile rings of a bounded grid are typically immune by other rules, so anchors only need to serve the interior and connect to those rings — significantly reducing anchor count

## Sizing (from URR 9×9 implementation)

| Grid | Anchor tiles needed | Hidden grids (with rotations/reflections) |
|------|--------------------|--------------------------------------------|
| 9×9  | ~9 (minimum found) | 20 |
| 7×7  | fewer              | 16 |
| 5×5  | 1                  | 8  |

## When to Use

- Generation algorithm is expensive to restart or revert
- Connectivity violations are rare but catastrophic (suspension of disbelief, gameplay logic)
- Grid dimensions are small enough that a finite set of anchor patterns covers all rotations/reflections
- Per-step runtime cost matters more than design freedom

## Contrast With Flood-Fill

| | Anchor Grid | Flood-Fill |
|---|---|---|
| Per-step cost | O(1) lookup | O(n) traversal |
| Design freedom | Slightly reduced (anchor tiles fixed) | Full |
| Implementation complexity | Precomputation only | Runtime graph traversal |
| Guarantees islands never form | Yes | Yes (with revert) |

## Related
- [[URR 0.11 Update #57: Map Geometry and Island Prevention]]
- [[Ultima Ratio Regum]]
