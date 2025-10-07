# Glossary

A comprehensive guide to Opals terminology. Every technical term is defined with simple explanations and usage examples.

## A

### Aave V3

A decentralized lending protocol. Users deposit assets and earn yield.

Opals integrates Aave for WorkLock vaults. Supporters stake ETH, earn interest, receive LP tokens.

**Related**: WorkLock, Yield

### Access Control

Rules determining who can perform actions. Contracts enforce permissions automatically.

Opals uses three tiers. Project-based permissions for components. Role-based for factory operations. Social layer for community governance.

**Related**: Operator, Admin, Project

### Admin

The highest permission level. Admins can grant operator roles and manage critical settings.

Each project has one admin. Usually the founder. Cannot be changed after deployment in most templates.

**Related**: Operator, Access Control

## B

### Batch Pricing

Selling multiple items at once with price increases per batch. Prevents bot manipulation.

Stepped markets use batch pricing. First 100 cards cost 0.1 ETH each. Next 100 cost 0.15 ETH each.

**Related**: Stepped Market, Bot Resistance

### Believers

Long-term supporters committed to project success. Hold Patron Cards permanently.

PatronPower rewards believers with 10x multiplier. Mercenary capital earns almost nothing.

**Related**: PatronPower, Diamond Hands, Mercenary Capital

### Bot Resistance

Features that prevent automated purchasing. Protects fair distribution.

Batch pricing forces bots to buy entire batches. Makes automated sniping unprofitable.

**Related**: Anti-Gaming, Stepped Market

## C

### Card Set

A group of Patron Cards deployed together. Usually represents one fundraising round.

Projects can have multiple card sets. Each set can have different pricing and benefits.

**Related**: Patron Cards, NFT

### CEI Pattern

Checks-Effects-Interactions programming pattern. Prevents reentrancy attacks.

All Opals contracts follow CEI. Check conditions first. Update state second. Call external contracts last.

**Related**: Reentrancy Protection, Security

### Claim

The act of withdrawing earned rewards. Does not remove original stake.

Supporters claim trading fees from PatronClaim. Claim LP token allocations from completed markets. Claim yield from WorkLock.

**Related**: PatronClaim, VaultClaim

### Clone

A lightweight copy of a contract template. Uses EIP-1167 minimal proxy pattern.

Each project deploys clones. Not full contracts. Saves 98.5% of gas costs.

**Related**: Template Factory, EIP-1167

### Commitment

The decision to lock tokens for a specific duration. Longer commitment earns higher rewards.

Permanent commitment: 10x multiplier. 7-day commitment: 0.024x multiplier.

**Related**: PatronPower, Lock Duration

## D

### Diamond Hands

Supporters who hold permanently and never sell. Highest commitment level.

Diamond hands earn maximum PatronPower. 10x multiplier. 416x more than minimum locks.

**Related**: Believers, Permanent Lock, PatronPower

### DiamondClaim

A claim template with vesting and penalty redistribution. Early exits penalize quitters.

Similar to VaultClaim but designed for token vesting. Penalties go to remaining holders.

**Related**: VaultClaim, OVL, Vesting

### Distributor

A vault template that distributes ETH based on PatronPower. Pro-rata allocation.

Receives protocol fees. Distributes to PatronClaim and VaultClaim holders. Weighted by PatronPower.

**Related**: PatronPower, Vault

## E

### EIP-1167

Ethereum Improvement Proposal 1167. Defines minimal proxy pattern for contract clones.

Opals uses EIP-1167 throughout. Creates 300-byte clones instead of full contracts. Reduces gas from $60 to $15.

**Related**: Template Factory, Clone, Gas Savings

### EIP-712

Ethereum standard for typed structured data signing. Enables gasless transactions.

Opals contracts support EIP-712 signatures. Users can approve actions off-chain. No gas for approvals.

**Related**: Signature, Gasless

### ETH Rewarder

A contract that distributes ETH rewards. Permissionless donation model.

Anyone can deposit ETH for a supporter. Supporter withdraws when ready. No timing restrictions.

**Related**: Rewards, Distributor

## F

### Factory

See Template Factory.

### Fee Structure

The breakdown of platform fees. Opals charges 2% on NFT sales.

Split: 50% project creator, 20% protocol treasury, 15% platform referrer, 15% order referrer.

**Related**: Revenue, Platform Fee

### Fixed Market

A market type with constant pricing. Every NFT costs the same.

Simple and predictable. Less FOMO than stepped pricing. Good for community-first projects.

**Related**: Stepped Market, Members Market, Market Types

## G

### Gas Savings

