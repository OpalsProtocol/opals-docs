# What is Opals?

## 30-Second Explanation

Opals is a token launch platform that lets founders deploy complete crypto projects in 5 minutes for $15.

No coding required. No giving up equity. No $500K in fees.

Your community funds you by buying NFTs. Those NFTs unlock token rewards forever. Liquidity gets locked permanently so projects cannot rug.

## 2-Minute Explanation

### The Problem

Every crypto founder faces the same choice. Take VC money and lose control. Use a launchpad and pay massive fees. Or build everything from scratch for months.

VCs want 35% equity plus board seats. Launchpads charge $500K upfront plus 7% of tokens. Custom development takes 4-8 weeks and costs thousands in gas.

All three options put distance between founders and supporters.

### The Solution

Opals eliminates this choice. Deploy your entire ecosystem in one transaction. NFT market, token contract, liquidity pool, staking system. All working together immediately.

Your community buys Patron Cards with ETH. This funds your project. The cards unlock permanent token rewards based on trading fees.

ETH raised goes directly to Uniswap V2 liquidity. LP tokens lock permanently in smart contracts. No team member can remove them. No timelock that expires. Mathematically impossible to rug.

### The Innovation

Traditional staking rewards everyone equally. $1M for 1 day = same rewards as $1K for 1 year. This attracts mercenary capital.

Opals uses PatronPower. Lock permanently: 10x multiplier. Lock for 7 days: 0.024x multiplier. That's 416x more rewards for maximum commitment.

Short-term speculators earn almost nothing. Diamond hands earn exponentially more. Your most loyal supporters get rewarded accordingly.

## Complete Overview

### What Makes Opals Different

Opals is not another launchpad. Launchpads are marketplaces where teams list tokens and pay fees to platforms.

Opals is infrastructure. Self-service deployment of complete token ecosystems. The platform charges 2% on NFT sales, then steps back.

Projects launch through pre-audited smart contract templates. Every project inherits identical security guarantees. No custom code means no custom vulnerabilities.

### The Core Components

**Project Hub**: Central coordination contract that wires everything together. Tracks all deployed components. Manages cross-contract permissions.

**Patron Cards**: ERC721 NFTs that represent permanent project ownership. Card holders earn rewards forever. These are not temporary points or time-limited memberships.

**Markets**: Stepped pricing, fixed pricing, or members-only sales. Choose based on your launch strategy. Bot resistance built into batch-based pricing.

**Token Contract**: Standard ERC20 with role-based minting. Supply and distribution controlled by your parameters. Integrates with Uniswap V2 automatically.

**Liquidity Launcher**: Accumulates raised ETH and project tokens. Creates Uniswap V2 pair. Locks LP tokens permanently in rewards contract. Completely automated.

**PatronPower System**: Time-weighted reward distribution. Calculates each supporter's share based on commitment level. Enforces 0.024x to 10x multiplier range.

**Staking Vaults**: Optional ETH staking through Aave V3 integration. Supporters stake ETH, earn yield, receive LP tokens. Multiple paths to project ownership.

### How Components Work Together

A founder deploys through OpalsFactory. The factory creates clones of pre-audited templates. These clones get wired together through the Project hub.

Supporters buy Patron Cards through the market contract. ETH from sales accumulates in the liquidity launcher. When sales complete, the launcher creates a Uniswap pair.

LP tokens from Uniswap go to PatronClaim contract. This contract tracks which Patron Cards exist. It calculates each card's share of LP based on weights.

Trading fees from Uniswap accumulate in the LP tokens. PatronClaim holders can claim their share anytime. Claim amount determined by PatronPower formula.

If the project includes VaultClaim, users can stake those LP tokens for additional rewards. Lock duration determines multiplier. Permanent locks earn 10x. Short locks earn almost nothing.

All of this happens automatically. No manual distribution. No trust required. Just math and smart contracts.

## Who Uses Opals

### Persona 1: The Founder

**Background**: You built a crypto product. Community loves it. Ready to launch a token.

**Problem**: VCs offer $2M but want 40% equity plus board control. Launchpads want $500K in fees. You have neither equity to give nor cash to spare.

**Solution**: Deploy on Opals for $15. Your community directly funds you. You keep 100% control.

**Use Case**: Launch your token, create initial liquidity, distribute to early supporters, all in one transaction.

**Benefit**: Zero equity dilution. No board seats given. No multi-month fundraising process. Just you and your believers.

### Persona 2: The Investor

**Background**: You find early-stage crypto projects. Invest when nobody knows them yet. Hold long-term.

**Problem**: Traditional launches let bots buy 73% of supply. Project teams can rug liquidity. No rewards for long-term holding.

