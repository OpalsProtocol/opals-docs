# Token Launch Mechanics: How Automatic Launch Works

Your token launch on Uniswap happens automatically. No manual steps. No admin intervention. No possibility of error.

This guide explains how the LiquidityLauncher works without diving into code.

<figure><img src="../.gitbook/assets/image (1).png" alt="Token Launcher Interface"><figcaption><p>Total raised is 45 ETH out of a target of 100</p></figcaption></figure>

## The Three Phases

### Phase 1: Accumulation

During your NFT sale, the LiquidityLauncher accumulates resources:

**ETH collection**: Every Patron Card mint sends ETH to the market contract. After fees, ETH goes to LiquidityLauncher.

**Token allocation**: Your Token contract mints total supply. The percentage you allocated for liquidity (typically 40%) is held for Uniswap launch.

**Waiting for threshold**: LiquidityLauncher waits until your sale completes or hits minimum threshold.

No trading possible yet. Everything is accumulating.

### Phase 2: Atomic Launch

When threshold is reached, launch happens in a single transaction:

**Step 1**: LiquidityLauncher receives accumulated ETH

**Step 2**: Token contract transfers LP allocation to LiquidityLauncher

**Step 3**: LiquidityLauncher creates Uniswap V2 pair for your token + ETH

**Step 4**: LiquidityLauncher adds all ETH + all LP tokens as liquidity

**Step 5**: Uniswap mints LP tokens representing the liquidity position

**Step 6**: LiquidityLauncher sends LP tokens to PatronClaim

**Step 7**: PatronClaim locks LP tokens permanently (no withdrawal function)

All steps happen atomically. If any step fails, entire transaction reverts. Either everything succeeds or nothing happens.

### Phase 3: Trading

Once liquidity is added:

**Immediate trading**: Anyone can buy or sell your token on Uniswap

**Price discovery**: Market determines price through supply and demand

**Permanent liquidity**: LP tokens locked forever in PatronClaim

**Automatic rewards**: Supporters can stake Patron Cards to claim rewards

Your token is live. The infrastructure is immutable.

## Initial Price Calculation

Your token's starting price on Uniswap is determined by a simple formula:

**Price = ETH Raised / LP Token Supply**

### Example 1: $100k Raise

**Scenario**: You raised 50 ETH (approximately $100k at $2,000/ETH). You allocated 40% of 1 billion tokens to LP.

**LP token supply**: 400,000,000 tokens

**ETH raised**: 50 ETH

**Initial price**: 50 ETH / 400,000,000 tokens = 0.000000125 ETH per token

**In USD** (at $2,000/ETH): $0.00025 per token

**Market cap at launch**: 1,000,000,000 tokens × $0.00025 = $250,000

### Example 2: $500k Raise

**Scenario**: You raised 250 ETH (approximately $500k). Same 40% LP allocation.

**LP token supply**: 400,000,000 tokens

**ETH raised**: 250 ETH

**Initial price**: 250 ETH / 400,000,000 tokens = 0.000000625 ETH per token

**In USD**: $0.00125 per token

**Market cap at launch**: 1,000,000,000 × $0.00125 = $1,250,000

### Example 3: Different Token Supply

**Scenario**: You raised 100 ETH but only minted 100 million total tokens. 40% to LP still.

**LP token supply**: 40,000,000 tokens

**ETH raised**: 100 ETH

**Initial price**: 100 ETH / 40,000,000 = 0.0000025 ETH per token

**In USD**: $0.005 per token

**Market cap at launch**: 100,000,000 × $0.005 = $500,000

Notice: Smaller supply, higher price per token, similar market cap.

## Liquidity Depth and Price Impact

### What Is Liquidity Depth?

Liquidity depth determines how much someone can buy or sell without moving price significantly.

**Deeper liquidity = smaller price impact**

**Shallower liquidity = larger price impact**

### Example: Deep Liquidity

**Launch state**: 100 ETH + 400M tokens in pool

