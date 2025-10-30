# Claims

Claims are the bridge between Patron Cards and tokens. They're how supporters convert card ownership into actual token ownership.

## Ingredient 1: The Claiming Process

Simple and permissionless.

**How to claim**:
1. Wait for project launch (Uniswap pair created)
2. Connect your wallet with Patron Cards
3. Call `claim()` on ClaimContract
4. Receive your tokens in wallet

**That's it**. No KYC. No approvals. No delays. Smart contracts handle everything automatically.

**Timing**:
- Claims become available immediately after launch
- Can claim anytime: day 1, year 1, year 4, whenever
- Once claimed: cannot claim again (finality)

## Ingredient 2: The Diamond Hands Mechanism

This is the secret sauce. Patience is rewarded economically.

**The mechanic**: When you claim, you forfeit unvested tokens. Forfeited tokens redistribute to remaining holders.

**Example**: Patron Card allocation: 1,000 tokens vesting over 4 years

**Scenario A**: Claim at 25% vesting
- You receive: 250 tokens (25% vested)
- You forfeit: 750 tokens (75% unvested)
- Community receives: 750 extra tokens (distributed pro-rata)

**Scenario B**: Claim at 100% vesting
- You receive: 1,000 tokens (all vested)
- You forfeit: 0 tokens
- Community receives: 0 (you got everything)

**The formula**:
```
Your tokens = allocation × (vesting percentage)
Forfeited = allocation × (1 - vesting percentage)
Redistributed = forfeited tokens go to remaining holders
```

**Real numbers**: 1M total supply, 600M to Patron Cards, 10,000 Patron Cards

- Each card: 60,000 tokens over 4 years
- If 5,000 people claim at 25% vesting:
  - Each gets: 15,000 tokens
  - Total forfeited: 225M tokens
  - Remaining 5,000 holders share 225M bonus
  - Each remaining holder gets ~45k extra tokens

**Why it works**: Claiming early hurts you more than it helps. Patience pays.

## Ingredient 3: Claiming Strategies

Different strategies work for different token holders.

**Strategy 1: Claim Early (Day 1)**
- Get tokens immediately for trading
- Forfeit 75% of allocation
- Best for: Need immediate liquidity, already rich
- Gas cost: ~60k gas (one-time)

**Strategy 2: Claim at 1 Year (25% vesting)**
- Get 25% of allocation + share of forfeited tokens
- Better than day 1, much worse than waiting
- Best for: Need some tokens but can wait
- Gas cost: ~60k gas (one-time)

**Strategy 3: Claim at 4 Years (100% vesting)**
- Get all 60,000 tokens + share of forfeited bonus
- Maximum allocation + bonus from patient holders
- Best for: True believers, maximizing tokens
- Gas cost: ~60k gas (one-time)

**Strategy 4: Never Claim**
- Keep cards indefinitely
- Earn 10x PatronPower rewards forever
- Get trading fee distributions without token disposal
- Best for: Wants rewards + token price appreciation

## Recipe: When Should You Claim?

**Claim early if**:
- You need tokens for some immediate use
- You don't believe in project long-term
- You want to reduce risk by taking gains

**Claim later if**:
- You believe in the project
- You can afford to wait
- You want to maximize tokens + bonuses

**Never claim if**:
- You want maximum rewards (PatronPower 10x)
- You trust the project completely
- You want long-term passive income

## Technical Implementation

### Claim Contract (PatronClaim)

**Key state**:
- `claimees[]`: List of Patron Card holders
- `claimedAmount[]`: How many tokens each person claimed
- `totalClaimed`: Total claimed so far
- `vestingStart`: When vesting began
- `vestingDuration`: How long until fully vested (typically 4 years = 126,144,000 seconds)

**Key functions**:

`availableBalance(address holder) -> uint`:
- Calculates how many tokens are claimable
- Based on: (allocation × time elapsed / vesting duration)
- Returns: claimable amount

`claim() -> uint`:
- Called by holder
- Checks: holder has Patron Card
- Calculates: vested amount
- Transfers: tokens to holder wallet
- Records: claim in claimedAmount[holder]
- Returns: tokens transferred

`getForfeited() -> uint`:
- Calculates total forfeited across all claimers
- Used to distribute bonuses to remaining holders