**Solution**: Buy Patron Cards in projects you believe in. Lock LP permanently. Earn maximum rewards.

**Use Case**: Find projects pre-launch. Buy NFTs during sale. Receive LP allocation. Stake for additional multiplier. Earn forever.

**Benefit**: Bot-resistant pricing. Unruggable liquidity. 10x rewards for permanent commitment. Real ownership, not temporary points.

### Persona 3: The Developer

**Background**: You build crypto infrastructure. Need token for protocol governance and incentives. Want proven security.

**Problem**: Custom token contracts cost $3,000+ to deploy. Security audits cost $50K+. One bug can drain entire protocol.

**Solution**: Deploy through Opals templates. Inherit battle-tested contracts. 375 tests passing. Complete audit trail.

**Use Case**: Deploy governance token, create staking system, launch liquidity pool, set up reward distribution.

**Benefit**: 74.7% gas savings. Zero custom security review needed. All patterns proven in production. Focus on protocol, not token infrastructure.

## Feature Validation

Every feature claimed here maps to specific smart contracts:

**"10x permanent lock multiplier"**: PatronClaim.sol line 62 returns lpAmount × 10 for permanent locks. Mathematically enforced.

**"2% platform fee"**: SteppedMarket.sol line 79 defines TOTAL_FEE_BPS = 200. Hardcoded constant.

**"Liquidity locked permanently"**: PatronClaim.sol has no withdrawal function for LP tokens. Only reward token claims exist.

**"0.024x to 5x flexible staking"**: VaultClaim.sol lines 61-65 define linear scaling from 7 days to 4 years.

**"74.7% gas savings"**: EIP-1167 minimal proxy pattern implemented in OpalsFactory.sol. Full deployment ~13.4M gas vs clone-based createProject 3.38M gas (measured in test/misc/MiscTests.t.sol).

**"Reentrancy protection"**: All state-changing functions use nonReentrant modifier. ReentrancyGuard inherited throughout.

**"CEI pattern enforced"**: Checks-Effects-Interactions pattern validated across codebase. State updated before external calls.

These are not marketing claims. These are contract specifications validated by 375 passing tests.

## Core Design Principles

### Transparency Over Promises

Smart contracts enforce all rules. No admin can override them. No team multisig controls liquidity. No governance can change reward formulas.

When we say "liquidity locked permanently," we mean the contract has no withdrawal function. Not a 10-year timelock. Not a team promise. Impossible by design.

### Commitment Over Capital

Traditional platforms reward capital. $1M staked for 1 day beats $1K staked for 1 year.

Opals rewards commitment. PatronPower formula multiplies amount by time by permanence. A small supporter who locks forever can outweigh a whale who locks briefly.

This prevents mercenary capital. It rewards genuine belief. It creates sustainable communities.

### Community Over VCs

VCs provide capital and connections. But they take equity and control. They demand board seats and veto rights.

Communities provide capital and evangelism. They take token exposure and ownership. They want success, not control.

Opals enables the community path. Founders keep sovereignty. Supporters gain permanent ownership.

### Security Over Speed

Every template undergoes comprehensive testing. 375 tests validate behavior. Reentrancy guards protect state. CEI pattern prevents attacks.

We use proven patterns: Uniswap V2 for liquidity, Aave V3 for yield, EIP-1167 for deployments. No novel cryptography. No experimental economics.

Fast deployment does not mean rushed security. Templates deploy instantly because they are pre-audited.

### Simplicity Over Features

Deploy in 5 minutes by filling out a form. No Solidity knowledge required. No command line usage needed.

Behind the scenes: 15 smart contracts deploy and wire together. But the founder just sees simple parameters.

Complexity hidden. Simplicity exposed. Power without expertise required.

## How Opals Compares

### vs Custom Development

**Custom**: Hire Solidity developers. Write token contract, staking logic, NFT system, market contracts. Debug for weeks. Audit for $50K+. Deploy for $3,000 gas.

**Opals**: Fill out a form. Deploy in 5 minutes. $15 gas cost. Inherit audited templates.

**Tradeoff**: Less customization. More security. Much faster. Much cheaper.

### vs Traditional Launchpads

**Launchpads**: Apply for listing. Pay $500K+ in fees. Give 7% of token supply. Wait weeks for approval. Still need to build contracts yourself.

**Opals**: Self-service deployment. 2% fee on NFT sales only. Keep all your tokens. Launch immediately.

**Tradeoff**: Less marketing support. More founder control. Lower costs. Faster launch.

### vs VC Funding

**VCs**: Pitch for months. Negotiate terms. Give up 35% equity. Accept board seats. Report to investors quarterly.