**Someone buys for 1 ETH**:
- Price impact: Approximately 1%
- They receive tokens at near-initial price
- Pool rebalances slightly

**Someone buys for 10 ETH**:
- Price impact: Approximately 10-12%
- They receive tokens at higher average price
- Pool rebalances significantly

### Example: Shallow Liquidity

**Launch state**: 10 ETH + 400M tokens in pool

**Someone buys for 1 ETH**:
- Price impact: Approximately 10%
- They receive significantly fewer tokens
- Price moves dramatically

**Someone buys for 10 ETH**:
- Price impact: 50%+ (massive slippage)
- They receive far fewer tokens than expected
- Pool becomes imbalanced

**Lesson**: Deeper liquidity creates healthier markets.

## Slippage Protection

The LiquidityLauncher includes automatic slippage protection on initial add.

### How It Works

When adding liquidity, LiquidityLauncher specifies minimum amounts:

**Minimum token amount**: 98% of LP allocation

**Minimum ETH amount**: 98% of accumulated ETH

If Uniswap cannot add at least these amounts, transaction reverts.

### Why This Matters

**Without slippage protection**: Someone could manipulate pool creation by front-running the transaction.

**With slippage protection**: The launch transaction will revert if conditions aren't favorable.

**Result**: Your launch cannot be sandwiched or manipulated.

The 2% tolerance (98% minimums) accounts for minor price movements during transaction confirmation.

## Permanent Liquidity Lock

Once LP tokens go to PatronClaim, they're locked forever.

### How the Lock Works

**PatronClaim has no withdrawal function for LP tokens**. There is no function in the contract that can transfer LP tokens out.

**Patron Card holders receive rewards, not LP tokens**. The LP tokens stay locked. Only reward distributions come out.

**No admin override exists**. Even the project creator cannot withdraw LP tokens.

**No upgrade mechanism exists**. The contracts are immutable. Cannot be changed.

### What This Guarantees

**Liquidity cannot be removed**: Rug pulls are mathematically impossible.

**Price has a floor**: There will always be liquidity to trade against.

**Holders are protected**: Their investments have permanent market depth.

**Trust is unnecessary**: Smart contract enforcement, not promises.

## Weight-Based LP Allocation

While LP tokens stay locked, Patron Card holders earn based on weight.

### How Weight Works

Each Patron Card NFT has a weight. Weight determined by:
- Mint price (higher price = higher weight)
- Position in sale (earlier = higher weight, depending on market type)
- Any bonuses applied

Total weight across all NFTs determines share of LP value.

### Example Distribution

**Project has 100 ETH in LP, 100 Patron Cards minted**:

**Card #1**: Minted at 0.5 ETH, weight = 500
**Card #2**: Minted at 0.6 ETH, weight = 600
**Card #100**: Minted at 1.0 ETH, weight = 1000

**Total weight**: Approximately 70,000 (sum of all cards)

**Card #1's LP allocation**: (500 / 70,000) × 100 ETH = 0.714 ETH worth of LP

**Card #100's LP allocation**: (1000 / 70,000) × 100 ETH = 1.429 ETH worth of LP

Higher contribution gets higher LP share. Fair and transparent.

## PatronPower Multiplier System

LP allocation is just the start. Staking adds multipliers.

### Base Allocation

When you stake your Patron Card NFT:
- You commit to a lock duration (7 days to permanent)
- Your LP allocation becomes "staked LP"
- Multiplier applies based on lock duration

### Multiplier Scale

**7 days**: 0.024x multiplier (minimum)
**30 days**: 0.104x multiplier
**1 year**: 1.25x multiplier
**2 years**: 2.5x multiplier
**4 years**: 5x multiplier
**Permanent**: 10x multiplier (maximum)

### PatronPower Calculation

**PatronPower = LP Allocation × Multiplier**

**Example**:
- Your card allocated 1 ETH worth of LP
- You lock permanently
- Your PatronPower: 1 × 10 = 10

