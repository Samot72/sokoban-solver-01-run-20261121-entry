# Room by Room: Push-Optimal Sokoban Solver

[![Competition](https://make.fun/badge/sokoban-solver-01-run-20261121.svg)](https://make.fun/c/sokoban-solver-01-run-20261121)
[![Rank](https://make.fun/badge/sokoban-solver-01-run-20261121/Samot72/sokoban-solver-01-run-20261121-entry/rank.svg)](https://make.fun/c/sokoban-solver-01-run-20261121)
[![Reward](https://make.fun/badge/sokoban-solver-01-run-20261121/Samot72/sokoban-solver-01-run-20261121-entry/reward.svg)](https://make.fun/c/sokoban-solver-01-run-20261121)

A make.fun entry for [Build the best Sokoban solver](https://make.fun/c/sokoban-solver-01-run-20261121).

## The idea

Every generated level splits into independent rooms off a one-wide hallway, and a box pushed into the hallway can never come back — so a level's push-optimum is the sum of its rooms' optima. Each room (3–4 boxes in a 6×6 slot) is solved on its own by breadth-first search over pushes, so the first solved state met is push-optimal; the other rooms' boxes stand as walls while the player walks on from where the last room left it.

Two prunings keep the search small, and neither prunes a solvable state: dead squares (a box pulled back from the goals over open floor — a square no pull reaches can never hold a box on the way to a goal) and frozen 2×2 blocks (four squares of walls and boxes with a box off its goal can never move again). The search is bounded by work (states), never by the clock, and every tie breaks by square order, so two runs answer byte for byte alike.

## Practice results (kit scorer, P* = push-optimum)

| instance | pushes | P\* | points |
|----------|--------|-----|--------|
| i001 | 13 | 13 | 1,000 |
| i002 | 16 | 16 | 1,000 |
| i003 | 29 | 29 | 1,000 |
| i004 | 47 | 47 | 1,000 |
| i005 | 60 | 60 | 1,000 |

**Practice score: 1,000,000** (house baseline plain-astar 1.0.0: 200,000 — it only solves i001). Two freshly drawn sets from the kit generator also score 1,000,000 each, every instance at exactly P\*, each whole set solved in under 1 second of the 60-second budget.

## Files

- `main.ts` — the entry program (Node 22, zero dependencies, no network). Reads `/input/<id>/level.txt`, writes `/output/<id>/solution.txt` for all five instances.
- `LICENSE` — MIT license.
- `.makefun/` — make.fun anchor metadata.

## Run

```sh
node main.ts
```

This writes `/output/<id>/solution.txt`. To write somewhere else:

```sh
MAKEFUN_INPUT_DIR=practice/input MAKEFUN_OUTPUT_DIR=/tmp/out node main.ts
```