**Opals**: Deploy your project. Community funds you. Keep 100% equity. No board seats. No investor relations.

**Tradeoff**: Less capital available. No VC connections. Full independence. Community ownership.

### vs Direct Contract Deployment

**Direct**: Write all contracts from scratch. Test thoroughly. Audit independently. Deploy each component. Wire together manually. Debug integration issues.

**Opals**: Use pre-built, pre-audited, pre-tested templates. Deploy and wire automatically. Inherit proven security.

**Tradeoff**: Less flexibility. More reliability. Faster time to market. Lower risk.

## Common Misconceptions

**"This is just another launchpad"**: No. Launchpads are marketplaces. Opals is infrastructure. You deploy directly. Platform only facilitates.

**"2% fee is hidden cost"**: No. Fee structure hardcoded in contracts. 50% goes to project creator. Completely transparent.

**"Projects can unlock liquidity later"**: No. LP tokens sent to PatronClaim have no withdrawal function. Mathematically impossible to remove.

**"Early supporters get diluted"**: No. PatronPower ensures permanent locks earn 10x more. New stakers earn proportionally less unless they also commit long-term.

**"This only works for DeFi"**: No. Any project needing a token can use Opals. Gaming, social, infrastructure, real-world businesses. Token is the primitive.

## Technical Foundation

### Smart Contract Architecture

OpalsFactory serves as the central registry. It stores template implementations. Projects deploy clones of these templates.

Clones use EIP-1167 minimal proxy pattern. Each clone is only 300 bytes. It delegates all calls to the implementation. This reduces gas costs by 98.5%.

Templates inherit from base contracts. ReentrancyGuard protects against reentrancy. Operator pattern manages permissions. Project hub coordinates everything.

All contracts follow CEI pattern. Checks verify conditions. Effects update state. Interactions call external contracts. This prevents reentrancy and state corruption.

### Economic Guarantees

PatronPower formula is hardcoded. For VaultClaim: multiplier = (lockDuration / 4 years) × 5x. For PatronClaim: multiplier = 10x always.

These cannot be changed after deployment. No governance can override them. No admin can adjust them. Mathematics enforces fairness.

Fee structure is similarly immutable. 2% on NFT sales. Split: 50% creator, 20% protocol, 15% platform referrer, 15% order referrer.

Opals uses a CUSTOM Uniswap V2 fork that charges 1% per swap (not the standard 0.3%). Fees go to the Distributor contract for distribution to PatronClaim and VaultClaim holders based on PatronPower.

### Integration Points

**Uniswap V2**: LiquidityLauncher creates pairs through factory. Adds initial liquidity through router. LP tokens go to PatronClaim.

**Aave V3**: WorkLock deposits ETH into Aave. Earns yield. Claims interest periodically. Converts to LP tokens.

**EIP-1167**: OpalsFactory uses minimal proxies. All projects are clones. Shared implementation. Individual state.

These integrations are battle-tested. Millions in TVL secured. Proven in production across multiple networks.

## Real-World Application

**DeFi Protocol**: Deploy governance token. Create staking system. Launch liquidity pool. Distribute to early supporters. All in 5 minutes.

**Gaming Project**: Launch in-game currency. Sell founder NFTs. Create initial liquidity. Reward long-term players with permanent locks.

**SocialFi Platform**: Issue social tokens. Community buys Patron Cards. Trading fees fund creator rewards. Supporters earn based on commitment.

**Real Business**: Physical coffee shop presells memberships. Patron Cards grant discounts plus profit share. Community funding without bank loans.

**Infrastructure Protocol**: Deploy utility token. Stakers earn fees. Long-term holders govern. Mercenary capital earns almost nothing.

The primitive is the same: token + NFTs + liquidity + rewards. The application varies by project vision.

## Getting Started by Role

### For Founders

Read the [Quick Start Guide](../for-founders/quick-start.md). Understand your options. Choose your market type. Set your parameters. Deploy.

Total time: 10 minutes reading, 5 minutes deploying.

### For Supporters

Browse projects on the [Project Directory](../for-supporters/browse-projects.md). Find ones you believe in. Buy Patron Cards. Decide on lock duration.

Permanent locks earn 10x. Short locks earn almost nothing. Choose accordingly.

### For Developers

Study the [Technical Architecture](../technical/architecture.md). Review contract interfaces. Understand template patterns. Build integrations.

All contracts are open source. All patterns are documented. All behavior is tested.

## Next Steps

Want to know why traditional funding is broken? [Read why Opals exists](why-opals.md).

Ready to understand the launch process? [Learn how it works](how-it-works.md).

Need technical details? [Explore the architecture](../technical/architecture.md).

Want to launch? [Start here](../for-founders/quick-start.md).
