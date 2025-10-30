# LP Tokens

LP tokens represent your share of the Uniswap liquidity pool. They're how you own a piece of the trading pair and earn from its success.

These are the economic foundation of Opals. Everything flows through LP tokens.

## Ingredient 1: What LP Tokens Represent

Ownership in a trading pair, not just a receipt.

**How they work**:
1. Uniswap pair created: TOKEN-ETH (50-50 split)
2. Founder deposits: X ETH + Y TOKENs
3. Uniswap mints: LP receipt tokens
4. LP tokens represent: Fractional ownership of pool

**Example**:
- Founder deposits: 1,000 ETH + 50M TOKENs
- Uniswap mints: 7,071 LP tokens (√(1,000 × 50M))
- Each LP token: Represents ownership of that pool share
- As pool grows: LP token value increases

**What you get owning LP tokens**:
1. **Trading fee share**: Proportional % of all 1% fees
2. **Pool growth**: As pool accumulates value
3. **Liquidity**: Can sell tokens on secondary market
4. **Potential governance**: Some projects enable voting

## Ingredient 2: Permanent Lock Guarantee

No rug pulls. Mathematically impossible.

**How locks work**:
- Founder deploys PatronClaim contract
- Transfers all LP tokens to PatronClaim
- PatronClaim has NO withdrawal function
- LP tokens locked permanently in contract code

**Why this matters**:
- Rug pull requires: Removing liquidity
- Removing liquidity requires: Calling `removeLiquidity()` on Uniswap
- Calling `removeLiquidity()` requires: LP token transfer
- But PatronClaim: Forbids transfers (no function)
- Result: Mathematically impossible to rug pull

**The contract**:
```
contract PatronClaim {
  IERC20 public lpToken;  // The locked LP tokens

  constructor(address _lpToken) {
    lpToken = _lpToken;
    // Transfer all LP to this contract
    // Now they're locked forever
  }

  // NO transfer() function
  // NO withdraw() function
  // NO admin() function
  // Result: LP cannot leave contract
}
```

**Example numbers**:
- Initial LP locked: 7,071 tokens
- Value at launch: $5M
- Locked forever: 7,071 tokens
- Cannot be withdrawn: Ever
- Founder cannot rug: Mathematically impossible

## Ingredient 3: Fee Generation & Distribution

Every swap generates revenue shared with LP holders.

**Fee flow**:
1. Trader buys TOKEN on Uniswap
2. Uniswap charges 0.3% normal fee (goes to Uniswap)
3. Opals adds 1% additional fee (custom hook)
4. 1% flows to Distributor contract
5. Distributor tracks LP ownership
6. Fees distributed pro-rata based on LP holdings

**Example**: 10,000 ETH daily volume
- Daily trading: $15M (10k ETH × $1,500/ETH)
- Opals fee: 1% = $150k per day
- Monthly: $4.5M in fees
- To LP holders: Distributed based on their share

**Who gets what**:
- Patron Card holders (permanent LP): 10x multiplier
- 1-year stakers: 3.75x multiplier
- 30-day stakers: 0.2x multiplier
- Multiplier × LP amount = PatronPower
- PatronPower % of total = Fee % earned

## Ingredient 4: LP Token Economics

How LP value changes over time.

**LP value calculation**:
```
LP Value = (Pool Token A Reserve × Price A) + (Pool Token B Reserve × Price B) / # of LP Tokens

Example:
- Uniswap reserves: 1,000 ETH + 50M TOKENS
- ETH price: $1,500
- TOKEN price: $0.05
- Total value: (1,000 × $1,500) + (50M × $0.05) = $3.5M
- LP tokens: 7,071
- Per LP value: $495 (3.5M / 7,071)
```

**LP value growth**:
As trading happens and fees accumulate:
- Uniswap reserves grow
- Token prices fluctuate
- Fee accumulation increases reserve value
- LP token value increases proportionally

**Example timeline**: Founder's 7,071 LP tokens

- Launch: $3.5M total value = $495/token
- Month 1: Trading volume grows, fees accumulate = $3.8M total = $537/token
- Month 3: Project gaining traction = $4.5M total = $636/token
- Year 1: Successful project = $8M total = $1,131/token

Result: LP value doubled in 1 year from fee accumulation + token appreciation.

## Recipe: LP Token Distribution Strategies

### Strategy 1: Permanent Lock (Founder + Patrons)

**Position**: All initial LP tokens locked in PatronClaim
**Amount**: 7,071 tokens (example)
**Lock**: Permanent, no withdrawal ever
**Earning**: Proportional fee share

**Timeline**:
- Year 1: LP value: $495 → $1,131 (2.28x)
- Fee income: ~$54k (from $4.5M annual fees)
- Total gain: Capital appreciation + fee income
- Forever: Continuous fee generation

**Best for**: Founders, long-term supporters

### Strategy 2: Divided Allocation (Gradual Stake)

**Position**:
- 3,500 LP tokens permanent (50% allocation)
- 3,500 LP tokens via 2-year stake (50% allocation)

**Lock**:
- Permanent: Never exits
- 2-year: Unlocks and can re-stake or exit

**Rewards**:
- Permanent LP: Earning forever (10x multiplier)
- 2-year LP: High multiplier (5x) until unlock
- Total: Diversified exposure

**Example Year 2**:
- Permanent 3,500 × 10x = 35,000 PatronPower
- 2-year 3,500 × 5x = 17,500 PatronPower
- Total: 52,500 PatronPower
- Fee share: 52,500 / (total pool) = proportional earnings

### Strategy 3: Secondary Market LP (Traders)

