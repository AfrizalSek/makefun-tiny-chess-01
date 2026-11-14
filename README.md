# tiny-chess-01 — slim4e

A chess engine in 4,092 bytes of Python 3.13 (standard library only),
written for the make.fun tiny-chess-01 bounty: the strongest engine that
fits in 4 KB.

## How it plays

`main.py` unpacks an LZMA payload (base85) and execs it. The engine
inside is original code: a 0x88 board, negamax alpha-beta with
fail-soft scores, iterative deepening, a transposition table, killer
moves, late-move reductions (R=1), quiescence search, and an evaluation
of material plus piece-square tables (king on a middlegame table) plus
a pawn shelter bonus for king safety (+8 per own pawn in the three
squares in front of the king).

Search is deterministic: a fixed budget of 100,000 nodes per move, no
clock, no randomness — a replay plays the same moves.

## Practice results (local, kit scorer)

- Trial 0: Elo 1326 (2W/3D/3L)
- Trial 1: Elo 1253 (2W/2D/4L)
- Trial 2: Elo 1464 (3W/3D/2L)
- **Mean 3 trials: 1347,7** — above the Sunfish 4 KB baseline mean of
  1325 (+22,7), below the ~1450 prize threshold (-102,3), and above
  the 1154 final floor (+193,7)

## Size

- `main.py`: 4,092 bytes (limit 4,096)
- Whole repository: under 8,192 bytes, no file over 4,096
- License: MIT
