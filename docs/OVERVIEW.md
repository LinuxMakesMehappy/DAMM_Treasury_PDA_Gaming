# Overview

## Concept
A program-owned Treasury PDA denominated in a stablecoin (e.g., USDC) deposits into a whitelisted stablecoin LP to earn fees/emissions. The **principal is permanently locked**, with **no human withdrawal paths**. Only harvested **yield** is distributed to players.

## Goals
- Provide near minimum-wage equivalent earnings for active players.
- Grow Treasury via fee inflows and compounding LP rewards.
- Scale funded players deterministically: +1 per $50k TVL milestone; optional cap/rotation.

## Flow
1. Fees from a game/service route by CPI into the Treasury PDA.
2. Treasury LPs into an allowlisted stable pool.
3. Keeper harvests every few minutes, sending yield to a rewards vault.
4. Yield is split among active players; leftover compounds; principal never decreases.

## Safety rails
- No general `withdraw` instruction exists.
- Principal floor enforced across all transfers and LP ops.
- Only allowlisted pools; price oracles used for USD TVL calculations.
- Upgrades gated (multisig/timelock) with path to freeze after audit.

## Eligibility
- Stake a specified token OR hold a verified NFT collection.
- Active set determined by TVL milestones, optional cap, and epoch rotation.


