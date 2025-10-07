# How It Works

## Four-Phase Launch Process

Every Opals launch follows the same pattern. Configure, sell, launch, reward. Four phases that take your project from idea to live token with permanent liquidity.

Each phase maps to specific smart contracts. Everything automated. Nothing manual. Just smart contracts executing agreed rules.

Total time: 5 minutes to deploy. Hours to days for NFT sale. Instant liquidity launch. Perpetual reward distribution.

## Phase 1: Configuration

### What Happens

You configure your project through simple parameters. Token details, market settings, reward structure, liquidity targets.

Behind the scenes, OpalsFactory deploys 5-15 smart contracts. All clones of pre-audited templates. All wired together through Project hub.

This phase takes 5 minutes. No Solidity knowledge required. Just fill out a form. Contracts deploy and configure automatically.

### The Contracts Deployed

**Project Hub** (Project.sol): Central coordination contract. Tracks all components. Manages permissions. Wires everything together.

**Token Contract** (Token.sol): Standard ERC20 with role-based minting. Supply and distribution controlled by configuration.

**Card Contract** (Card.sol): ERC721 NFTs representing project ownership. These are your Patron Cards. Holders earn rewards forever.

**Market Contract**: Either SteppedMarket, FixedMarket, or MembersMarket depending on your choice. This is where supporters buy Patron Cards.

**PatronClaim** (PatronClaim.sol): Receives LP tokens from launch. Distributes them to Card holders based on weights. Calculates rewards.

**Liquidity Launcher** (LiquidityLauncher.sol): Accumulates ETH from sales. Creates Uniswap pair. Locks LP tokens in PatronClaim.

Optional contracts based on configuration:
- **VaultClaim**: Time-locked staking with PatronPower multipliers
- **WorkLock**: ETH staking through Aave V3 for yield
- **Distributor**: Direct ETH distribution to supporters
- **EthRewarder**: Protocol fee collection and distribution

### Key Configuration Decisions

**Token Supply**: How many tokens total? Common: 1 billion (1e27 in contract terms).

**Card Supply**: How many Patron Cards to mint? This determines funding denominator. Common: 1,000 to 10,000.

**Market Type**:
- Stepped: Batch-based pricing. Price increases per package. Bot-resistant.
- Fixed: Same price for all cards. Simpler but less bot protection.
- Members: Requires existing membership NFT. Restricted to specific community.

**Pricing Strategy**:
- Low initial price, high increments: Gradual FOMO building
- High initial price, low increments: Quality filtering
- Fixed price: Maximum simplicity

**Treasury Allocation**: What percentage of raised ETH goes to team vs liquidity? Common: 30% treasury, 70% liquidity.

**Card Weights**: Do all cards have equal weight? Or do early buyers get bonuses? This affects LP distribution.

### Technical Mapping

Configuration parameters map to contract initialization:

`tokenSupply` → Token.sol: Sets `totalSupply` in constructor

`cardSupply` → Card.sol: Sets `maxSupply` for NFT minting

`startingPrice, priceIncrement` → SteppedMarket.sol: Defines pricing curve

`treasuryPercent` → LiquidityLauncher.sol: Determines ETH split on launch

`baseWeight, bonusWeights` → PatronClaim.sol: Configures LP distribution formula

These values are immutable after deployment. Choose carefully. Cannot change later.

## Phase 2: NFT Sale

### What Happens

Your market goes live. Supporters can buy Patron Cards. ETH from sales accumulates in contracts.

Sale continues until target reached or timeout expires. No manual intervention required. Contracts handle everything.

Duration varies by project. Fast sales: 6 hours. Typical sales: 2-3 days. Maximum: set in configuration.

### The Purchase Flow

Supporter visits market contract. Calls `mint()` function. Sends ETH equal to current price.

Market contract executes:

**Check**: Verify payment amount matches price. Verify supply not exceeded. Verify wallet limits if configured.

**Effect**: Mint NFT to supporter address. Update `totalSold` counter. Calculate and accumulate fees.

**Interaction**: Send fees to recipients (creator, protocol, referrers). Emit `Minted` event.

This follows CEI pattern. State updated before external calls. Reentrancy protection active. Safe by design.

### Fee Distribution

2% fee on every sale. Split four ways immediately:

**Project Creator** (50% of fee): Sent to project's designated treasury address. Available immediately.

**Protocol** (20% of fee): Sent to Opals protocol. Funds ongoing development and security.

**Platform Referrer** (15% of fee): Sent to whoever referred the project to Opals. Zero if no referrer.

