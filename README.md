# tiny-chess-01 — slim4s

[![make.fun · tiny-chess-01](https://make.fun/badge/tiny-chess-01.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![rank](https://make.fun/badge/tiny-chess-01/AfrizalSek/makefun-tiny-chess-01/rank.svg)](https://make.fun/bounty/tiny-chess-01/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)
[![reward](https://make.fun/badge/tiny-chess-01/AfrizalSek/makefun-tiny-chess-01/reward.svg)](https://make.fun/bounty/tiny-chess-01?utm_source=github&utm_medium=readme&utm_campaign=tiny-chess-01)

A chess engine in 3,291 bytes of Python 3.13 (standard library only),
written for the [make.fun tiny-chess-01 bounty](https://make.fun/bounty/tiny-chess-01):
the strongest engine that fits in 4 KB.

slim4s is slim4e plus one change: a side-to-move tempo bonus (+10) in
the evaluation. Rebuilt fresh from scratch in a new session on 21 Nov
2026 (the first submission was rejected on a missing run record, so the
engine was rewritten in the session that submits it) and re-screened
in one fresh 32-game run.

## How it plays

`main.py` is the kit's `makefun compress` output of the readable
source (`slim4s-source.py`): an LZMA payload exec'd at import. The
engine inside is original code: a 0x88 board, negamax alpha-beta with
fail-soft scores, iterative deepening, a transposition table, killer
moves, late-move reductions (R=1), quiescence search, and an evaluation
of material plus piece-square tables (king on a middlegame table) plus
a pawn shelter bonus for king safety (+8 per own pawn in the three
squares in front of the king), plus the tempo bonus (+10 for the side
to move).

Search is deterministic: a fixed budget of 100,000 nodes per move, no
clock, no randomness — a replay plays the same moves.

## Practice results (local, kit scorer)

slim4e (the entry this replaces):

- Trial 0: Elo 1326 (2W/3D/3L)
- Trial 1: Elo 1253 (2W/2D/4L)
- Trial 2: Elo 1464 (3W/3D/2L)
- **Mean 3 trials: 1347,7** — above the Sunfish 4 KB baseline mean of
  1325 (+22,7), below the ~1450 prize threshold (-102,3), and above
  the 1154 final floor (+193,7)

slim4s screening vs slim4e (10k nodes, one fresh 32-game run,
21 Nov 2026): 15W-14D-3L, Elo +137,0 (90% CI [+28,0, +246,0]).
Full gauntlet not yet run; this entry is submitted on the
screening evidence.

## Size

- `main.py`: 3,291 bytes (limit 4,096)
- Whole repository: under 8,192 bytes, no file over 4,096
- License: MIT
