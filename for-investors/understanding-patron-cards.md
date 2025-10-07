# Understanding Patron Cards

Patron Cards represent your ownership stake in a project's Uniswap liquidity pool. This guide explains what they are, how they work, and how they generate returns.

## What Are Patron Cards?

Patron Cards are collectible digital certificates (NFTs) that represent your share of a project's permanent liquidity pool.

<figure><img src="../.gitbook/assets/Screenshot 2025-02-03 at 6.21.21 PM.png" alt="Patron Cards Examples"><figcaption><p>Some illustrative examples (non affiliated)</p></figcaption></figure>

**Simple analogy**: Imagine a project creates a Uniswap pool with $100,000 liquidity. You buy a Patron Card representing 1% ownership. You now own $1,000 of that liquidity permanently, and you earn from every trade forever.

**Technical truth**: Each Patron Card entitles you to claim a specific amount of LP (liquidity provider) tokens. These LP tokens represent your fractional ownership of the ETH-Token pair on Uniswap.

**Key difference from regular NFTs**: Most NFTs are just collectible art. Patron Cards are ownership certificates with real economic value tied to trading activity.

## Economic Rights: What You Actually Own

When you buy a Patron Card, you gain three forms of economic rights:

### 1. LP Token Allocation

**What it is**: A permanent claim on a portion of the project's Uniswap liquidity pool.

**Value source**: The LP tokens contain both ETH and project tokens. As trading happens and fees accumulate, your LP value grows.

**Permanence**: Once allocated, these LP tokens are locked forever. The project can never remove liquidity, and neither can you withdraw the underlying tokens directly.

**Example**: You buy a Patron Card for 1 ETH during the launch. Project raises 100 ETH total and allocates 40 ETH worth of liquidity to Patron Card holders. You own 1/100 = 1% of that liquidity = 0.4 ETH worth of LP tokens.

### 2. Trading Fee Income

**What it is**: Opals uses a custom Uniswap V2 fork that charges 1% per swap (not the standard 0.3%). LP token holders receive this fee, which is distributed to the Distributor contract for PatronPower-weighted rewards.

**How it works**: Fees go to the feeReceiver (Distributor contract) which distributes them to PatronClaim and VaultClaim holders based on their PatronPower. This is in addition to the standard LP value appreciation.

**Calculation**: If $1,000,000 trades through the pool daily, that generates $10,000 in fees. If you own 1% of total PatronPower, you earn $100 daily = $36,500 annually.

**Variability**: Trading volume fluctuates. Some days high, some days low. Average over time for realistic expectations.

### 3. Protocol Fee Rewards

**What it is**: Projects on Opals pay a 2% platform fee on sales. Part of this flows to PatronClaim holders as rewards.

**Distribution**: Based on PatronPower, not just LP token amount. Patron Cards have a 10x multiplier, giving you 10 times the power of an equivalent staker with minimal lock period.

**Frequency**: Distributed as projects accumulate fees. Claim anytime.

**Example**: Project generates $10,000 in protocol fees monthly. You hold a Patron Card with 5% of total PatronPower. You earn $500 monthly in protocol fee distributions.

## How PatronPower Works

PatronPower determines your share of rewards. It's calculated based on:

**LP token amount**: How much liquidity you own
**Lock duration**: How long you've held your position
**Commitment bonus**: Additional rewards for long-term holders
**Card multiplier**: Patron Cards get 10x multiplier

**Formula**: PatronPower = (LP tokens × lock duration × commitment bonus) × card multiplier

**Example**: You hold 1% of LP tokens for 1 year with 2x commitment bonus and Patron Card multiplier:
PatronPower = (1% × 365 days × 2) × 10 = 7,300 points

## The Permanent Lock: Why It Matters

### What "Permanent" Means

**No withdrawal function**: The PatronClaim contract has no function to withdraw LP tokens. This is hardcoded and immutable.

**No admin override**: Even the project creators cannot remove liquidity. No admin keys exist.

**No time limit**: Not locked for 6 months or 2 years. Locked forever.

**Mathematical guarantee**: The liquidity cannot be removed by anyone, ever.

### Why This Protects You

**Rug pull protection**: Projects cannot remove liquidity and run away with your money.

