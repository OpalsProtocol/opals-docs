# Tokens

Tokens are the economic engine of Opals projects. They're not just speculative assets—they're income-generating instruments tied to real usage.

## Token Ingredient: What Tokens Do

Tokens in Opals serve four purposes:

1. **Medium of exchange**: Trading pair on Uniswap (the project token paired with ETH)
2. **Reward**: Distributed to early supporters based on commitment
3. **Economic participation**: Trading fees flow to token holders via Distributor
4. **Governance** (optional): Projects can assign voting rights

## Token Distribution: Three Classes

Opals supports flexible token allocation across three classes:

**Patron Cards** (60-80% of supply):
- Early, committed supporters
- Buy Patron Cards during launch
- Longest vesting period (typically 4 years)
- Earn 10x PatronPower rewards
- Example: $1M raise, 60% to Patron Cards = 600M tokens allocated

**Member & Contributor Cards** (10-30% total):
- Member Cards: Community members, 10-20% supply, 2-year vest
- Contributor Cards: Team/advisors, 5-15% supply, 1-year vest
- Lower PatronPower (2-5x)

**Team Reserve** (5-10%):
- Project founders and key team
- Often vests 4 years with 1-year cliff
- Aligns team incentives with long-term success

**Example allocation of 1 billion tokens**:
- Patron Cards: 600M (60%)
- Member Cards: 200M (20%)
- Contributor Cards: 100M (10%)
- Team: 100M (10%)

All percentages are configurable per project.

## Vesting: Linear Distribution

All tokens vest linearly. No cliffs. No sudden unlocks that create market shocks.

**Patron Cards example**: 600M tokens over 4 years = 150M unlocked per year = 12.5M per month

**Member Cards example**: 200M tokens over 2 years = 100M per year = 8.3M per month

Vesting starts at deployment. Supporters can claim tokens starting immediately but often wait for full vesting to avoid forfeiting unvested tokens (see Diamond Hands mechanism).

## Trading Fee Revenue Stream

Every swap on the project's Uniswap pool generates 1% in fees. These fees flow to the Distributor contract and get distributed based on PatronPower.

**Monthly revenue example**:
- Trading volume: $10M/month
- Fee rate: 1% = $100k/month in fees
- Distributor allocates based on PatronPower

Token holders with permanent locks (10x PatronPower) earn 10x more than short-term traders (0.024x multiplier).

## Token Economics: Three Models

### Fixed Supply Model

- Total supply: Fixed (no inflation)
- Example: 1 billion tokens, max supply
- Scarcity increases value as adoption grows
- Most common on Opals

**Pros**:
- Simple to understand
- Value increases through scarcity
- No dilution concerns

**Cons**:
- Cannot fund ongoing development through token emissions
- Limited long-term revenue model

### Inflationary Model

- Annual inflation: 3-10% new tokens per year
- Example: 1 billion initial, 50M new tokens per year
- Emissions can fund treasury or rewards
- Less common, requires careful management

**Pros**:
- Sustainable ongoing funding
- Can reward community participation over time

**Cons**:
- Existing holders diluted annually
- Requires transparent governance

### Hybrid Model

- Fixed supply for Patron/Member/Contributor allocations
- Small annual emission (1-2%) for ecosystem incentives
- Balance between scarcity and sustainability

## Governance (Optional)

Projects can assign governance rights to tokens:

**Democratic model**: 1 token = 1 vote on proposals
**Quadratic voting**: Vote weight = sqrt(tokens held) to reduce whale control
**Delegated model**: Token holders delegate voting power

Opals leaves governance structure to project teams. Some projects prefer decentralized governance. Others prefer founder-controlled decisions initially.

## Contract Architecture

### Token Contract (ERC20 Standard)

**Deployed by**: TemplateFactory as a clone of Token template
**Network addresses**: Ethereum, Optimism, Base, Arbitrum
**Key functions**:
- `mint(to, amount)`: Create new tokens (only called during allocation)
- `transfer(recipient, amount)`: Send tokens to another address
- `approve/transferFrom`: Allow third parties to move your tokens

**Vesting tracking**: Stored in separate Vesting contract (not the token itself)

### Vesting Contract

**Purpose**: Track token release schedules per allocation class
**Key data**: Start time, cliff (if any), duration, amount claimed vs unclaimed

**Example state**:
```
Patron Cards: 600M total, 12.5M per month, started Jan 1, 2025
- January: 12.5M claimable
- February: 25M claimable total
- March: 37.5M claimable total
...
```

## Real-World Example: DeFi Protocol Launch

**Scenario**: DeFi protocol raising via Opals

**Token Supply**: 1 billion PROTOCOL tokens

**Allocation**:
- 600M (60%): Patron Cards - supporter ownership
- 200M (20%): Member Cards - community members
- 100M (10%): Contributor Cards - developers, advisors
- 100M (10%): Team - founders

**Vesting Schedule**:
- Patron Cards: 4-year linear vest, starts at deployment
- Member Cards: 2-year linear vest
- Contributor Cards: 1-year linear vest
- Team: 4-year vesting with 1-year cliff

**Trading Fees**:
- Launch with $10M in liquidity
- First month: $5M trading volume = $50k fees
- Token holder with Patron Card: Gets rewards based on 10x PatronPower

**Year 1 picture**:
- 150M Patron tokens vest (25% of allocation)
- 100M Member tokens vest (50% of allocation)
- 100M Contributor tokens vest (100%, released)
- Team tokens locked (1-year cliff)
- Trading volume growing, fees accumulating
- Token price determined by market, but backed by fee revenue

## Comparison: Opals vs Traditional Equity

| Aspect | Opals Token | Traditional VC Equity |
|--------|-----------|---------------------|
| Distribution | Transparent, smart contract | Private cap table |
| Vesting | Linear, 4 years typical | Cliff + linear (common 1yr cliff) |
| Liquidity | Can trade day 1 (vesting permitting) | Illiquid until IPO/acquisition (5-10 years) |
| Revenue sharing | Via trading fees + governance | Via dividends (rarely given in startups) |
| Ownership % | Founder keeps majority | Diluted by series rounds |
| Founder control | Full (no board oversight) | Limited (board seats lost) |

## When Token Distribution Matters Most

**For founders**:
- Team allocation reflects long-term alignment
- Patron allocation incentivizes supporter commitment
- Vesting schedules prevent team dumping

**For supporters**:
- Vesting schedules determine when you can claim
- Allocation percentages show founder transparency
- Fee revenue stream provides real value beyond speculation

**For developers**:
- Standard ERC20 token integrates with DeFi
- Vesting contract provides release schedule
- Distributor handles fee allocation automatically

## Next Steps

- **[Markets](./markets.md)** - How tokens get distributed (Stepped, Fixed, Members)
- **[Claims](./claims.md)** - How holders claim their token allocations
- **[Distributor](./distributor.md)** - How fees flow to token holders