**Compare to short-term holder**:
- Same 1 ETH LP allocation
- They lock 7 days
- Their PatronPower: 1 × 0.024 = 0.024

**You earn 416x more rewards** despite same initial contribution.

## Reward Distribution

Rewards flow based on PatronPower share.

### How Distribution Works

**Project sends reward tokens to PatronClaim**: You transfer tokens periodically.

**PatronClaim calculates shares**: Each staker's PatronPower / Total PatronPower.

**Rewards accumulate**: Each staker can claim their pro-rata share.

**Claiming is permissionless**: Stakers claim whenever they want.

### Example Scenario

**Total PatronPower across all stakers**: 1,000

**Your PatronPower**: 100 (10% of total)

**Project deposits 10,000 reward tokens**:
- Your share: 10% × 10,000 = 1,000 tokens
- You can claim 1,000 tokens

**Next month, project deposits 20,000 tokens**:
- Your share: 10% × 20,000 = 2,000 tokens
- You can claim 2,000 more tokens

**Your total claimable**: 3,000 tokens

As long as your PatronPower percentage stays 10%, you receive 10% of all reward distributions.

## Launch Timing and Triggers

### When Does Launch Happen?

**Scenario 1: Sale completes successfully**
- All Patron Cards sold
- LiquidityLauncher triggers automatically
- Uniswap launch immediate

**Scenario 2: Minimum threshold reached**
- You set a minimum ETH target
- Sale reaches threshold even if not 100% sold
- LiquidityLauncher triggers automatically
- Uniswap launch immediate

**Scenario 3: Time expires with threshold**
- Sale duration ends
- Threshold was reached
- LiquidityLauncher triggers automatically
- Uniswap launch immediate

**Scenario 4: Time expires without threshold**
- Sale duration ends
- Threshold not reached
- Launch does NOT happen
- Supporters reclaim their ETH

### No Manual Steps Required

You don't click "launch". You don't initiate the transaction. The smart contracts handle everything.

**This prevents**:
- Delayed launches
- Manual errors
- Admin manipulation
- Failed launches due to mistakes

**This guarantees**:
- Immediate launch when conditions met
- Atomic execution
- No possibility of partial launch
- Full transparency

## Post-Launch Price Dynamics

### How Price Changes

Once trading begins, price follows supply and demand:

**More buyers than sellers**: Price increases

**More sellers than buyers**: Price decreases

**Equal buying and selling**: Price stable

Your initial launch price is just a starting point. Market decides future price.

### Liquidity Provider Fees

Opals uses a CUSTOM Uniswap V2 fork that charges 1% per swap (not the standard 0.3%). This fee goes to the feeReceiver (Distributor contract) which distributes to PatronClaim and VaultClaim holders based on PatronPower.

**Example**:
- Someone buys $10,000 of your token
- They pay $100 in fees (1% custom fee)
- Fee goes to Distributor contract
- Distributed to PatronClaim/VaultClaim based on PatronPower

**Note**: This is higher than standard Uniswap V2's 0.3% fee, providing more rewards to committed supporters.

Over time, trading fees compound. PatronClaim's LP position grows even without price appreciation.

### Impermanent Loss (or Gain)

LP positions experience impermanent loss when price moves significantly from launch:

**If token price increases dramatically**:
- LP position has less token, more ETH
- Value is less than if you just held tokens
- But LP still gained value, just less than holding

**If token price decreases**:
- LP position has more token, less ETH
- Value is more than if you just held tokens
- LP protects against downside

**If price returns to launch level**:
- "Impermanent loss" disappears
- LP value equals 2x initial ETH value plus fees

**For PatronClaim**: LP tokens stay locked forever. Impermanent loss is permanent. But trading fees accumulate forever too.

## Security Features Built-In

### CEI Pattern (Checks-Effects-Interactions)

LiquidityLauncher follows strict CEI pattern:

**Checks**: Verify threshold met, token approvals correct, Uniswap pair doesn't exist yet

