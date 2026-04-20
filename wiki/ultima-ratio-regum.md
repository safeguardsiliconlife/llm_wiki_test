---
title: Ultima Ratio Regum
type: entity
tags: [game, roguelike, procedural-generation, indie]
created: 2026-04-20
updated: 2026-04-20
sources: [https://www.markrjohnsongames.com/2026/04/11/ultima-ratio-regum-0-11-update-57-interesting-map-geometry-and-mathematics/]
---

# Ultima Ratio Regum

Solo-developed roguelike by [[Mark R Johnson]], notable for extremely deep procedural world generation — cultures, histories, languages, and physical artifacts are all generated. Version 0.11 is in active development as of 2026.

## Map Clue System

World map clues are procedurally damaged paper fragments that players find in-world. Damage is applied organically (multiple spread-start points, iterative growth) at four difficulty tiers: Easy, Normal, Hard, Ultra. Higher difficulties discard more generation attempts that don't meet quality parameters.

Key constraint: clue damage must never produce floating islands — disconnected undamaged regions — as this would break suspension of disbelief. Solved via [[Anchor Grid Island Prevention]].

## Related
- [[Mark R Johnson]]
- [[Anchor Grid Island Prevention]]
- [[URR 0.11 Update #57: Map Geometry and Island Prevention]]
