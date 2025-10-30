# Staking

Staking means locking LP tokens to earn PatronPower. PatronPower determines your share of trading fees.

This is how you transform speculation into income.

## Ingredient 1: The Staking Process

Simple lock-and-earn mechanism.

**How to stake**:
1. Hold LP tokens (from Uniswap pair)
2. Call `stake(amount, duration)` on VaultClaim contract
3. Specify how long to lock (7 days to permanent)
4. LP tokens locked, position created as NFT
5. Earn PatronPower based on duration

**That's it**. No approvals beyond standard ERC20. No KYC. Fully permissionless.

**Staking creates an NFT**:
- Represents your staked position
- Non-transferable (locked to address)
- Can be traded on secondary markets
- Burned when stake unlocks

## Ingredient 2: Lock Duration → PatronPower Multiplier

Time commitment directly determines rewards.

**Multiplier schedule**:
- 7-day lock: 0.024x
- 30-day lock: 0.2x
- 90-day lock: 1.0x
- 6-month lock: 2.5x
- 1-year lock: 3.75x
- 2-year lock: 5.0x
- 4-year lock: 7.5x
- Permanent lock: 10.0x

**The economics**:
```
PatronPower = LP Amount × Multiplier

100 LP tokens, 7-day: 100 × 0.024 = 2.4 PatronPower
100 LP tokens, 1-year: 100 × 3.75 = 375 PatronPower
100 LP tokens, permanent: 100 × 10 = 1,000 PatronPower

Result: Permanent earns 416x more rewards despite same capital
```

**Real-world impact**:
- $1M staked 7 days: Earns same as $2,406 staked permanently
- $100k staked 1-year: Earns same as $26.7k staked permanently
- Small holders committed long term beat massive whales on short-term

This eliminates mercenary capital advantage. Size doesn't matter if commitment doesn't match.

## Ingredient 3: Flexible Locking

Three staking options for different strategies.

### Option A: PatronClaim (During Launch)

**When**: During Patron Card sale phase
**How**: Buy Patron Card = automatic stake
**Lock period**: Permanent (only option)
**Multiplier**: 10x (maximum)
**NFT**: Patron Card itself is the stake position

**Example**:
- Buy Patron Card for 0.5 ETH
- Automatic LP allocation (from reserve pool)
- Permanent lock, earning 10x immediately
- Can sell card on secondary market (stake transfers)

### Option B: VaultClaim (After Launch)

**When**: Anytime after launch
**How**: Call `stake()` with LP tokens + duration
**Lock period**: 7 days to permanent (you choose)
**Multiplier**: 0.024x to 10x (based on choice)
**NFT**: Vault receipt token (non-transferable)

**Example**:
- Stake 10 LP tokens, 1-year lock
- Position NFT created
- Lock expires in 1 year
- Can claim LP + rewards after expiration
- Or extend lock before expiration

### Option C: Open Vested Liquidity (OVL) - Early Exit

**When**: Want to exit before lock expires
**How**: Call `exitEarly()` on VaultClaim
**Penalty**: % penalty based on time remaining
**Recipient**: Penalty goes to remaining stakers

**Example**:
- Staked for 1 year (lock expires in 12 months)
- Exit after 6 months: 50% penalty
- Get back: 50% of LP + 50% of accrued rewards
- Remaining 50% redistributed to other stakers

## Recipe: Staking Strategies

### Strategy 1: Long-Term Believer (Permanent)

**Position**: Patron Card with permanent lock
**Capital**: 0.5 ETH Patron Card + auto-allocated LP
**PatronPower**: 10x multiplier
**Rewards**: 10% of project's trading fees (depends on total stakers)

**Timeline**:
- Month 1: Earning rewards immediately
- Year 1: Accumulated significant rewards
- Year 5: Rewards exceed original investment
- Forever: Passive income from project success

**Best for**: Founders, early believers, patient capital

### Strategy 2: Graduated Commitment (Ladder)

**Position**:
- 2 LP tokens, permanent lock: 2 × 10 = 20 PatronPower
- 3 LP tokens, 2-year lock: 3 × 5 = 15 PatronPower
- 3 LP tokens, 1-year lock: 3 × 3.75 = 11.25 PatronPower
- 2 LP tokens, 90-day lock: 2 × 1 = 2 PatronPower
- Total: 48.25 PatronPower

**Rewards**: Spread across different stake expiration dates
- 90-day: Unlocks and available to reinvest
- 1-year: Unlocks next
- 2-year: Unlocks later
- Permanent: Continuously earning

**Best for**: Diversified risk, progressive commitment

### Strategy 3: Short-Term (Testing)

**Position**: 1 LP token, 30-day lock
**PatronPower**: 1 × 0.2 = 0.2 PatronPower
**Rewards**: Small, but tests the mechanism

**Timeline**:
- Day 1-29: Earning rewards (though minimal)
- Day 30: Unlocks
- Can withdraw LP + rewards
- Or re-stake for longer duration

**Best for**: First-time stakers, new projects

## Technical Implementation

### VaultClaim Contract

**Key state**:
- `stakes[holder]`: Array of stake positions
- `totalStaked`: Sum of all LP locked
- `accumulatedRewards[holder]`: Claimable rewards
- `lockDurations[]`: Predefined lock options
- `multipliers[]`: Corresponding multipliers

