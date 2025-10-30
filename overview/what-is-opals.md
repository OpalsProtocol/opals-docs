# What is Opals?

Deploy a complete token ecosystem in 5 minutes. Community funds your idea. Early supporters earn for the life of the project. 

## The Three Problems It Solves

### Problem 1: VC Funding Costs

VCs offer capital but take 35% equity + board seats. Your timeline becomes their timeline. You end up with 10-15% of company you built, and their short term goals dont align with your long term vision.

**Opals**: The Community Token Launcher.

### Problem 2: Exchanges Extract Value

Exchanges charge $500K upfront + 10% tokens just to be listed. They provide marketing (a tweet) and community (73% bots). Projects succeed despite the platform, not because of it.

**Opals**: Deploy directly. 2% fee on NFT sales only. Card sales go towards launching your token and funding project treasury.

### Problem 3: Rug Pulls Are Easy

Standard token launches let teams remove liquidity anytime. Timelocks delay rugs (6 months) but don't prevent them. No onchain guarantees exists.

**Opals**: LP tokens locked permanently in PatronClaim contract. No withdrawal function exists, making it impossible to rug.

## How It Works (5 Steps)

1. **Deploy** - Fill out form, pay ~$15 gas, contracts wire automatically
2. **Sell** - Community buys Patron Cards (NFTs) at stepped prices (bot-resistant)
3. **Launch** - Sales end → ETH + tokens → Uniswap pair → LP locks forever
4. **Trade** - Token trades, generates 1% fees (vs 0.3% standard)
5. **Earn** - Supporters claim trading fees based on PatronPower multiplier

## PatronPower: Time Over Capital

**PatronPower = LP Amount × Time Multiplier**

| Lock Duration | Multiplier | Comparison |
|---|---|---|
| 7 days | 0.024x | $1M locked 7 days |
| 1 year | 1.25x | vs |
| Permanent | 10x | **$1K locked permanently = 416x more** |

Short-term speculators earn almost nothing. Diamond hands earn exponentially more. This prevents mercenary capital and creates genuine community.

## The Components

- **Patron Cards** (ERC721): Permanent ownership NFT, entitles you to LP share
- **Market** (Stepped/Fixed/Members): Bot-resistant pricing during sale
- **Token Contract** (ERC20): Your project token, role-based minting
- **Liquidity Launcher**: Accumulates ETH, creates Uniswap V2 pair, locks LP forever
- **PatronClaim**: Tracks card holders, distributes trading fees based on PatronPower
- **VaultClaim**: Optional - stake LP tokens for additional 0-5x multiplier rewards

All pre-audited. 375 passing tests. Proven patterns (Uniswap V2, Aave V3, EIP-1167).

## Comparison

| | Opals | VC | Launchpad | DIY |
|---|---|---|---|---|
| **Cost** | $15 | $0 | $500K+ | $50K+ |
| **Equity loss** | 0% | 35% | 0% | 0% |
| **Control** | 100% | 65% | 100% | 100% |
| **Time to launch** | 1 week | 6 months | 8 weeks | 8 weeks |
| **Rug risk** | Impossible | Low | High | Medium |
| **Gas savings** | 74.7% | - | - | - |

## Design Principles

**Transparency**: Smart contracts enforce all rules. No admin overrides, no multisig, no governance changes. When we say "locked permanently," the contract literally has no withdrawal function.

**Commitment Over Capital**: PatronPower rewards time commitment more than capital size. $1K permanent > $1M for 7 days.

**Community Over VCs**: Communities provide capital + evangelism. They want success, not control. Founders keep sovereignty.

**Security Over Speed**: Pre-audited templates mean instant deployment is also instant security.

## Who Uses Opals

**Founders**: Launch your token, create liquidity, distribute to early supporters, all in 5 minutes. Zero equity dilution. Keep 100% control.

**Investors**: Buy projects early. Permanent lock gives you 10x rewards. Rug-proof liquidity. Real ownership.

**Developers**: Deploy governance token, staking system, liquidity, reward distribution. Inherit audited templates. 74.7% less gas. No custom security review needed.

## Key Numbers

- **$15** deployment cost (vs $500+ custom, $500K+ launchpad)
- **2%** platform fee (50% back to creator)
- **10x** multiplier for permanent locks
- **416x** advantage (permanent vs 7-day lock, same capital)
- **1%** trading fees (vs 0.3% standard Uniswap)
- **375** passing tests
- **74.7%** gas savings (EIP-1167 minimal proxies)

## Common Misconceptions

❌ "Just another launchpad" → No, self-service infrastructure you control completely

❌ "2% fee is hidden" → No, hardcoded in contracts, 50% returns to you

❌ "Founders can unlock liquidity" → No, PatronClaim has zero withdrawal functions

❌ "Early backers get diluted" → No, permanent locks earn 10x more forever

## Next Steps

- **[Why Opals](./why-opals.md)** - Problems + solutions + guarantees
- **[How It Works](./how-it-works.md)** - 4-phase launch journey
- **[For Founders](../for-founders/README.md)** - Launch your token
- **[For Investors](../for-investors/README.md)** - Find & fund projects
- **[Technical](../technical/README.md)** - Architecture & integration
