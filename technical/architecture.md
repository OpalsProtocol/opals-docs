# Architecture: LP Allocation and Fee Distribution

Opals creates permanent liquidity through LP token allocation rather than burning. Every participant ends up owning locked liquidity that generates perpetual fee income. This document explains the technical flow from presale to distribution.

## Capital Flow During Presale

When users purchase Patron Cards, the Market contract receives ETH and executes a precise capital split. Eighty percent flows to the Project Treasury for operational runway. Twenty percent accumulates in the Token Launcher for liquidity creation.

The Token Launcher holds both ETH from sales and its token allocation (20% of total supply, or 2e26 tokens). These reserves wait dormant until the funding threshold triggers. No manual intervention required—the smart contract executes automatically when conditions meet.

The Project Treasury receives its 80% token allocation (8e26 tokens) immediately at deployment. These tokens vest to Patron Card holders through the Diamond Claim mechanism, creating aligned incentives through time-locked distribution.

## Liquidity Creation and LP Allocation

At threshold, the Token Launcher pairs its entire token reserve with accumulated ETH on OpalSwap. This creates the initial liquidity pool with mathematical precision—no slippage, no front-running, no manual calculation.

The critical innovation: LP tokens transfer to the PatronClaim contract, not to a burn address. The PatronClaim contract contains no withdrawal function. No admin override. No emergency exit. The liquidity locks permanently through missing functionality rather than time-based promises.

Patron Card holders receive pro-rata allocation of these LP tokens through card-level accounting. Card #42 owns X LP tokens. Sell the card on OpenSea, the new owner inherits the LP allocation automatically. No migration required. The card itself represents liquidity ownership.

This creates tradeable, income-generating assets. Secondary markets price cards based on their LP allocation and accumulated fees. Liquidity ownership becomes liquid itself through NFT transferability.

## WorkLock Interest Mechanism

WorkLock enables risk-free participation through USDC deposits. Users stake USDC, which WorkLock deposits into Aave. The principal remains withdrawable anytime—true liquidity preservation.

Interest accumulates as aUSDC. The protocol splits this interest: 70% converts to LP, 30% flows to Project Treasury as operational runway. This dual-purpose mechanism funds both liquidity depth and project development.

The 70% portion undergoes "zapping"—half swaps for project tokens, creating buy pressure. The remaining ETH pairs with these tokens, forming new LP positions. Every interest harvest deepens liquidity while supporting token price through automated market buying.

These LP tokens lock in the VaultClaim contract, earning the depositor PatronPower based on their contribution. Risk-free principal, productive interest, permanent liquidity creation—aligned incentives through mechanism design.

## VaultClaim and Post-Launch Staking

After launch, users can provide liquidity directly on OpalSwap. They receive LP tokens representing their position. These LP tokens stake in the VaultClaim contract with flexible duration options.

Lock durations range from seven days to permanent. PatronPower multipliers scale with commitment: 1.024x for week-long locks, 10x for permanent stakes. Time preference encoded in smart contracts.

The Open Vested Liquidity mechanism allows early exit with proportional penalties. Need liquidity after one year of a four-year lock? Exit with 37.5% penalty. That penalty redistributes to remaining stakers. Weak hands subsidize diamond hands automatically.

Both PatronClaim and VaultClaim accumulate LP positions over time. PatronClaim through presale allocation. VaultClaim through post-launch staking and WorkLock interest. Different paths, same destination: locked liquidity earning fees.

## Distributor and Fee Distribution

OpalSwap charges 1% on all trades—higher than Uniswap's 0.3%, but this premium funds the entire reward system. Fees accumulate in the Distributor contract, which maintains a real-time ledger of LP ownership across all claims.

The distribution formula operates with mathematical precision:

```
User Share = (User LP Amount / Total System LP) × Accumulated Fees
```

Critical distinction: distribution weights by LP amount, not token holdings. A user with 1,000 LP tokens in VaultClaim earns the same as someone with 1,000 LP tokens in PatronClaim (assuming equal PatronPower multipliers). The system rewards liquidity provision, not token accumulation.

Users claim rewards from their respective contracts. PatronClaim for presale participants. VaultClaim for post-launch stakers. No governance votes determine distribution. No admin can modify allocations. Pure mathematical distribution based on provable on-chain state.

## System Coherence

Every mechanism reinforces the core principle: permanent liquidity with distributed ownership. Presale funds create initial liquidity. WorkLock interest deepens it. Post-launch staking expands it. All participants own pieces of an ever-growing, never-shrinking liquidity pool.

The missing withdrawal functions make this irreversible. Not "locked until governance votes" or "locked until timelock expires." Locked because the unlock function doesn't exist in compiled bytecode. Mathematical certainty through absent functionality.

Fee distribution creates sustainable yield without token inflation. Volume generates fees. Fees flow to LP owners. No minting. No dilution. Honest economics where low volume means low yield, high volume means high yield. The protocol can't lie about its health through inflationary rewards.

---

**Technical Implementation:**

Nine contracts. Atomic deployment. No withdrawal functions. LP tokens allocated, not burned. Distribution by LP ownership, not token weight. This architecture makes rug pulls mathematically impossible while creating sustainable yield for committed participants.