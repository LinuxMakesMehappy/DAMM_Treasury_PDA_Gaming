# Program Specification (no code)

## Accounts
- Config PDA
  - stable_mint, oracle_pubkey, harvest_cadence_sec, target_pay_per_day_usd
  - active_cap, pool_allowlist[], optional collection_mint/stake_mint

- Treasury PDA
  - Holds stablecoin and LP position tokens
  - Tracks `principal_floor` (sum of external inflows − cumulative authorized yield)
  - Enforces non-withdrawal invariant

- Rewards Vault (program-owned ATA)
  - Temporary sink for harvested yield prior to distribution

- Player Registry PDA
  - Entries: { wallet, eligibility_kind (NFT/STAKE), weight_bps, active, last_paid_ts }

- Crank State PDA
  - last_harvest_ts, last_distribution_ts, anti-front-run flags

## Invariants
- No instruction can reduce Treasury below `principal_floor`.
- No generic token transfer from Treasury to arbitrary accounts.
- Only Rewards Vault → player payouts, bounded by available yield.
- LP migrations only within allowlisted pools; must preserve principal floor.

## Instructions (names illustrative)
- initialize_config(params)
- ingest_fee(amount)                   // CPI from game/service
- register_nft(proof) | stake(amount)  // eligibility paths
- update_active_set()                  // milestones/cap/rotation
- lp_deposit(amount)
- harvest_and_distribute()             // keeper-called every few minutes
- set_params(delta)                    // guarded, cannot weaken floor or add withdrawals

## Keeper cadence
- On each call:
  1) Harvest LP fees/emissions to Rewards Vault
  2) Compute active set from TVL and rules
  3) Calculate period payouts vs available yield
  4) Distribute to players; compound surplus; update accounting

## Oracles and USD math
- Use Pyth/Switchboard to value TVL in USD for milestone calculations.
- Maintain small stablecoin buffer (e.g., 0.5–2%) to reduce LP churn.

## Governance & Safety
- Multisig/timelock for parameter changes.
- No upgrade may introduce withdrawals or decrease floor enforcement.
- Recommended path to lock/burn upgrade authority post-audit.