**Order Referrer** (15% of fee): Sent to whoever referred this specific supporter. Zero if direct purchase.

These transfers happen atomically in the same transaction. No manual claims needed. Everything automatic.

### Market Type Differences

**Stepped Market** (SteppedMarket.sol):

Price = `startingPrice + (packageId × priceIncrement)`

Package ID = `totalSold / itemsPerPackage`

Example: Start at 0.1 ETH, increment 0.01 ETH per 100 cards. First 100 cost 0.1. Next 100 cost 0.11. Creates gradual FOMO.

Bot resistance: All purchases in same package pay same price. No first-mover advantage within batch.

**Fixed Market** (FixedMarket.sol):

Price = `fixedPrice` for all cards.

Simpler to understand. Easier to explain. Less bot protection.

Good for projects prioritizing simplicity over bot resistance.

**Members Market** (MembersMarket.sol):

Requires ownership of specific NFT collection. Verifies ownership before allowing purchase.

Good for existing communities. Rewards current members. Creates exclusivity.

### Technical Details

Market contracts inherit from ReentrancyGuard. Every state-changing function has `nonReentrant` modifier.

Fee calculation uses basis points: `feeAmount = (price × TOTAL_FEE_BPS) / 10000`. Where `TOTAL_FEE_BPS = 200` (2%).

Fee splits are constants: `TOKEN_CREATOR_FEE_BPS = 5000` (50% of fee), etc. Hardcoded. Cannot change.

Slippage protection on market interactions. Excess ETH refunded. Insufficient ETH reverts. No edge case losses.

## Phase 3: Token Launch

### What Happens

NFT sale completes. Liquidity Launcher activates. Creates Uniswap V2 pair. Adds initial liquidity. Locks LP tokens.

This happens in a single transaction. Atomic operation. Either everything succeeds or everything reverts. No partial states.

Result: Trading goes live instantly. Initial price determined by raise amount. LP tokens locked in PatronClaim forever.

### The Launch Sequence

LiquidityLauncher.sol `launch()` function executes the following steps:

**Step 1: Split Raised ETH**

Total ETH from sales divided based on treasury percentage.

Example: $2M raised, 30% treasury
- $600K → Project treasury address
- $1.4M → Remains for liquidity

**Step 2: Calculate Token Allocation**

Token supply allocated to liquidity based on configuration.

Example: 1B total supply, 50% to liquidity
- 500M tokens → Liquidity pool
- 500M tokens → Remain in token contract for other distributions

**Step 3: Create Uniswap Pair**

Call `IUniswapV2Factory(factory).createPair(token, WETH)`

This creates the trading pair. Returns pair address. Stores for future reference.

If pair already exists, uses existing pair address. Idempotent operation.

**Step 4: Approve Router**

`Token.approve(router, tokenAmount)` and `WETH.approve(router, ethAmount)`

Allows Uniswap router to transfer tokens and ETH for liquidity addition.

**Step 5: Add Liquidity**

```
IUniswapV2Router02(router).addLiquidityETH{value: ethAmount}(
    tokenAddress,
    tokenAmount,
    minTokenAmount,  // 98% of tokenAmount (2% slippage protection)
    minETHAmount,    // 98% of ethAmount (2% slippage protection)
    address(this),   // LP tokens sent to this contract
    deadline
)
```

Slippage protection prevents sandwich attacks. 2% tolerance hardcoded.

LP tokens minted to LiquidityLauncher contract.

**Step 6: Transfer LP Tokens**

`lpPair.transfer(patronClaim, lpBalance)`

All LP tokens sent to PatronClaim contract. PatronClaim has no withdrawal function. Locked forever.

**Step 7: Initialize PatronClaim**

PatronClaim.setLPToken(lpPairAddress) registers the LP token address.

PatronClaim.notifyLPReceived() calculates LP per card based on weights.

### Initial Price Calculation

Price = ETH in pool / Tokens in pool

Example: 1.4M ETH, 500M tokens
- Price = 1,400,000 / 500,000,000 = 0.0000028 ETH per token
- Or $2.80 per 1,000 tokens at $1,000 ETH

This is the market-clearing price. Fair by definition. Determined by actual raise, not arbitrary choice.

### Technical Mapping

This entire sequence maps to LiquidityLauncher.sol lines 38-106:

Lines 70-72: Create pair via factory
Lines 74-77: Approve router for token and ETH transfers
Lines 79-89: Add liquidity with slippage protection
Lines 92-102: Transfer LP tokens to PatronClaim and initialize

