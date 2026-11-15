# Tiny Chess 01 — 4 KB chess engine

A compact alpha-beta chess engine in a single `main.py` (Python 3.13,
standard library only, at most 4,096 bytes as committed).

## Design

- **Board:** 0x88, incremental material + piece-square evaluation.
- **Search:** negamax alpha-beta with a transposition table, killer moves,
  history heuristic, null-move pruning and late-move reductions,
  iterative deepening to a **fixed node budget per move** — no clock, no
  unseeded randomness, so a replayed trial plays the same moves.
- **Quiescence:** captures, promotions and all replies to check.
- **Evaluation:** material + piece-square tables, bishop-pair bonus, pawn
  structure (isolated/doubled), tempo, and a separate king table for
  queenless endgames. Repetition is a draw (game history).
- **Protocol:** talks to the env at `MAKEFUN_ENV_URL`
  (`POST /game`, `POST /move`), plays every game of the gauntlet and exits
  when the env reports done.

## Files

- `main.py` — the whole engine, packed by the kit's
  `makefun compress` from the readable source below (4,085 bytes).
- `src.py` — the readable source of `main.py` (kept in the repository
  folder, not committed); the transcript bundle ships it beside the
  sessions, never published.
- `LICENSE` — MIT.
- `.makefun/owner.json` — claim file with the entrant's wallet.