**Effects**: Update internal state, transfer tokens to LiquidityLauncher

**Interactions**: Call Uniswap factory, add liquidity, transfer LP tokens

This prevents reentrancy attacks and state corruption.

### Reentrancy Protection

All state-changing functions use nonReentrant modifier. Even if attacker tries to reenter during launch, transaction reverts.

### Immutable Parameters

Once launch completes:
- LP tokens are locked forever
- Liquidity cannot be removed
- No admin can override
- No upgrade mechanism exists

**These aren't features you enable. They're how the contracts are built.**

## Common Launch Scenarios

### Healthy Launch

**Indicators**:
- Sale completes in 3-7 days
- Threshold reached easily
- Community engaged
- Launch happens smoothly
- Initial price holds or increases

**Post-launch**:
- Steady trading volume
- 60%+ of cards staked
- Average lock duration over 1 year
- Regular reward distributions

### Struggling Launch

**Indicators**:
- Sale takes weeks to hit threshold
- Community quiet
- Minimal marketing
- Launch barely reaches minimum

**Post-launch**:
- Low trading volume
- Less than 30% cards staked
- Short average lock durations
- Irregular rewards

**Recovery strategy**: Increase marketing, deliver on roadmap, engage community, distribute rewards consistently.

### Failed Launch

**Indicators**:
- Time expires before threshold
- No Uniswap launch
- Supporters reclaim ETH

**What happens**:
- All ETH returned to supporters
- No tokens launched
- No liquidity created
- Project can try again with adjusted parameters

**No penalty** for failed launches except lost time and $15 gas.

## Maximizing Launch Success

### Before Launch

**Optimize token allocation**: 40% LP creates good depth. Less risks shallow liquidity.

**Price reasonably**: Don't overprice Patron Cards. Early supporters are your foundation.

**Build community**: 50-100 engaged people is enough. Quality over quantity.

### During Launch

**Communicate constantly**: Daily updates build confidence.

**Answer questions**: Transparency matters more than perfection.

**Create milestones**: Celebrate 25%, 50%, 75% sold.

### After Launch

**Distribute rewards promptly**: First distribution should happen within days.

**Maintain communication**: Post-launch engagement keeps community strong.

**Deliver on roadmap**: Execute what you promised.

## Technical Deep Dive (Optional)

For founders who want technical details:

### Contract Interaction Flow

1. Market contract (SteppedMarket/FixedMarket) collects ETH from mints
2. After fees, ETH accumulates in market contract
3. When threshold reached, anyone can call launch()
4. LiquidityLauncher pulls ETH from market
5. LiquidityLauncher pulls tokens from Token contract
6. LiquidityLauncher calls Uniswap factory.createPair()
7. LiquidityLauncher approves Uniswap router
8. LiquidityLauncher calls router.addLiquidityETH()
9. Uniswap mints LP tokens to LiquidityLauncher
10. LiquidityLauncher transfers LP tokens to PatronClaim
11. PatronClaim records LP allocation by weight
12. Launch complete

### Key Function: addLiquidityETH()

This Uniswap function adds liquidity in one transaction:

**Inputs**:
- Token address
- Token amount
- Minimum token amount (slippage protection)
- Minimum ETH amount (slippage protection)
- LP token recipient (PatronClaim)
- Deadline (prevents stale transactions)

**Outputs**:
- Actual token amount used
- Actual ETH amount used
- LP tokens minted

LiquidityLauncher wraps this in safety checks and CEI pattern.

## Next Steps

Understanding launch mechanics helps you:
- Design better tokenomics
- Set realistic expectations
- Communicate clearly with supporters
- Plan post-launch strategy

**Ready to configure your launch?**

[Choose your market type](./choosing-market-type.md) →

[Plan your economics](./pricing-and-economics.md) →

[View full launch process](./launch-process.md) →

---

**Remember**: The automatic launch system removes human error. Trust the smart contracts. They've been audited, tested, and proven in production.
