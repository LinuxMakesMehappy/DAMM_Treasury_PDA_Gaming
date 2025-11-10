# Perpetual Stable Treasury (Solana) – Docs Only

A non-withdrawable, perpetually compounding stablecoin Treasury PDA that LPs into a whitelisted stablecoin pool and streams only the yield to players. Principal can never be withdrawn; yield scales funded player slots at $50k TVL milestones.

- **No human withdrawals**; principal is locked permanently.
- **Yield only** (LP fees/emissions) is distributed to active players.
- **Scaling**: +1 funded player per $50k TVL milestone; optional cap/rotation.
- **Eligibility**: via staking or owning verified NFTs.
- **Cadence**: harvest and distribute every few minutes via a keeper.

Read next:
- `docs/OVERVIEW.md` – concept and flow
- `docs/TOKENOMICS.md` – economics and math
- `docs/SPEC.md` – program accounts, instructions, and invariants (no code)

## Why this model
- Aligns value with players: sustainable “near minimum wage” target funded by yield.
- Principal compounds, increasing durable yield over time.
- Deterministic scaling via TVL milestones; optional rotation for fairness.

## High-level flow
1. Game/service routes stablecoin fees to the Treasury PDA.
2. Treasury deposits into a whitelisted stablecoin LP pool.
3. Keeper harvests LP fees/emissions every few minutes.
4. Yield is split among active players; surplus compounds; principal remains locked.

## Status
- Design draft for dev review; no code in this repo.
- Implementation targets: Solana (Anchor), stable LPs (e.g., Orca Whirlpool/Meteora).

## Contributing
See `CONTRIBUTING.md`. Open design questions and proposals via Issues/Discussions.

## License
MIT – see `LICENSE`.


