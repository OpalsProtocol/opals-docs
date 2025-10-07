# Understanding Patron Cards: Your Share of the Liquidity Pool

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

## Pricing Mechanics: Stepped Batch System

Patron Cards don't have a fixed price. They use stepped pricing, where each batch costs more than the last.

### How Stepped Pricing Works

**Batch structure**: Projects divide Patron Card sales into batches. Common setup:

- Batch 1: Cards 1-10 at 0.50 ETH each
- Batch 2: Cards 11-20 at 0.55 ETH each (+10%)
- Batch 3: Cards 21-30 at 0.605 ETH each (+10%)
- And so on...

**Progressive pricing**: Early supporters pay less. Later supporters pay more. This rewards those who invest before the project is proven.

**Batch size**: Projects choose batch size (5, 10, 25, etc.). Smaller batches = faster price increases. Larger batches = more time at each price level.

**Price increment**: Projects choose increment percentage (5%, 10%, 15%, etc.). Higher increments = steeper price curve.

### Why Stepped Pricing?

**Bot resistance**: Bots profit from information advantages and speed. Stepped pricing eliminates time-based advantages. Everyone in the same batch pays the same price regardless of when they buy.

**Fair distribution**: No gas wars. No frontrunning. No special deals for insiders. Transparent pricing for everyone.

**Early supporter rewards**: Those who believe in projects before they're proven get better prices. Risk and reward align properly.

**Progressive funding**: Projects can gauge demand at each price level. Supporters can see real-time validation as batches sell out.

### Calculating Your Effective Price

Your effective cost per LP token depends on which batch you buy in:

**Example scenario**:
- Total raise: 100 ETH
- LP allocation: 40 ETH (40%)
- Total cards: 100
- You buy 1 card in batch 1 for 0.5 ETH
- You buy 1 card in batch 5 for 0.732 ETH

**Your LP allocation**:
- Total invested: 1.232 ETH
- Your share: 1.232 / 100 = 1.232%
- Your LP value: 40 ETH × 1.232% = 0.493 ETH worth of LP

**Your effective price**: Paid 1.232 ETH for 0.493 ETH worth of LP = 2.5x premium

**Where premium goes**:
- 40% allocated to LP (your 0.493 ETH)
- 30% to reward pools
- 30% to team/development
- 2% platform fee

So you're not just buying LP. You're funding the entire project ecosystem.

## ROI Scenarios: Three Real Examples

Let's model realistic returns across different scenarios.

### Scenario 1: Small Success

**Project**: Community-focused DeFi tool
**Raise**: 100 ETH
**Your investment**: 1 ETH in batch 1
**Your LP allocation**: 0.4 ETH worth of LP tokens

**6 months later**:
- Token 2x from launch
- Average daily volume: $50,000
- Daily trading fees: $500 (1% custom fee)
- Your share (1% PatronPower): $5/day = $1,825 over 6 months

**LP value**: Your LP contains ETH + tokens. With 2x token appreciation, LP worth approximately 1.41x = 0.565 ETH

**Protocol fees**: Project generated $5,000 in protocol fees over 6 months. Your 1% PatronPower share = $50

**Total value**: 0.565 ETH + $547.50 fees + $50 protocol = ~1.162 ETH equivalent

**ROI**: 16.2% in 6 months, or 32% annualized

### Scenario 2: Moderate Success

**Project**: Gaming platform with active community
**Raise**: 100 ETH
**Your investment**: 1 ETH in batch 2 (0.55 ETH)
**Your LP allocation**: 0.4 ETH worth of LP tokens (0.4% of total)

**12 months later**:
- Token 5x from launch
- Average daily volume: $200,000
- Daily trading fees: $2,000 (1% custom fee)
- Your share (0.4% PatronPower): $8/day = $2,920 over 12 months

**LP value**: With 5x token appreciation, LP worth approximately 2.236x = 0.894 ETH

**Protocol fees**: Project generated $20,000 in protocol fees over 12 months. Your 0.4% share = $80

**Total value**: 0.894 ETH + $876 fees + $80 protocol = ~1.95 ETH equivalent

**ROI**: 255% in 12 months (paid 0.55 ETH, now worth 1.95 ETH)

### Scenario 3: Major Success

**Project**: Innovative DeFi protocol with strong adoption
**Raise**: 100 ETH
**Your investment**: 2 ETH across batch 1 and batch 3
**Your LP allocation**: 0.8 ETH worth of LP tokens (0.8% of total)