**Stake structure**:
```
stake = {
  amount: 10 (LP tokens),
  startTime: 1704067200,
  duration: 31536000 (1 year in seconds),
  multiplier: 3.75,
  patronPower: 37.5,
  positionNFT: 0x123 (stake ID)
}
```

**Key functions**:

`stake(uint amount, uint durationIndex)`:
- Validates: amount > 0, duration valid
- Transfers: LP tokens to contract
- Creates: stake struct
- Mints: position NFT to holder
- Updates: totalStaked, holder's PatronPower

`claimRewards() -> uint`:
- Calculates: accrued rewards since last claim
- Formula: (holderPatronPower / totalPatronPower) × feesAccumulated
- Transfers: reward amount to holder
- Resets: rewardTimer
- Returns: amount distributed

`unstake(uint nftId)`:
- Validates: lock period expired
- Transfers: LP + rewards to holder
- Burns: position NFT
- Updates: totalStaked, PatronPower

`exitEarly(uint nftId) -> (uint lpAmount, uint rewardAmount)`:
- Calculates: time remaining as percentage
- Applies: penalty = (time_remaining / total_duration)
- Transfers: (LP - LP penalty) to holder
- Redistributes: LP penalty to remaining stakers
- Burns: position NFT
- Returns: LP received, rewards received

## Gas Costs

**Creating stake**: ~120k gas
- At $30 gas: ~$3.60
- At $5 gas (L2): ~$0.60

**Claiming rewards**: ~80k gas
- At $30 gas: ~$2.40
- At $5 gas (L2): ~$0.40

**Early exit**: ~140k gas
- At $30 gas: ~$4.20
- At $5 gas (L2): ~$0.70

**Unstaking after lock expires**: ~95k gas
- At $30 gas: ~$2.85
- At $5 gas (L2): ~$0.48

All reasonable, especially on Layer 2 networks.

## Real-World Example: Multi-Year Staking

**Project**: Decentralized trading platform
**Investor**: Holds 100 LP tokens, $50k value

**Year 1: 50 LP permanent + 50 LP 4-year**

- Permanent: 50 × 10 = 500 PatronPower
- 4-year: 50 × 7.5 = 375 PatronPower
- Total: 875 PatronPower
- Pool total: 1M PatronPower (~0.0875% share)
- Monthly fees: $50k
- Monthly reward: $43.75

**Year 2: Permanent earning, 4-year locked**

- Earned Year 1: $43.75 × 12 = $525
- Reinvest rewards: Add 1 more LP token permanent
- New total: 501 × 10 + 50 × 7.5 = 5,385 PatronPower
- New monthly reward: ~$269 (higher volume project now)

**Year 5: 4-year lock expires**

- Total earned from fees: ~$18,000 (scaling with volume)
- 50 LP from 4-year stake released
- Can: Unstake, reinvest, or re-stake longer
- Permanent 50+ (original) still earning
- Still holding: ~$50k LP + $18k rewards + reinvestment gains

**Result**: Patient staking creates compounding wealth

## Anti-Gaming: Lock Enforcement

Several mechanisms prevent cheating:

**Mechanism 1: Time-locked withdrawal**
- Cannot unlock before expiration
- Smart contract prevents early access
- Exception: OVL with penalties

**Mechanism 2: Penalty-based early exit**
- Want to exit early? Pay penalty
- Penalty scales with time remaining
- Penalty goes to remaining stakers (incentive aligned)

**Mechanism 3: NFT position tracking**
- Each stake = unique NFT
- NFT cannot be split or combined
- Prevents gaming by splitting positions

**Mechanism 4: PatronPower freezes**
- PatronPower set at stake time
- Cannot change mid-stake
- Prevents flash-loan attacks

## Navigation: Staking Decisions

**Question**: Should I stake for 1 year or permanent?
- Answer: Permanent earns 2.67x more. Only choose 1-year if you might need liquidity.
- Next: [Lock Duration vs Multiplier table](#ingredient-2-lock-duration--patronpower-multiplier)

**Question**: Can I withdraw early?
- Answer: Yes, via Open Vested Liquidity with penalties. Penalty goes to remaining stakers.
- Next: [Option C: OVL](#option-c-open-vested-liquidity-ovl---early-exit)

**Question**: Do I need to claim rewards manually?
- Answer: Yes, claim rewards whenever you want. No penalty for waiting.
- Next: [Distributor](./distributor.md) - How rewards accumulate

**Question**: What if I change my mind about the project?
- Answer: Exit early with penalty, or wait for lock to expire. Your choice.
- Next: [Investor Risk Management](../for-investors/risk-management.md)

## Comparison: Staking vs Holding

| Aspect | Staking | Just Holding |
|--------|---------|-------------|
| LP Locked | Yes (cannot sell) | No (can sell anytime) |
| Rewards | Yes (PatronPower-based) | No |
| Risk | Lock commitment | Full flexibility |
| Return | Higher (if you commit) | Lower |
| Best for | Long-term supporters | Short-term traders |

## Next Steps

- **[Distributor](./distributor.md)** - How rewards flow to stakers
- **[Claims](./claims.md)** - Claiming token allocations from staking
- **[Investor Staking Guide](../for-investors/staking-rewards-guide.md)** - Strategy deep-dive
