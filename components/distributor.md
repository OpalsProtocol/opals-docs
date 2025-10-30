# Distributor

The Distributor is the fee engine. It collects 1% from every trade and distributes rewards based on PatronPower.

This is how Opals creates real, sustainable value for supporters: through revenue, not speculation.

## Ingredient 1: Fee Collection

Trading generates fees. Opals captures them automatically.

**Fee sources**:
- Every swap on Uniswap pair: 1% fee captured
- Collected in Distributor contract automatically
- Accumulates continuously

**Example**: Project with $10M daily volume
- $10M × 1% = $100k per day in fees
- $3M per month
- $36M per year
- Distributed to Patron Card holders

**Fee flow**:
1. User swaps 100 ETH for TOKEN on Uniswap
2. 1 ETH fee captured → Distributor contract
3. Contract accumulates ETH
4. Holders can claim their share anytime

## Ingredient 2: PatronPower-Based Distribution

Rewards scale with commitment, not just investment size.

**Distribution formula**:
```
Your reward share = Your PatronPower / Total PatronPower

Example:
- Total PatronPower across project: 1,000,000
- Your PatronPower: 10,000 (1% of total)
- Monthly fees: $300k
- Your share: $3,000/month
```

**PatronPower calculation**:
- Permanent lock (Patron Card): 10x multiplier
- 2-year lock: 5x multiplier
- 1-year lock: 3.75x multiplier
- 30-day lock: 0.2x multiplier

**Real example**: 10,000 Patron Cards, $100k monthly fees

Card A holder (permanent lock):
- 1 card = 60k tokens × 10 = 600k PatronPower
- Share: 600k / 1M total = 0.6%
- Monthly reward: 600 (0.6% × $100k)

Card B holder (1-year lock):
- 1 card = 60k tokens × 3.75 = 225k PatronPower
- Share: 225k / 1M total = 0.225%
- Monthly reward: 225 (0.225% × $100k)

Difference: Permanent lock holder earns 2.67x more despite same capital.

## Ingredient 3: Continuous Accumulation

Rewards accumulate automatically. No claiming required to earn.

**How accumulation works**:
- Fees flow into Distributor daily/hourly
- Smart contract tracks your claimable balance
- Balance grows automatically
- You claim whenever convenient

**Example timeline**: Holder with 1% PatronPower

- Month 1: $1,000 accumulated
- Month 2: $2,000 total (can claim)
- Month 3: $3,000 total
- Claim at month 3: Receive full $3,000

