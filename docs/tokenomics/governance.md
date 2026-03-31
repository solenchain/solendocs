# Governance

Token holders participate in on-chain governance by voting with their staked tokens.

## Parameters

| Parameter | Value |
|-----------|-------|
| Quorum | 30% of staked supply must participate |
| Pass threshold | 66.67% supermajority |
| Voting period | 14 days (configurable in genesis) |
| Timelock | 3 epochs after passing before execution |

The voting period is set per-network in the genesis config (`governance_voting_period` in epochs). Testnet uses 14 epochs (~46 min) for fast testing. Mainnet will use ~604,800 epochs (~14 days at 2s blocks).

## Proposal Lifecycle

1. **Submission** — Any staked account can submit a proposal
2. **Voting** — Stakers vote yes/no for the voting period
3. **Tallying** — Quorum and supermajority thresholds checked
4. **Timelock** — Passed proposals wait 3 epochs before execution
5. **Execution** — Proposal is applied automatically

## What Governance Can Change

- Base fee per gas
- Burn rate
- Block time
- Epoch rewards
- Staking parameters (minimum stake, unbonding period)
- Rollup registration
- Emergency pause/resume

## What Governance Cannot Change

These require a hard fork:

- Total supply cap
- Vesting schedules for already-allocated tokens
- Consensus mechanism

## Emergency Actions

Governance can perform emergency pause/resume of the network. This requires the same quorum and supermajority but may have an expedited voting period.

## System Contracts

Governance is implemented as a [system contract](../architecture/overview.md) with privileged access. The governance contract manages:

- Proposal storage and lifecycle
- Vote tallying and threshold checking
- Timelock enforcement
- Parameter update execution