**Position**: Buy LP tokens on secondary market
**Source**: Other holders selling LP (for liquidity reasons)
**Cost**: Market price (variable)
**Earning**: Fee share pro-rata

**Timeline**:
- Buy: 100 LP tokens at $600/token = $60k
- Hold: 1 year, earn fees
- Sell: 100 LP tokens at $750/token = $75k
- Plus: Fee income earned during holding

**Best for**: Speculators wanting both income + appreciation

## Technical Implementation

### LP Token Mechanics (Uniswap V2)

**LP token contract**:
- Standard ERC20 token
- Minted when liquidity added: `mint(address to, uint amount)`
- Burned when liquidity removed: `burn(address from, uint amount)`
- Transferable like any ERC20

**Uniswap pair contract**:
```
// Provides liquidity: Get LP tokens
addLiquidity(amountA, amountB) -> lpMinted

// Remove liquidity: Burn LP tokens
removeLiquidity(lpAmount) -> (amountA, amountB)

// Check reserves
getReserves() -> (reserveA, reserveB, blockTime)
```

### Permanent Lock Implementation

**PatronClaim contract structure**:

```
contract PatronClaim {
  IERC20 public immutable lpToken;
  address public immutable uniswapPair;

  constructor(address _lpToken) {
    lpToken = IERC20(_lpToken);
    // Transfer all LP tokens to this contract
    // Now they're locked forever
  }

  // Distribution functions exist (claim rewards)
  // But LP transfer functions don't exist
  // Result: LP cannot leave contract

  function claimRewards() public returns (uint) {
    // Claim your fee share
    // But don't touch the LP tokens
  }

  // NO withdrawLP() function
  // NO removeLiquidity() function
  // NO transfer() function for LP
  // Immutable: Cannot add functions later
}
```

**Proof of lock**:
- Code verified on Etherscan/Basescan
- No withdrawal function exists
- Constructor transfers LP
- Contract immutable (no upgrade proxy)
- Result: LP locked mathematically

### Fee Tracking

Opals tracks LP ownership for fee distribution:

```
mapping(address => uint) public patronPower;
mapping(address => uint) public claimedFees;

// When fees arrive from trading
feesAccumulated += 0.1 ETH;

// When holder claims their share
holderFeeShare = (holderPatronPower / totalPatronPower) × feesAccumulated;
transfer(holder, holderFeeShare);
```

## Gas Costs

**Creating Uniswap pair**: ~180k gas (one-time)
- At $30 gas: ~$5.40
- At $5 gas (L2): ~$0.90

**Adding liquidity**: ~150k gas (one-time initial add)
- At $30 gas: ~$4.50
- At $5 gas (L2): ~$0.75

**Removing liquidity**: ~120k gas (would-be, but LP locked)
- Prevented by smart contract

## Real-World Example: Project Token Launch

**Project**: DeFi yield aggregator

**LP token scenario**:

**Initial Setup**:
- 1,000 ETH + 50M YIELD tokens locked in Uniswap
- LP tokens minted: 7,071
- Value: $1.5M (1,000 × $1,500) + (50M × $0.01) = $2M
- All LP locked in PatronClaim forever
- Proof: Code verified, no withdrawal function

**Year 1 - Successful Launch**:
- Daily volume: $20M average
- Monthly fees: ~$6M (1% of $600M monthly volume)
- LP token appreciation: $2M → $6M (from reserve growth + token price $0.01 → $0.09)
- Holder with 1% of LP:
  - LP value growth: $6M × 1% = $60k
  - Fee income: $6M × 1% × 12 = $72k
  - Total: $132k from $20k initial investment

**Year 2 - Growing Ecosystem**:
- Daily volume: $50M average
- Monthly fees: ~$15M
- LP value: $15M (from continued growth)
- Holder with 1% continues earning:
  - Fee income: $15M × 1% × 12 = $1.8M annually
  - Plus LP appreciation

**Permanent lock guarantee**:
- 7,071 LP tokens locked at Day 1
- Still locked at Year 5: Unchanged
- Still locked at Year 100: Forever
- Rug pull: Mathematically impossible
- Founder cannot withdraw: Code prevents it

## Comparison: LP Tokens vs Other Ownership

| Aspect | LP Tokens (Opals) | VC Equity | Bonds |
|--------|------------------|----------|-------|
| Lock | Permanent | N/A (resellable) | Fixed term |
| Fee share | 1% trading fees | Dividends (rare) | Interest payments |
| Rug risk | Zero (locked) | High (can dump) | Issuer default |
| Liquidity | Tradeable anytime | Illiquid (5-10 yrs) | Market-dependent |
| Governance | Possible (future) | Yes (board seats) | No |
| Sustainability | Real usage-based | Diluted by rounds | Fixed payments |

## Navigation: Understanding LP Economics

**Question**: What exactly do I own with LP tokens?
- Answer: Fractional ownership of a trading pair
- Next: [Staking](./staking.md) - Lock LP for higher rewards

**Question**: Can the liquidity be removed?
- Answer: No. Permanently locked by contract code.
- Next: [Why-Opals](../overview/why-opals.md) - Security model

**Question**: How do I earn from LP tokens?
- Answer: Trading fees distributed pro-rata based on PatronPower
- Next: [Distributor](./distributor.md) - Fee distribution mechanism

**Question**: Can I sell my LP tokens?
- Answer: Yes, on secondary markets. Economic rights transfer with tokens.
- Next: [Markets](./markets.md) - Trading mechanisms

## Next Steps

- **[Distributor](./distributor.md)** - How fees get distributed from LP
- **[Staking](./staking.md)** - Lock LP tokens to earn rewards
- **[Tokens](./tokens.md)** - Project token paired with ETH in LP
