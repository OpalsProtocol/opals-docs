# Staking Rewards Guide: Earn Up to 10x More

Lock your LP tokens or project tokens to earn multiplied rewards. Your commitment level determines your multiplier. This guide explains exactly how the system works and how much you can earn.

## Two Staking Options: PatronClaim vs VaultClaim

Opals offers two distinct staking mechanisms with different characteristics.

### PatronClaim: Permanent Lock, Maximum Rewards

**What it is**: When you buy Patron Cards during launch, you automatically participate in PatronClaim. Your LP allocation is locked permanently.

**Multiplier**: 10x (the highest possible)

**Lock period**: Permanent (forever)

**Liquidity**: None. Cannot withdraw LP tokens. Can only sell the Patron Card NFT itself on secondary markets.

**Best for**: True believers committed to the project long-term.

### VaultClaim: Flexible Locks, Variable Rewards

**What it is**: After launch, you can stake LP tokens or project tokens with custom lock periods from 7 days to permanent.

**Multiplier**: 0.024x to 10x depending on lock duration

**Lock period**: You choose (7 days minimum to permanent)

**Liquidity**: Exit early via Open Vested Liquidity (OVL) with penalties, or wait for lock expiration

**Best for**: Investors wanting flexibility and control over commitment level.

## Understanding PatronPower

PatronPower determines your share of reward distributions. Higher PatronPower = larger reward share.

### The Formula

**PatronPower = LP Amount × Time Multiplier**

**For PatronClaim**:
PatronPower = LP Amount × 10

**For VaultClaim**:
PatronPower = LP Amount × (Lock Duration / 4 years) × 5 (capped at 5x for time locks)

Or PatronPower = LP Amount × 10 for permanent locks

### Why This Matters

Two people with the same LP amount earn vastly different rewards based on their commitment.

**Example**:
- Alice: 10 ETH worth of LP, locked 7 days = 10 × 0.024 = 0.24 PatronPower
- Bob: 1 ETH worth of LP, locked permanently = 1 × 10 = 10 PatronPower

Bob earns 41.7x more rewards than Alice despite having 10x less LP.

This is intentional. Opals rewards long-term commitment, not just capital size.

## Complete Multiplier Table

Lock durations map to multipliers using a linear formula based on time:

| Lock Duration | Multiplier | Calculation |
|---------------|------------|-------------|
| 7 days | 0.024x | (7 days / 4 years) × 5 = 0.024 |
| 30 days | 0.104x | (30 days / 4 years) × 5 = 0.104 |
| 90 days | 0.311x | (90 days / 4 years) × 5 = 0.311 |
| 180 days | 0.621x | (180 days / 4 years) × 5 = 0.621 |
| 1 year | 1.25x | (365 days / 4 years) × 5 = 1.25 |
| 2 years | 2.5x | (2 years / 4 years) × 5 = 2.5 |
| 3 years | 3.75x | (3 years / 4 years) × 5 = 3.75 |
| 4 years | 5x | (4 years / 4 years) × 5 = 5.0 |
| Permanent | 10x | Fixed maximum multiplier |

**Key insight**: Multiplier scales linearly from 7 days to 4 years, then doubles for permanent locks.

## Reward Calculation Examples

Let's work through detailed scenarios showing exactly how rewards get distributed.

### Scenario 1: Simple Two-Staker Pool

**Setup**:
- Alice: 10 ETH LP, 7-day lock = 0.24 PatronPower
- Bob: 10 ETH LP, permanent lock = 100 PatronPower
- Total PatronPower: 100.24

**Reward distribution**:
Project generates $10,000 in protocol fees this month.

- Alice's share: (0.24 / 100.24) × $10,000 = $23.94
- Bob's share: (100 / 100.24) × $10,000 = $9,976.06

Bob earns 417x more than Alice with same LP amount, purely because of commitment level.

### Scenario 2: Diverse Staker Pool

**Setup**:
- Alice: 5 ETH LP, 1-year lock = 6.25 PatronPower
- Bob: 10 ETH LP, 2-year lock = 25 PatronPower
- Carol: 2 ETH LP, permanent lock = 20 PatronPower
- Dave: 20 ETH LP, 30-day lock = 2.08 PatronPower
- Total PatronPower: 53.33

**Reward distribution**:
Project generates $5,000 in protocol fees this month.

- Alice: (6.25 / 53.33) × $5,000 = $586.44 (11.7% APY on her 5 ETH)
- Bob: (25 / 53.33) × $5,000 = $2,343.77 (23.4% APY on his 10 ETH)
- Carol: (20 / 53.33) × $5,000 = $1,875.02 (93.8% APY on her 2 ETH!)
- Dave: (2.08 / 53.33) × $5,000 = $194.99 (1.0% APY on his 20 ETH)