All in one transaction. All CEI pattern compliant. All reentrancy protected.

## Phase 4: Rewards

### What Happens

Trading begins on Opals' custom Uniswap V2 fork. Each swap charges 1% fee (not the standard 0.3%). Fees go to the Distributor contract for PatronPower-weighted distribution.

Patron Card holders can claim their share of accumulated rewards based on their PatronPower anytime.

This phase is perpetual. As long as trading continues, rewards accumulate. As long as cards exist, holders can claim.

### LP Token Ownership Structure

LP tokens locked in PatronClaim contract. PatronClaim tracks which cards exist and their weights.

When a card holder claims, contract calculates:
1. Total LP tokens held by PatronClaim
2. Card's share based on weight (card weight / total weight)
3. Rewards accumulated in that LP share
4. Transfer rewards to card holder

The LP tokens themselves never leave PatronClaim. Only the rewards from those LP tokens get claimed.

### Weight-Based Distribution

Not all cards are equal. Early supporters can get bonus weights. Founders can get special weights.

Example configuration:
- Base weight: 100 per card
- First 100 cards: +50 bonus weight (150 total)
- Next 900 cards: No bonus (100 total)
- Total weight: (100 × 150) + (900 × 100) = 105,000

Card 1 LP share: 150 / 105,000 = 0.143%
Card 500 LP share: 100 / 105,000 = 0.095%

Early supporter gets 50% more LP allocation for same purchase price. Reward for early belief.

### Reward Accumulation Math

Uniswap V2 LP tokens automatically accumulate trading fees. No claiming needed at Uniswap level.

As trading happens:
- Swap of $10,000: 1% fee = $100 (custom Uniswap V2 fork, not standard 0.3%)
- Fee goes to Distributor contract
- Distributor distributes to PatronClaim/VaultClaim based on PatronPower
- Card holders can claim their share based on PatronPower

Contract uses accumulator pattern for efficient calculations. Tracks rewards per weight instead of per card. Gas-efficient even with 10,000 cards.

### The Claim Process

Card holder calls `PatronClaim.claimTokensForNFTs([cardId])`

Contract executes:

**Step 1: Calculate LP Share**

`lpShare = (cardWeight / totalWeight) × totalLPTokens`

**Step 2: Determine Rewards**

Query Uniswap pair for current reserves. Calculate card's share of both tokens.

Rewards = Token0 amount + Token1 amount (in this case: Project Token + ETH)

**Step 3: Remove Liquidity**

`IUniswapV2Pair(pair).removeLiquidity()` but only for this card's calculated share.

Proportional amounts of both tokens received.

**Step 4: Transfer to Holder**

Send both tokens to card holder address. Update accounting. Emit claim event.

This is safe because only the accumulated rewards get claimed. The base LP position remains locked in PatronClaim.

### Optional: Staking for Multipliers

If project includes VaultClaim, holders can stake their LP tokens for additional multiplier.

Lock LP in VaultClaim → Choose duration → Earn PatronPower multiplier

**7 days**: 0.024x multiplier (almost nothing)
**1 year**: 1.25x multiplier (25% bonus)
**4 years**: 5x multiplier (500% bonus)
**Permanent**: 10x multiplier (1,000% bonus)

This creates second layer of commitment rewards. Already own LP from cards. Lock that LP for even more rewards.

Formula: `multiplier = (lockDuration / 4 years) × 5x` capped at 5x, or 10x for permanent.

Early exit possible through OVL system: `penalty = (remainingTime / totalTime) × 50%`

Penalties redistribute to remaining stakers. Flexibility exists but commitment wins.

### Technical Mapping

PatronClaim.sol implements this:

Lines 158-246: Weight system and LP calculation
Lines 640-667: getNFTTotalLPTokens() calculates per-card LP allocation
Lines 248-288: claimTokensForNFTs() executes the claim process

VaultClaim.sol implements staking:

Lines 61-65: Defines multiplier constants and ranges
Lines 564-605: getPatronPower() calculates multiplier based on duration
Lines 401-480: earlyExit() handles OVL penalty calculation and redistribution

## Contract Interaction Flow

### The Complete Picture

1. **Configuration**: OpalsFactory deploys Project, Token, Card, Market, PatronClaim, LiquidityLauncher
2. **Sale**: Supporters buy Cards through Market. ETH accumulates. Fees distribute automatically.
3. **Launch**: LiquidityLauncher creates Uniswap pair, adds liquidity, locks LP in PatronClaim
4. **Rewards**: Trading fees accumulate. Card holders claim via PatronClaim. Optional staking in VaultClaim.