Reduction in transaction costs through optimization. Opals achieves 74.7% savings.

Full contract deployment: $60 in gas. Opals clone deployment: $15 in gas.

**Related**: EIP-1167, Template Factory

### Gasless

Transactions that don't require the user to pay gas. Enabled by signatures.

EIP-712 signatures allow off-chain approvals. Relayers can submit transactions. User pays no gas.

**Related**: EIP-712, Signature

## I

### Immutable

Cannot be changed after deployment. Critical for security guarantees.

PatronPower formula is immutable. Fee structure is immutable. Liquidity locks are immutable.

**Related**: Security, Unruggable

## L

### Liquidity

Token supply available for trading. Paired with ETH in pools.

Opals projects launch liquidity on Uniswap V2. LP tokens lock permanently in PatronClaim.

**Related**: Liquidity Launcher, LP Tokens, Uniswap V2

### Liquidity Launcher

A contract that accumulates funds and creates Uniswap pairs. Completely automated.

Collects ETH from NFT sales. Receives tokens from project. Creates Uniswap V2 pair. Sends LP tokens to PatronClaim.

**Related**: Uniswap V2, LP Tokens, Automated Launch

### Lock Duration

Time period tokens remain staked. Determines PatronPower multiplier.

Minimum: 7 days (0.024x). Maximum flexible: 4 years (5x). Permanent: forever (10x).

**Related**: PatronPower, Commitment, Staking

### LP Tokens

Liquidity Provider tokens. Represent share of Uniswap pool.

Opals locks LP tokens in PatronClaim. Holders earn trading fees forever. Cannot be removed.

**Related**: Uniswap V2, Liquidity, PatronClaim

## M

### Members Market

A market type requiring membership verification. Gated access.

Only approved members can purchase. Requires approval from project operator.

**Related**: Market Types, Access Control, Gated Sale

### Mercenary Capital

Short-term investors seeking quick profits. Extract value and leave.

PatronPower prevents mercenary capital. 7-day locks earn 0.024x multiplier. Makes quick flips worthless.

**Related**: Believers, PatronPower, Diamond Hands

### Multiplier

A number that increases rewards based on commitment. 0.024x to 10x range.

PatronPower uses multipliers. Permanent locks: 10x. 4-year locks: 5x. 7-day locks: 0.024x.

**Related**: PatronPower, Lock Duration, Rewards

## N

### NFT

Non-Fungible Token. Unique digital asset on blockchain.

Opals uses NFTs for Patron Cards. Each card is an ERC721 token. Represents permanent project ownership.

**Related**: Patron Cards, ERC721

### Nonreentrant

Protection against reentrancy attacks. Prevents recursive calls.

All Opals state-changing functions are nonreentrant. External calls cannot re-enter the function.

**Related**: Reentrancy Protection, CEI Pattern, Security

## O

### Operator

A permission level below admin. Can perform day-to-day operations.

Projects have multiple operators. Cannot change critical settings. Cannot remove admins.

**Related**: Admin, Access Control

### OVL

See Open Vested Liquidity.

### Open Vested Liquidity

A vesting mechanism that allows early exit with penalties. Penalties reward remaining holders.

Exit early: lose (Remaining Time / Total Time) × 50%. Penalty goes to diamond hands.

**Related**: VaultClaim, DiamondClaim, Vesting, Diamond Hands

## P

### Patron Cards

NFTs representing permanent project ownership. Grant lifetime rewards.

Card holders earn LP token allocations. Receive trading fees forever. PatronPower determines share.

**Related**: NFT, PatronPower, PatronClaim

### PatronClaim

A claim template for Patron Card holders. Weight-based LP allocation.

Receives LP tokens from liquidity launcher. Distributes based on card weights. 10x permanent multiplier.

**Related**: Patron Cards, PatronPower, LP Tokens

### PatronPower

The commitment-weighted reward system. Multiplies rewards by lock duration.

Formula: PatronPower = Amount × Multiplier. Multiplier ranges from 0.024x to 10x.

**Related**: Multiplier, Lock Duration, Rewards, Commitment

### Penalty

Amount forfeited for early exit. Redistributed to remaining holders.

OVL penalty: (Remaining Time / Total Time) × 50%. Rewards diamond hands.

**Related**: OVL, Early Exit, Diamond Hands

### Permanent Lock

Locking tokens forever with no exit option. Highest PatronPower.

Earns 10x multiplier. 416x more than 7-day locks. Unruggable commitment.

**Related**: PatronPower, Diamond Hands, Commitment

### Platform Fee

The fee charged by Opals. 2% on NFT sales.