**Permanent value**: Your investment is protected from project failure or bad actors.

**Sustainable rewards**: Trading fees continue flowing as long as the pool exists.

**Community alignment**: Projects are incentivized to build long-term value.

## Understanding the Value Proposition

### What You're Buying

**Not just a token**: You're buying a permanent stake in a project's liquidity.

**Not just an NFT**: You're buying an ownership certificate with real economic value.

**Not just a collectible**: You're buying a revenue-generating asset.

### What You're Not Buying

**Not equity**: You don't own shares in the company.

**Not governance**: You don't vote on project decisions.

**Not control**: You can't influence project direction.

**Not guarantees**: The project might still fail.

## How to Evaluate Patron Cards

### Project Quality

**Team**: Who are the founders? What's their track record?

**Product**: What are they building? Does it solve real problems?

**Community**: How engaged is the community? How many supporters?

**Traction**: Do they have users? Revenue? Partnerships?

### Economic Factors

**Total supply**: How many Patron Cards are being sold?

**Pricing**: Is the price reasonable for the value proposition?

**Allocation**: What percentage of tokens goes to liquidity?

**Fees**: What percentage of trading fees do you receive?

### Market Conditions

**Timing**: Is this a good time to invest in this type of project?

**Competition**: How does this project compare to competitors?

**Trends**: Are there broader market trends affecting this sector?

**Risk**: What are the main risks to this investment?

## Common Misconceptions

### "It's Just an NFT"

**Reality**: Patron Cards are ownership certificates with real economic value.

**Why it matters**: Unlike most NFTs, Patron Cards generate ongoing income.

### "I Can Withdraw My Liquidity"

**Reality**: LP tokens are locked permanently. You cannot withdraw them.

**Why it matters**: This protects you from rug pulls but limits your flexibility.

### "I Own the Project"

**Reality**: You own a share of the liquidity pool, not the project itself.

**Why it matters**: You benefit from trading activity, not project success directly.

### "It's Guaranteed to Make Money"

**Reality**: All investments carry risk. You can lose money.

**Why it matters**: Only invest what you can afford to lose.

## Risk Factors

### Project Risk

**Execution risk**: The project might fail to deliver on promises.

**Team risk**: Key team members might leave or be replaced.

**Market risk**: The market might not want what they're building.

**Competition risk**: Competitors might build better solutions.

### Technical Risk

**Smart contract risk**: Bugs in the code could cause losses.

**Network risk**: Ethereum network issues could affect operations.

**Upgrade risk**: Protocol upgrades could change the rules.

**Integration risk**: Third-party integrations could fail.

### Market Risk

**Token price risk**: The project token price could go down.

**Trading volume risk**: Low trading volume means lower fees.

**Liquidity risk**: Low liquidity could make trading difficult.

**Regulatory risk**: New regulations could affect the project.

## Maximizing Your Returns

### Choose Quality Projects

**Research thoroughly**: Understand what you're investing in.

**Check the team**: Look for experienced, credible founders.

**Evaluate the product**: Make sure it solves real problems.

**Assess the community**: Strong communities drive success.

### Hold Long-Term

**PatronPower grows**: Longer holds mean higher rewards.

**Compound returns**: Reinvest rewards for exponential growth.

**Avoid panic selling**: Don't sell during temporary dips.

**Stay informed**: Keep up with project developments.

### Diversify Your Portfolio

**Don't put all eggs in one basket**: Spread risk across multiple projects.

**Different sectors**: Invest in different types of projects.

**Different stages**: Mix early-stage and established projects.

**Different risk levels**: Balance high-risk and low-risk investments.

## Next Steps

Ready to start investing?

1. **[Getting Started](./getting-started.md)** - Set up your wallet and make your first purchase
2. **[Staking & Rewards Guide](./staking-rewards-guide.md)** - Learn how to maximize your returns
3. **[Risk Management](./risk-management.md)** - Protect your investment
4. **[Maximizing Returns](./maximizing-returns.md)** - Advanced strategies

---

**Remember**: Patron Cards are a new type of investment. They offer unique benefits but also carry unique risks. Take time to understand what you're buying and only invest what you can afford to lose.