**Claiming mechanics**:
- Call `claimRewards()` on Distributor
- Receives all accumulated ETH/tokens
- Balance resets to 0
- No time limit (rewards don't expire)

## Recipe: Distribution Scenarios

### Scenario 1: Early Supporter (Permanent Lock)

**Position**: 1 Patron Card, permanent lock
- PatronPower: 600k
- Monthly allocation: 0.6% of fees

**Project success**: $5M monthly volume = $50k fees
- Monthly reward: 0.6% × $50k = $300/month
- Annual: $3,600

**Project mega-success**: $50M monthly volume = $500k fees
- Monthly reward: 0.6% × $500k = $3,000/month
- Annual: $36,000

Result: Revenue scales with project success, not reinvestment.

### Scenario 2: Gradual Staker (Multiple Locks)

**Position**:
- 1 Patron Card permanent: 600k PatronPower
- 2 Cards locked 1 year: 450k PatronPower
- Total: 1,050k PatronPower

**On moderate project** ($20M volume = $200k fees):
- Share: 1,050k / (larger pool) ~0.9%
- Monthly: ~$1,800

**Key insight**: Diversification + long locks = steady revenue

### Scenario 3: Short-Term Trader (30-day Locks)

**Position**: 10 Patron Cards, 30-day locks
- PatronPower per card: 60k × 0.2 = 12k
- Total: 120k PatronPower

**On same $200k monthly fees**:
- Share: 120k / (larger pool) ~0.1%
- Monthly: ~$200

Result: Short-term commitment earns 1/10th as much as permanent lock holders.

## Technical Implementation

### Distributor Contract

**Key state**:
- `accumulatedFees`: Total ETH collected so far
- `userBalance[address]`: How much each holder can claim
- `totalPatronPower`: Sum of all PatronPower in system
- `lastDistribution`: Timestamp of last distribution

**Key functions**:

`depositFees(uint amount)`:
- Called by market contracts when fees collected
- Records amount in accumulatedFees
- Triggers distribution if threshold met

`updatePatronPower(address holder, uint newPower)`:
- Called by staking contracts when positions change
- Updates totalPatronPower
- Recalculates distribution shares

`claimableBalance(address holder) -> uint`:
- Returns: holder's current accumulated fees
- Formula: (holderPatronPower / totalPatronPower) × accumulatedFees
- Updated in real-time as fees arrive

`claim() -> uint`:
- Transfers claimable balance to holder
- Resets userBalance to 0
- Returns amount transferred

### Accumulator Pattern

Opals uses an efficient "accumulator" pattern to distribute fees.

**Traditional approach** (inefficient):
- On each fee: Calculate 10k holders' shares
- Result: Very expensive gas

**Opals approach** (efficient):
- Accumulate fees in contract
- When holder claims: Calculate their share at claim time
- Result: O(1) gas cost per claim

**How it works**:
```
// When fee arrives (cheap, happens once)
accumulatedFees += 0.1 ETH
totalFees = 100.1 ETH

// When holder claims (expensive, only holder pays)
holderShare = (holderPatronPower / totalPatronPower) × totalFees
transfer(holder, holderShare)
```

This scales to millions of holders efficiently.

## Real-World Example: DeFi Protocol Launch

**Project**: DEX protocol raising $5M via Opals

**Initial state**:
- 10,000 Patron Cards sold
- Average $500 card price = $5M raised
- $5M → Uniswap LP (50/50 ETH + TOKEN)

**Month 1 - Early momentum**:
- Daily volume: $500k
- Daily fees: $5k = $150k/month
- Distributed to 10k card holders
- Average per card: $15/month

**Month 3 - Gaining traction**:
- Daily volume: $2M
- Daily fees: $20k = $600k/month
- Average per permanent card: $60/month

**Month 6 - Successful project**:
- Daily volume: $5M
- Daily fees: $50k = $1.5M/month
- Average per permanent card: $150/month

**Year 1 - Established protocol**:
- Daily volume: $10M average
- Daily fees: $100k = $3M/month
- Permanent card holder: $300/month passive income

**Cumulative for 1 permanent card holder**:
- Year 1 rewards: ~$18k
- Return on $500 investment: 3,600% in first year (from fees alone, before token appreciation)

## Comparison: Fee Distributions vs Token Inflation

| Aspect | Fee Distribution | Token Inflation |
|--------|-----------------|-----------------|
| Source | Real trading activity | Printing new tokens |
| Dilution | None (shares actual value) | Massive (dilutes all holders) |
| Sustainable | Yes (scales with usage) | Often unsustainable |
| Alignments | Holders profit when project succeeds | Holders profit only on dump |
| Predictability | Tied to trading volume | Subject to governance changes |
| Long-term value | Actual revenue streams | Often hyperinflation |

Opals uses fee distribution. This is more sustainable than token inflation.

## Gas Costs

**Depositing fees**: ~35k gas per transaction
- Called by market contracts automatically
- Minimal cost

**Claiming rewards**: ~40k gas per transaction
- Holder pays to claim
- Can batch multiple claims

**Updating PatronPower**: ~50k gas
- Called by staking contracts when stakes change
- Typically once per stake lifecycle

All costs are reasonable on Layer 2 networks (~$0.10-$1 per operation).

## Anti-Gaming: Preventing Reward Manipulation

Opals prevents several attack vectors:

**Attack 1: Flash loan attack**
- Attacker borrows huge amount of tokens
- Tries to claim outsized rewards
- Prevention: PatronPower frozen at stake time, cannot change mid-block

**Attack 2: Sybil attack (many small accounts)**
- Attacker creates 1000 accounts
- Each gets tiny reward
- Prevention: Minimum stake requirement, small addresses earn negligible fees

**Attack 3: Exit before distribution**
- Attacker stakes, then exits before distribution
- Prevention: Distribution happens continuously, no "distribution window" to game

**Attack 4: Front-running claims**
- Attacker sees large claim coming
- Tries to exit before distribution
- Prevention: PatronPower weighted by time locked, cannot exit immediately

## Navigation: Understanding Fee Flows

**Question**: Where does my reward come from?
- Answer: Your PatronPower share of accumulated fees
- Next: [Staking](./staking.md) - How to maximize PatronPower

**Question**: How often can I claim?
- Answer: Anytime. Rewards accumulate continuously
- Next: [Claims](./claims.md) - Token claiming mechanics

**Question**: What if volume drops?
- Answer: Rewards scale with volume. Temporary drops recover
- Next: [For-Investors](../for-investors/README.md) - Long-term holding strategy

**Question**: Is this sustainable?
- Answer: Yes. Based on real trading activity, not inflation
- Next: [Tokenomics](../mechanisms/tokenomics.md) - Economic model

## Next Steps

- **[Staking](./staking.md)** - Lock tokens to increase PatronPower
- **[Tokens](./tokens.md)** - Token distribution and supply
- **[Mechanisms: PatronPower System](../mechanisms/patronpower-system.md)** - Deep dive into rewards