Each phase depends on the previous. Cannot launch before sale completes. Cannot claim before launch happens. Sequential, automated, trustless.

### Permission Structure

Project hub controls everything through Operator pattern.

Market can mint Cards: `Card.setOperator(market, true)`

LiquidityLauncher can mint Tokens: `Token.grantRole(MINTER_ROLE, launcher)`

PatronClaim can transfer LP: `Project.setOperator(patronClaim, true)`

These permissions set during deployment. Immutable after initialization. Security through simplicity.

### State Transitions

Market state: Active → Completed
- Active: Can mint cards, accumulate ETH
- Completed: Cannot mint, ready for launch

Launcher state: Pending → Launched
- Pending: Accumulating tokens and ETH
- Launched: LP created, tokens locked, cannot launch again

PatronClaim state: Uninitialized → Initialized → Active
- Uninitialized: No LP token set
- Initialized: LP token registered, awaiting LP transfer
- Active: LP received, claims enabled

Vault state: Open → Locked → Unlocked → Claimed
- Open: Can stake
- Locked: Staking active, cannot unstake before expiry
- Unlocked: Can unstake without penalty
- Claimed: Rewards distributed

These states enforce correct sequencing. Cannot skip steps. Cannot repeat operations. Idempotent where safe, restrictive where necessary.

## Gas Costs Breakdown

### Deployment Phase

OpalsFactory uses EIP-1167 minimal proxies. Each clone is ~300 bytes. Each component deployment: ~300K gas.

Full project with 6 components: ~1.8M gas total.

At 50 gwei and $2,000 ETH: ~$15 total cost.

Compare to full deployments: Each component ~3M gas. Full project: ~18M gas. At same prices: ~$1,800 cost.

Savings: 74.7% through template pattern.

### Sale Phase

Each mint: ~100K gas. At 50 gwei: ~$10 per card.

Supporter pays this gas. Not project team. Cost scales with engagement, not with team.

### Launch Phase

Single transaction: ~500K gas. At 50 gwei: ~$50.

Creates pair, adds liquidity, locks LP. All atomic. Team or supporter can trigger.

### Claim Phase

Each claim: ~200K gas. At 50 gwei: ~$20.

Claimant pays. Not project. Only pays when claiming rewards. Optional timing.

### Total Project Cost

Deployment: $15
Launch: $50
Total: $65 for complete project

Compare to custom development: $3,000+ gas plus developer time.

## Success Criteria

### Metrics to Track

**Sale Phase**:
- Cards sold / Total supply
- ETH raised / Target amount
- Time elapsed / Time limit
- Average price paid
- Unique supporters

**Launch Phase**:
- Initial price achieved
- Liquidity depth
- LP tokens locked amount
- Treasury amount received

**Reward Phase**:
- Trading volume
- Fee generation
- Claims processed
- LP value appreciation
- Average lock duration (if VaultClaim)

### What Good Looks Like

**Fast Sale**: Target reached in hours to days, not weeks. Indicates strong demand.

**Wide Distribution**: Many unique wallets, not few whales. Indicates real community.

**Sustained Trading**: Volume continues post-launch. Indicates real utility, not just speculation.

**Long Locks**: High percentage choosing permanent or long-duration locks. Indicates genuine belief.

**Low Early Exits**: Minimal OVL penalty claims. Indicates aligned supporters.

These metrics are all on-chain. Verifiable. Transparent. No trust required to confirm success.

## Common Issues and Solutions

**Issue**: Sale completes but launch never happens.

**Solution**: Anyone can call `launch()` after sale completes. Permissionless. If team disappears, community can still launch.

**Issue**: Not enough liquidity raised.

**Solution**: Set minimum raise in configuration. Sale reverts if minimum not reached. Supporters refunded automatically.

**Issue**: Card weights misconfigured.

**Solution**: Weights set at deployment. Cannot change. Choose carefully. Test with small deployment first.

**Issue**: Rewards not accumulating.

**Solution**: Rewards come from trading. No trading = no rewards. This is expected. Not a bug.

**Issue**: Cannot unstake from VaultClaim.

**Solution**: Check lock expiry. Early exit requires penalty. After expiry, unstake freely.

## Next Steps

Want to launch your own project? [Read the founder's guide](../for-founders/quick-start.md).

Want to understand the economic model? [Learn about PatronPower](../core-concepts/patronpower.md).

Want technical details? [Explore the architecture](../technical/architecture.md).

Still have questions? [Read the FAQ](../help/faq.md).
