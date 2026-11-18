# tiny-chess-4k

[![make.fun](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/agungvg/tiny-chess-4k/rank.svg)](https://make.fun/bounty/tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/agungvg/tiny-chess-4k/reward.svg)](https://make.fun/bounty/tiny-chess-01)

A 4 KB Python chess engine for the [make.fun tiny-chess-01 bounty](https://make.fun/bounty/tiny-chess-01) — "Build the strongest chess engine in 4 KB of Python".

`main.py` (4,006 bytes) is the whole engine: a 0x88 board, negamax alpha-beta with iterative deepening under a fixed 80,000-node budget, a transposition table, MVV-LVA + killer + history move ordering, quiescence search with delta pruning, null-move pruning, and a tapered piece-square-table evaluation. Python 3.13, standard library only. Deterministic: fixed node count, no clock, no randomness. It plays the gauntlet over HTTP (`MAKEFUN_ENV_URL`), reading the position and legal moves from the environment.

Practice Elo (kit harness, 6 games per trial, 60,000-node budget): trial-0 1,545, trial-1 1,364, trial-2 1,099 — mean 1,336, above the 1,154 entry bar. The house sunfish baseline averages ~1,365 on the same trials.
