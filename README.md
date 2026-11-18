# tiny-chess

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/agungvg/tiny-chess-4k/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/agungvg/tiny-chess-4k/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A 4 KB Python chess engine for the [make.fun tiny-chess-01 bounty](https://make.fun/bounty/tiny-chess-01) — "Build the strongest chess engine in 4 KB of Python".

## How it plays

`main.py` is the whole engine, packed by the kit's `makefun compress` from the readable `chess.py` beside it. The board is 0x88, so off-board tests are one bitmask. The evaluation is material plus one piece-square table per piece, updated incrementally as moves are made and unmade, with a Zobrist key kept in step for the transposition table and for spotting repeated positions.

The search is negamax alpha-beta with iterative deepening under a fixed 80,000-node budget — no clock, so a position always gets the same move. Moves are ordered by MVV-LVA captures and promotions, the transposition table stores exact, lower and upper bounds so re-searched positions cut off early, and the leaves are extended by a quiescence search over captures, promotions and replies to checks. The engine talks to the gauntlet over HTTP (`MAKEFUN_ENV_URL`): it polls `/game`, reads the FEN and the legal moves it is given, and posts its choice to `/move` until every game is over.

## Files

- `chess.py` — the readable source, written for this entry.
- `main.py` — the packed entrypoint (`makefun compress chess.py --out main.py`), 4,061 bytes.
- `LICENSE` — MIT.

## Practice result

Kit trial-0 at the 60,000-node setting: Elo 1,191 (1 win, 3 draws, 2 losses over 6 games, no engine errors, ~2.9 s a move). The shipped budget was raised to 80,000 nodes after that trial; a full trial at 80,000 nodes was started but stopped early, so the 1,191 figure is the measured one and the 80k setting is unmeasured.