### Vesting Mathematics

**Linear vesting formula**:
```
vestedAmount = allocation × (elapsed_time / total_duration)

Example: 1,000 tokens, 4-year vesting
- Day 0: 0 tokens vested
- Day 365: 250 tokens vested (1/4)
- Day 730: 500 tokens vested (2/4)
- Day 1095: 750 tokens vested (3/4)
- Day 1460: 1,000 tokens vested (4/4 = 100%)
```

**Bonus redistribution**:
```
bonus_per_holder = total_forfeited / num_remaining_holders

Example:
- Total Patron Cards: 10,000
- Cards claimed so far: 5,000
- Total forfeited from claims: 225M tokens
- Remaining holders: 5,000
- Bonus per remaining holder: 225M / 5,000 = 45k tokens each
```

## Real-World Example: DeFi Protocol

**Project**: DeFi swap protocol raising $5M on Opals

**Token allocation**: 600M tokens to Patron Cards
- 10,000 Patron Cards = 60,000 tokens each
- Vesting: 4 years linear, starting at deployment

**Timeline**:

**Day 0 (Launch)**:
- Uniswap pair created
- Claims open
- Token price: $0.01 (1,000 ETH / 100M circulating)

**Day 1**:
- 1,000 impatient holders claim at 0% vesting
- Each gets: 0 tokens (nothing vested yet)
- Forfeit: 60,000 × 1,000 = 60M tokens
- Bonus to remaining: 60M / 9,000 = ~6,667 extra tokens each

**Day 30 (1 month)**:
- Token price: $0.05 (volume growing)
- 2,000 more holders claim at ~0.8% vesting
- Each gets: ~480 tokens
- Forfeit: ~59,520 × 2,000 = 119M tokens
- Bonus to remaining: 119M / 7,000 = ~17k extra tokens

**Year 1**:
- Token price: $0.50 (successful project)
- 2,000 more claim at 25% vesting
- Each gets: 15,000 tokens
- Forfeit: 45,000 × 2,000 = 90M tokens
- Bonus to remaining: 90M / 5,000 = 18k extra tokens

**Year 4 (Fully vested)**:
- Token price: $5.00 (successful project)
- Remaining 5,000 holders claim 100%
- Each gets: 60,000 + accumulated bonus (~60k) = 120k tokens
- They waited 4 years, now they have 2x the original allocation

## Gas Costs

**Claiming**: ~60k gas per transaction
- At 50 Gwei: ~$3 (Ethereum mainnet)
- At 5 Gwei: ~$0.30 (Base/Optimism)

**Batch claiming**: Multiple cards in one tx
- Card 1-10: ~60k gas + 5k per additional card
- Claiming 10 cards: ~105k gas total

## Common Questions

**Q: Can I claim part of my allocation?**
A: No. One claim transaction claims everything that's vested. All-or-nothing per holder.

**Q: What if I lose my Patron Card after claiming?**
A: You already have the tokens. The NFT doesn't matter after claiming. Tokens are yours.

**Q: Can founders change the vesting schedule?**
A: No. Vesting is immutable smart contract code. Founder cannot extend or shorten vesting.

**Q: What happens if I never claim?**
A: You keep the Patron Card forever. Earn 10x rewards. Never convert to tokens unless you want to.

**Q: Can I claim on behalf of someone else?**
A: No. Only the card holder can call claim(). They must sign the transaction.

## Comparison: Claim Strategies

| Strategy | Claim Time | Tokens Get | Bonus | Total | Best For |
|----------|-----------|-----------|-------|-------|----------|
| Immediate | Day 1 | 0-100 | None | 0-100 | Impatient |
| Early | 1 year | 15k | Small | 17-18k | Need cash |
| Patient | 2 years | 30k | Medium | 36-40k | Believers |
| Diamond Hands | 4 years | 60k | Large | 100-120k | True believers |
| Never Claim | Forever | 0 | N/A | ∞ rewards | Max rewards |

## Next Steps

- **[Tokens](./tokens.md)** - Token distribution and vesting
- **[Patron Cards](./patron-cards.md)** - Card ownership mechanics
- **[Staking](./staking.md)** - Lock tokens for rewards