**24 months later**:
- Token 10x from launch
- Average daily volume: $1,000,000 (growing protocol)
- Daily trading fees: $10,000 (1% custom fee)
- Your share (0.8% PatronPower): $80/day = $58,400 over 24 months

**LP value**: With 10x token appreciation, LP worth approximately 3.16x = 2.528 ETH

**Protocol fees**: Project generated $100,000 in protocol fees over 24 months. Your 0.8% share = $800

**Total value**: 2.528 ETH + $17,520 fees + $800 protocol = ~20.848 ETH equivalent

**ROI**: 942% over 24 months, or 471% annualized (paid 2 ETH, now worth 20.848 ETH)

**Note**: These scenarios illustrate possibilities. Actual returns depend on project execution, market conditions, and countless other factors. Many projects will underperform these examples. Some will exceed them. Past performance does not indicate future results.

## Secondary Market Dynamics

After launch, Patron Cards can trade on NFT marketplaces like OpenSea.

### Factors Affecting Secondary Market Price

**1. Underlying LP value**: What are the LP tokens worth right now?

**2. Expected future fees**: What's the trading volume trend? Increasing or decreasing?

**3. Protocol fee projections**: Is the project generating meaningful protocol fees?

**4. Project fundamentals**: Team executing on roadmap? Community growing? Product working?

**5. Market sentiment**: Bull market vs bear market affects all crypto prices.

**6. Liquidity**: Are there buyers? Can you actually sell if you want to?

### Premium to LP Value

Patron Cards often trade at a premium to underlying LP value because of:

**Future fee income**: Buyers pay for expected future trading fees, not just current LP value.

**PatronPower multiplier**: 10x multiplier makes Patron Cards more valuable than equivalent LP stakes elsewhere.

**Permanence**: LP locked forever guarantees long-term fee income.

**Scarcity**: Fixed supply of Patron Cards per project.

**Example**: Your LP tokens worth 1 ETH. Trading volume generates 20% annual yield on LP value. Rational buyer might pay 1.5-2 ETH for your Patron Card to capture that yield stream.

### Discount to LP Value

Sometimes Patron Cards trade below LP value because of:

**Low volume**: If trading volume is minimal, future fees look bad. Buyer discounts accordingly.

**Project concerns**: Team not executing, community shrinking, product failing.

**Liquidity needs**: If you need to sell quickly and there are few buyers, you may accept a discount.

**Market conditions**: Bear markets drive all prices down.

**Example**: Your LP tokens worth 1 ETH. Trading volume is near zero. Project seems abandoned. Best offer might be 0.5 ETH.

### When to Sell

**Consider selling when**:
- Project fundamentals deteriorating
- Found better opportunity elsewhere
- Need liquidity for emergencies
- Hit your target return
- Risk tolerance changed

**Consider holding when**:
- Project executing well
- Trading volume growing
- Community expanding
- You believe in long-term vision
- Tax implications favor holding

There's no universal right answer. It depends on your situation and goals.

## Comparing Patron Cards vs Direct LP Provision

You could bypass Patron Cards entirely and just provide liquidity to Uniswap yourself after launch. Why buy Patron Cards instead?

### Advantages of Patron Cards

**1. Better pricing**: You get LP tokens at pre-launch prices, often better than post-launch market prices.

**2. PatronPower multiplier**: 10x multiplier means you earn far more from protocol fee distributions than regular stakers.

**3. Supporting project**: Your funds help project launch. You're not just speculating on an existing pool.

**4. Early access**: Get in before public market. Higher risk but potentially higher rewards.

### Advantages of Direct LP Provision

**1. Liquidity**: You can remove liquidity anytime (subject to impermanent loss). Patron Cards lock LP forever.

**2. Lower risk**: Only provide liquidity to projects that already proved viability.

**3. No launch risk**: You don't risk project failing to reach funding threshold.

**4. Flexibility**: Can exit quickly if project looks bad.

### Which Is Better?

**Choose Patron Cards if**:
- You believe in project long-term
- You want maximum rewards via PatronPower
- You're comfortable with permanent lock
- You want best possible entry price

**Choose direct LP if**:
- You want flexibility to exit
- You prefer lower risk
- You're unsure about long-term commitment
- You want to wait for project to prove itself