Funds protocol development. 50% goes to project creator. Completely transparent.

**Related**: Fee Structure, Revenue

### Project

The central coordination contract. Wires all components together.

Tracks deployed components. Manages permissions. Coordinates cross-contract operations.

**Related**: Template, Component, Access Control

## R

### Recipe

High-level orchestration contract. Deploys and wires multiple templates.

OpalsRecipe creates complete project ecosystems. One transaction deploys 15+ contracts.

**Related**: Template, Factory, Deployment

### Reentrancy Protection

Security pattern preventing recursive attacks. Locks function during execution.

All Opals contracts use ReentrancyGuard. External calls cannot re-enter functions.

**Related**: Nonreentrant, CEI Pattern, Security

### Rewards

Earnings from participation. Trading fees, yield, token allocations.

Patron Card holders earn trading fees. VaultClaim stakers earn multiplied rewards. WorkLock users earn LP tokens.

**Related**: PatronPower, Claim, Trading Fees

## S

### Signature

Cryptographic proof of authorization. Enables gasless transactions.

EIP-712 signatures prove approval. Users sign off-chain. Relayers submit on-chain.

**Related**: EIP-712, Gasless

### Slippage

Price difference between expected and actual trade. Caused by market movement.

Liquidity launcher includes slippage protection. Transaction reverts if price moves too much.

**Related**: Uniswap V2, Protection

### Sovereign Startup

A project with full founder control. No VC board seats or veto rights.

Opals enables sovereign startups. Founders keep 100% control. Community funds directly.

**Related**: Independence, Control

### Staking

Locking tokens to earn rewards. Duration determines multiplier.

VaultClaim offers flexible staking. 7 days to 4 years or permanent. Longer locks earn more.

**Related**: Lock Duration, PatronPower, VaultClaim

### Stepped Market

A market type with batch pricing. Price increases each batch.

First 100 cards: 0.1 ETH. Next 100: 0.15 ETH. Prevents bot sniping.

**Related**: Batch Pricing, Bot Resistance, Market Types

## T

### Template

A pre-audited smart contract. Projects deploy clones.

Templates are battle-tested. 375 tests passing. All security patterns enforced.

**Related**: Template Factory, Clone, EIP-1167

### Template Factory

The central deployment system. Creates contract clones via EIP-1167.

Reduces gas costs by 74.7%. Each clone is 300 bytes. Delegates to shared implementation.

**Related**: EIP-1167, Clone, Factory

### Trading Fees

Fees from token swaps. Opals uses a CUSTOM Uniswap V2 fork that charges 1% per trade (not the standard 0.3%).

Fee goes to the Distributor contract, which distributes to PatronClaim and VaultClaim holders based on PatronPower. Claimed anytime.

**Related**: Uniswap V2, LP Tokens, Rewards

## U

### Uniswap V2

Decentralized exchange protocol. Automated market maker.

Opals integrates Uniswap V2. Liquidity launcher creates pairs. LP tokens lock in PatronClaim.

**Related**: Liquidity, LP Tokens, Trading Fees

### Unruggable

Mathematically impossible to rug. Not a promise, a guarantee.

LP tokens lock in contracts with no withdrawal function. Cannot be changed. Cannot be overridden.

**Related**: Immutable, Security, Permanent Lock

## V

### Vault

A contract that holds and manages staked assets. Earns yield or distributes rewards.

WorkLock is a vault. Holds ETH. Earns Aave yield. Distributes LP tokens.

**Related**: WorkLock, Staking, Yield

### VaultClaim

A claim template for staked LP tokens. Time-locked with OVL support.

Flexible lock durations. 0.024x to 5x multipliers. Early exit with penalty.

**Related**: Staking, OVL, PatronPower, Lock Duration

### Vesting

Gradual token release over time. Prevents immediate dumps.

DiamondClaim implements vesting. OVL allows early exit with penalties. Rewards patient holders.

**Related**: DiamondClaim, OVL, Time Lock

## W

### Weight

A value determining reward share. Higher weight means larger share.

Patron Cards have weights. PatronPower multiplies weight. Determines LP allocation.

**Related**: PatronPower, Allocation, Share

### WorkLock

A vault template for ETH staking. Integrates Aave V3 for yield.

Stake ETH. Earn Aave interest. Receive LP tokens. Automatic compounding.

**Related**: Vault, Aave V3, Yield, LP Tokens

## Y

### Yield

Earnings from deposited assets. Interest or rewards.

Aave generates yield on ETH. WorkLock claims yield. Converts to LP tokens.

**Related**: Aave V3, WorkLock, Interest