Carol has the least LP but earns the third most rewards because of her permanent lock. Her APY is highest because small capital with maximum commitment beats large capital with minimal commitment.

### Scenario 3: Real-World Complex Pool

**Setup**: 100 total stakers with mixed positions
- 10 Patron Card holders (permanent, avg 1 ETH each) = 100 PatronPower total
- 30 VaultClaim stakers (2-year avg, avg 2 ETH each) = 150 PatronPower total
- 40 VaultClaim stakers (1-year avg, avg 3 ETH each) = 150 PatronPower total
- 20 VaultClaim stakers (90-day avg, avg 5 ETH each) = 31.1 PatronPower total
- Total PatronPower: 431.1

**Reward distribution**:
Project generates $20,000 monthly in protocol fees.

**Per-group earnings**:
- Patron Card holders: (100 / 431.1) × $20,000 = $4,636.62
- 2-year stakers: (150 / 431.1) × $20,000 = $6,954.93
- 1-year stakers: (150 / 431.1) × $20,000 = $6,954.93
- 90-day stakers: (31.1 / 431.1) × $20,000 = $1,442.65

**Per-individual average**:
- Patron Card holder: $463.66 monthly on 1 ETH = 463% APY
- 2-year staker: $231.83 monthly on 2 ETH = 139% APY
- 1-year staker: $173.87 monthly on 3 ETH = 69% APY
- 90-day staker: $72.13 monthly on 5 ETH = 17% APY

**Takeaway**: Patron Card holders with smallest LP amounts earn the highest APY because of their permanent commitment and 10x multiplier.

### Scenario 4: Whale vs Diamond Hands

**Setup**:
- Whale: 100 ETH LP, 7-day lock = 2.4 PatronPower
- Small holder 1: 1 ETH LP, permanent lock = 10 PatronPower
- Small holder 2: 1 ETH LP, permanent lock = 10 PatronPower
- Small holder 3: 1 ETH LP, permanent lock = 10 PatronPower
- Total PatronPower: 32.4

**Reward distribution**:
Project generates $10,000 in protocol fees.

- Whale: (2.4 / 32.4) × $10,000 = $740.74 (0.74% monthly return on 100 ETH)
- Each small holder: (10 / 32.4) × $10,000 = $3,086.42 (308.6% monthly return on 1 ETH!)

Combined, three people with 3 ETH total earn $9,259.26 while the whale with 100 ETH earns only $740.74.

**This is the point**: PatronPower prevents mercenary capital from extracting value. Short-term whales get minimal rewards. Long-term believers get maximum rewards.

## Open Vested Liquidity (OVL): The Early Exit System

VaultClaim includes OVL, allowing you to exit before your lock period expires. But there's a cost.

### How OVL Works

**The penalty formula**:

Penalty = (Staked Amount × Remaining Time / Total Lock Duration) × 50%

**Key characteristics**:
- Maximum penalty: 50% (if you exit immediately after staking)
- Minimum penalty: 0% (if you exit exactly at lock expiration)
- Linear decrease: Penalty drops proportionally as time passes

**Where penalties go**: Redistributed to remaining stakers who completed their full lock terms. Diamond hands get rewarded with your penalties.

### OVL Examples

**Example 1: Exit Immediately**

- You stake: 10 ETH
- Lock period: 1 year
- You exit: 1 day later
- Remaining time: 364 days
- Penalty: (10 × 364/365) × 50% = 4.986 ETH
- You receive: 5.014 ETH
- Lost: 49.86%

**Example 2: Exit Halfway**

- You stake: 10 ETH
- Lock period: 1 year
- You exit: 6 months later
- Remaining time: 182.5 days
- Penalty: (10 × 182.5/365) × 50% = 2.5 ETH
- You receive: 7.5 ETH
- Lost: 25%

**Example 3: Exit Near End**

- You stake: 10 ETH
- Lock period: 1 year
- You exit: 11 months later
- Remaining time: 30 days
- Penalty: (10 × 30/365) × 50% = 0.411 ETH
- You receive: 9.589 ETH
- Lost: 4.11%

**Example 4: Exit at Expiration**

- You stake: 10 ETH
- Lock period: 1 year
- You exit: Exactly 1 year later
- Remaining time: 0 days
- Penalty: 0 ETH
- You receive: 10 ETH + any accumulated rewards
- Lost: 0%

### Strategic Use of OVL

**When OVL makes sense**:
- Emergency liquidity need
- Lost confidence in project
- Found much better opportunity
- Near end of lock period (low penalty)