Many investors do both: Buy Patron Cards for projects they deeply believe in, provide direct LP for others they like but aren't certain about.

## Understanding Impermanent Loss

Patron Cards contain LP tokens. LP tokens are subject to impermanent loss. You need to understand this.

### What Is Impermanent Loss?

When you provide liquidity, you deposit equal values of two assets (ETH and project token). If their relative prices change significantly, you end up with less total value than if you'd just held both assets separately.

**Example**:
- You provide 1 ETH + 1,000 tokens (both worth $2,000, so 1 token = $2)
- Total value: $4,000
- Token 4x to $8
- Uniswap rebalances: You now have less tokens, more ETH
- Your LP now worth ~$6,400
- But if you'd just held 1 ETH + 1,000 tokens: Worth $2,000 + $8,000 = $10,000
- Impermanent loss: $3,600 (36%)

### Why "Impermanent"?

If token price returns to original ratio, the loss disappears. It's only "permanent" if you withdraw at a different ratio.

### Does This Affect Patron Cards?

Yes. Your Patron Card LP value is subject to impermanent loss.

**Good news**: Trading fees offset impermanent loss. High-volume pools often generate enough fees to overcome impermanent loss.

**Better news**: You also earn protocol fee rewards via PatronPower, providing additional income beyond trading fees.

**Reality**: Some projects will generate enough fees to beat impermanent loss. Others won't. This is part of the risk.

### Minimizing Impermanent Loss Impact

**Choose projects with**:
- High expected trading volume (more fees)
- Relatively stable token prices (less impermanent loss)
- Strong fundamentals (sustainable growth)

**Understand that**:
- 2x price moves = small impermanent loss (~5.7%)
- 5x price moves = moderate impermanent loss (~25.5%)
- 10x price moves = large impermanent loss (~42.3%)

Even with impermanent loss, your total value still increases with price appreciation. You just would have made more by holding tokens directly.

## Tax Implications

Consult a tax professional. Generally:

**Buying Patron Cards**: May be taxable event if using appreciated crypto to buy.

**Receiving LP tokens**: May trigger taxable income at fair market value.

**Claiming rewards**: Usually taxable as income when claimed.

**Selling Patron Cards**: Capital gains tax on difference between purchase price and sale price.

**Trading fee income**: Accrues to LP value, taxable when you sell or withdraw.

Tax treatment varies wildly by jurisdiction. Get professional advice for your situation.

## Common Questions

**Q: Can I sell my Patron Card before launch completes?**
A: Yes, on secondary markets. But buyer assumes risk of project not reaching threshold.

**Q: What happens to my Patron Card if project fails to launch?**
A: You can reclaim your ETH. The Patron Card becomes worthless.

**Q: Can I convert my Patron Card back to ETH after launch?**
A: Not directly. You can sell the Patron Card on secondary markets for ETH.

**Q: How do I claim my LP tokens?**
A: After launch, go to Opals dashboard, connect wallet, click "Claim LP tokens" on your Patron Card. Approve transaction.

**Q: Can I stake my LP tokens after claiming?**
A: Yes. Stake them in VaultClaim contracts to earn multiplied rewards based on lock duration.

**Q: How often are trading fees distributed?**
A: Continuously. Every trade adds fees to the pool immediately. Your LP value updates in real-time.

**Q: How do I claim protocol fee rewards?**
A: Go to Opals dashboard, view your Patron Card, click "Claim Rewards", approve transaction.

**Q: Can the project remove liquidity?**
A: No. LP tokens are permanently locked in PatronClaim contract. Code verified. No admin keys.

**Q: What if the team abandons the project?**
A: LP remains locked. Trading continues. Fees continue accruing. Project abandonment doesn't affect core LP economics. But token value likely suffers if no development.

## Next Steps

Now that you understand Patron Cards:

**Learn about staking rewards**:
[Staking rewards guide](./staking-rewards-guide.md) →

**Assess your risks**:
[Risk management guide](./risk-management.md) →

**Optimize your returns**:
[Maximizing returns strategies](./maximizing-returns.md) →

**Ready to invest?**:
[Getting started guide](./getting-started.md) →

---

**Remember**: Patron Cards represent real economic value through LP token ownership. They generate income through trading fees and protocol rewards. But they also carry risks including impermanent loss, project failure, and market volatility. Invest responsibly.
