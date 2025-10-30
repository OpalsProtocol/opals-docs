# Why Opals Exists

## The Problem

Crypto founders have three broken funding paths:

**Path 1: VC Funding**
- Cost: 35% equity + board seats + quarterly reporting
- Time: 6 months minimum pitch to close
- Outcome: You lose control, optimize for VC exit timeline (7-10 years)

**Path 2: Launchpad Listing**
- Cost: $500K upfront fee + 7% tokens + 20% revenue share
- Approval: 2-8 weeks to get accepted
- Outcome: Access to bot-filled user base, no unique support

**Path 3: Custom Deployment**
- Cost: $3K-50K in gas + developer time
- Build time: 4-8 weeks of custom development
- Risk: Each custom contract needs audit, security review
- Outcome: Could have rug-pull vulnerabilities

All three paths extract value from founders without proportional benefit.

## The Core Issues

### Issue 1: Centralized Control & Dilution

VCs take board seats. They have veto power. Your timeline becomes their timeline. Future rounds bring Series B (20% more dilution), Series C, etc. Founders end up with 10-15% of company they built.

### Issue 2: Intermediary Extraction

Launchpads charge $500K listing fees but provide minimal value (marketing is a tweet, vetting is absent, community is mercenary speculators). They extract fees whether projects succeed or fail.

### Issue 3: Rug Pull Risk

Standard token launches leave liquidity removable. Team adds LP tokens to Uniswap, then withdraws them + community funds. No technical barrier prevents this.

Timelocks (6-month locks) only delay rugs, not prevent them. Trust-based solutions (reputable team, doxxing) are not technical guarantees.

## The Solution: Direct Community Funding

### How Opals Works

1. **Founder deploys** token contracts in 5 minutes, pays ~$15 gas
2. **Community buys** Patron Cards during launch sale (stepped pricing prevents bot advantage)
3. **Liquidity launches** automatically when sale ends (one atomic transaction)
4. **LP tokens lock permanently** in PatronClaim contract (no withdrawal function exists)
5. **Supporters earn forever** - trading fees distributed based on PatronPower

### What Changes

| Aspect | VC | Launchpad | Opals |
|--------|-----|-----------|-------|
| **Founder cost** | $0 upfront | $500K | $15 |
| **Equity/token loss** | 35% | 7% + fees | 0% |
| **Control retained** | 65% | 100% | 100% |
| **Time to launch** | 6 months | 8 weeks | 1 week |
| **Rug risk** | Low (investor pressure) | High | Mathematically impossible |
| **Tech required** | None | Low | None |

### Economic Reality: $2M Raise

**VC path**:
- Give 35% equity ($700K value at exit)
- Pay legal fees ($100K)
- Total cost: $800K+ plus loss of control

**Launchpad path**:
- Listing fee: $500K
- 7% tokens at launch: $140K
- 20% revenue share: $400K
- Total cost: $1.04M

**Opals path**:
- Gas deployment: $15
- 2% platform fee: $40K
- Total cost: $40,015

**Savings**: $760K-$1M, 100% equity retained

## How Opals Guarantees Security

### Permanent Liquidity Lock

PatronClaim.sol contract has **no withdrawal function**. This is not a 6-month timelock that expires. This is not a team promise. This is a mathematical fact verified on-chain.

**Proof**: Read PatronClaim.sol - contains functions to claim tokens, but not to withdraw LP tokens.

**Result**: Rug-pull is cryptographically impossible. Not "very unlikely." Impossible.

### Bot Resistance

Stepped pricing batches cards at fixed price. All cards in batch 1 sell for 0.5 ETH regardless of timing. No MEV exploitation. No speed advantage.

### Immutable Economics

All parameters set at deployment stay locked:
- Token supply (can't inflate)
- Fee structure (can't change)
- Lock multipliers (can't adjust)
- Liquidity split (can't increase your take)

No governance vote can change these. No team can override them.

## PatronPower: Aligning Incentives

### The Mechanism

**PatronPower = LP Amount × Time Multiplier**

| Lock Duration | Multiplier |
|---|---|
| 7 days | 0.024x |
| 1 year | 1.25x |
| Permanent | 10x |

### Why This Matters

Permanent lock earns **416x more** than 7-day lock with same capital.

This means:
- $1K locked permanently > $1M locked 7 days (in PatronPower terms)
- Mercenary capital (short-term speculators) earns almost nothing
- Long-term believers earn disproportionately

This creates community of supporters, not extractors.

### Prevents Dilution

Unlike VC dilution (Series B takes 20%, Series C takes more), PatronPower is fixed from launch. Early supporters never get diluted out. They just earn less if new supporters lock longer.

## Why Now

Crypto solves the capital access problem (anyone can buy tokens). But traditional funding structures haven't adapted.

Opals is the infrastructure for web3 fundraising:
- No permission required (deploy directly)
- No intermediaries (founder ↔ community)
- No compromises (100% equity, 100% control)
- Mathematically secure (code replaces trust)

This is native to crypto. Impossible in web2.

## Next Steps

- **[For Founders](../for-founders/README.md)** - How to launch
- **[For Investors](../for-investors/README.md)** - How to participate
- **[How It Works](./how-it-works.md)** - Technical walkthrough
