# Tokenomics

## Variables
- C: principal capital (USD)
- a: net APR from LP (after IL and costs)
- y: daily yield = C * a / 365
- p: target base pay per player per day (USD), configurable
- S: sustainable players per day = floor(y / p)

## Milestones
- Milestone slots = floor(C / 50,000).
- Active funded players = min(cap, max(S, Milestone slots)) or use milestones as a hard cap for determinism.

## Distribution cadence
- Every N minutes (e.g., 10m), per-player target payout = p * (N / 1440).
- If available yield < target, pay pro-rata; deficit does not touch principal.
- Surplus compounds (minus a small buffer to reduce LP churn).

## Risk notes
- Stable pool risk: depeg/IL → mitigate via conservative allowlist and oracle checks.
- Smart contract risk: audits and staged rollout; freeze upgrades after stabilization.
- Yield volatility: dynamic target protects principal; milestones add predictability.