**When OVL doesn't make sense**:
- Just started lock (50% penalty too high)
- No urgent need for liquidity
- Project still executing well
- Penalties exceed gains from alternative use

### Diamond Hands Bonus

If you complete your full lock period without early exit, you earn a 20% bonus on your staked amount.

**Example**:
- You stake: 10 ETH
- Lock period: 2 years
- You wait full 2 years
- Diamond bonus: 10 ETH × 20% = 2 ETH
- Total withdrawal: 10 ETH + 2 ETH + accumulated rewards = 12+ ETH

**Plus**: You've been earning rewards during the full 2 years at your lock multiplier (2.5x for 2-year locks).

**Combined benefit**: Your rewards over 2 years + 20% bonus significantly outweighs early exit.

## Comparing Lock Durations: ROI Analysis

Let's compare actual returns across different lock durations using realistic assumptions.

**Assumptions**:
- Initial stake: 10 ETH
- Project monthly protocol fees: $50,000
- Total competing PatronPower: 1,000 (you're competing against others)

### 7-Day Lock

- Your PatronPower: 0.24
- Your share: 0.024%
- Monthly rewards: $12
- Annual rewards: $144
- Annual ROI: 1.44%
- After 1 year: 10 ETH + $144 = ~10.07 ETH equivalent

**Pros**: Maximum flexibility
**Cons**: Minimal rewards

### 1-Year Lock

- Your PatronPower: 12.5
- Your share: 1.25%
- Monthly rewards: $625
- Annual rewards: $7,500
- Annual ROI: 75%
- After 1 year (full term): 10 ETH + $7,500 + 2 ETH bonus = ~12.7 ETH equivalent

**Pros**: Decent rewards, moderate commitment
**Cons**: 1-year liquidity lock

### 2-Year Lock

- Your PatronPower: 25
- Your share: 2.5%
- Monthly rewards: $1,250
- Annual rewards: $15,000
- 2-year rewards: $30,000
- Annual ROI: 150%
- After 2 years (full term): 10 ETH + $30,000 + 2 ETH bonus = ~16.5 ETH equivalent

**Pros**: Strong rewards, significant commitment
**Cons**: 2-year liquidity lock

### 4-Year Lock

- Your PatronPower: 50
- Your share: 5%
- Monthly rewards: $2,500
- Annual rewards: $30,000
- 4-year rewards: $120,000
- Annual ROI: 300%
- After 4 years (full term): 10 ETH + $120,000 + 2 ETH bonus = ~32 ETH equivalent

**Pros**: Maximum time-locked rewards
**Cons**: 4-year liquidity lock

### Permanent Lock

- Your PatronPower: 100
- Your share: 10%
- Monthly rewards: $5,000
- Annual rewards: $60,000
- Annual ROI: 600%
- After 1 year: 10 ETH + $60,000 = ~20 ETH equivalent
- After 4 years: 10 ETH + $240,000 = ~80 ETH equivalent

**Plus**: You continue earning forever. Year 10? 10 ETH + $600,000 = ~200 ETH equivalent.

**Pros**: Maximum possible rewards, benefit from all OVL penalties
**Cons**: Zero liquidity ever

**Note**: These calculations assume constant protocol fees. Real fees will vary significantly based on project success.

## Optimization Strategies

How to maximize your staking returns.

### Strategy 1: Ladder Your Locks

Don't put everything in one lock duration. Spread across multiple durations.

**Example allocation of 10 ETH**:
- 2 ETH: 90-day lock (liquidity in 3 months)
- 3 ETH: 1-year lock (liquidity in 1 year)
- 3 ETH: 2-year lock (better multiplier)
- 2 ETH: Permanent (maximum rewards)

**Benefits**:
- Some liquidity available at intervals
- Diversified risk
- Balanced reward optimization
- Can reassess and re-stake as locks expire

### Strategy 2: Start Conservative, Extend Later

Begin with shorter locks. As project proves itself, extend to longer locks.

**Example progression**:
- Month 1: Stake 5 ETH for 90 days (test the waters)
- Month 4: Stake 5 ETH for 1 year (project looking good)
- Month 6: Add 10 ETH for 2 years (strong conviction)
- Year 2: Convert some to permanent (ultra-conviction)

**Benefits**:
- Lower initial risk
- Learn system gradually
- Commit more as confidence grows
- Avoid permanent lock regret

### Strategy 3: Permanent Lock Small Amount

Put a small amount in permanent lock for maximum multiplier, keep rest flexible.

**Example with 10 ETH**:
- 1 ETH: Permanent (10x multiplier, high APY%)
- 9 ETH: 1-year lock (flexibility)

**Benefits**:
- Capture some maximum-multiplier rewards
- Maintain substantial liquidity
- Lower risk if project fails
- Can always add more to permanent later

### Strategy 4: Compound Rewards

Don't withdraw rewards. Restake them to compound returns.

**Example**:
- Initial: 10 ETH staked, 2-year lock
- Year 1 rewards: 5 ETH worth of rewards
- Restake: Add 5 ETH to new 2-year lock
- Year 2 rewards: Now earning on 15 ETH effective
- Continue compounding

**Benefits**:
- Exponential growth
- Higher PatronPower over time
- Larger share of reward pool
- Builds long-term wealth

**Cons**:
- Locks up rewards
- Increases exposure to single project
- Higher risk if project fails

### Strategy 5: Exit and Re-enter

Use OVL strategically when penalty is low.

**Example**:
- Staked 10 ETH for 1 year
- After 10 months: Penalty only 8.3%
- Exit: Receive 9.17 ETH
- Immediately restake 9.17 ETH for 1 year
- New lock ends 12 months later instead of 2 months later

**Benefits**:
- Reset lock expiration to convenient time
- Minimal penalty cost
- Maintain similar PatronPower
- Timing flexibility

**Use sparingly**: Only when strategic benefit exceeds penalty cost.

## Reward Distribution Mechanics

Understanding when and how you receive rewards.

### Accumulator-Based Accounting

Opals uses accumulator-based accounting for gas efficiency. You don't receive individual payments. Instead:

**How it works**:
1. Protocol fees deposit into reward contract
2. Contract calculates per-PatronPower distribution
3. Your claimable amount updates automatically
4. You claim anytime

**Benefits**:
- No need to claim immediately
- Rewards accumulate continuously
- Claim when gas is cheap
- Claim many periods at once

### When to Claim

**Claim frequently if**:
- You need the income
- You want to compound elsewhere
- Gas is cheap
- Large accumulated amount (risk mitigation)

**Claim infrequently if**:
- You're holding long-term anyway
- Gas is expensive
- Small accumulated amounts (gas cost > reward value)
- Tax timing considerations

### Gas Cost Considerations

**Claiming costs gas**. If your reward is $50 and gas is $20, you're paying 40% fees to claim.

**Strategy**: Wait until accumulated rewards are 10x gas cost before claiming. If gas is $20, wait until you've accumulated $200+ in rewards.

**Exception**: If you're compounding rewards, the long-term benefit may justify higher gas cost percentage.

## Tax Implications

Consult a tax professional. Generally:

**Staking**: May or may not be taxable depending on jurisdiction.

**Earning rewards**: Usually taxable as income when claimed.

**Compounding**: May trigger taxable event even if not withdrawing to bank account.

**Early exit via OVL**: Penalties may or may not be deductible losses.

**Diamond bonus**: Likely taxable as income.

Tax treatment varies wildly. Get professional advice.

## Common Questions

**Q: Can I add to my stake without resetting the lock period?**
A: No. Each stake is separate. Adding more creates a new staking position with its own lock period.

**Q: What happens if I transfer my VaultCard NFT?**
A: The new owner receives the staked LP and accumulated rewards. You lose access to that stake.

**Q: Can I partially withdraw from a stake?**
A: No. OVL is all-or-nothing. You exit the entire stake or none of it.

**Q: Do I lose accumulated rewards if I exit early via OVL?**
A: No. You keep accumulated rewards. You only pay penalty on the staked LP amount.

**Q: Can I convert a time-locked stake to permanent?**
A: Not directly. You'd need to exit via OVL (paying penalty), then restake as permanent.

**Q: What if project stops generating protocol fees?**
A: Your LP still earns trading fees from Opals' custom Uniswap V2 fork (1% of volume, not the standard 0.3%). Protocol fee rewards dry up, but trading fees continue as long as people trade.

**Q: Is my stake safe if project team disappears?**
A: Yes. Stakes are in smart contracts. Team can't access them. Your lock expiration still honors. You can still claim rewards and withdraw.

**Q: Can I stake tokens I bought on Uniswap after launch?**
A: Yes. VaultClaim accepts both LP tokens and regular project tokens (if configured). Check specific project's VaultClaim settings.

## Next Steps

Now that you understand staking:

**Assess your risks**:
[Risk management guide](./risk-management.md) →

**Optimize your strategy**:
[Maximizing returns](./maximizing-returns.md) →

**Understand your investment**:
[Understanding Patron Cards](./understanding-patron-cards.md) →

**Ready to start?**:
[Getting started guide](./getting-started.md) →

---

**Remember**: Longer locks earn exponentially more. A 1 ETH permanent lock earns more than a 100 ETH 7-day lock. PatronPower rewards commitment, not just capital. Choose your lock duration based on your conviction level and liquidity needs.
