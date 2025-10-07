# Pricing and Economics: Complete Cost Breakdown

This guide shows exactly what launching on Opals costs. Every number is verifiable in the smart contracts. No hidden fees.

## The Simple Version

**Platform fee**: 2% of ETH raised

**Gas costs**: Approximately $15 for deployment

**That's it.** No setup fees, no monthly costs, no hidden charges.

## Platform Fee Breakdown

The 2% fee is hardcoded in the smart contracts and distributed transparently:

**Fee split**:
- 50% to token creator (you)
- 20% to protocol treasurym bn  bb nb n nm                                                                                      met 1% of your raise back as the creator fee. Your net cost is 1% plus gas.

### How Fee Collection Works

Fees are collected during NFT mints:

When a supporter mints a Patron Card for 1 ETH:
- 0.98 ETH goes to your project
- 0.02 ETH goes to fee distribution

Fee distribution happens automatically. No manual processing needed.

### Fee Verification

The 2% fee is defined in SteppedMarket.sol, FixedMarket.sol, and MembersMarket.sol as a constant:

`TOTAL_FEE_BPS = 200` (200 basis points = 2%)

This cannot be changed. It's immutable.

## Gas Cost Breakdown

Deployment uses EIP-1167 minimal proxy pattern. You pay gas only for creating contract clones, not full deployments.

**Approximate gas usage**:
- Project contract: 150,000 gas
- Token contract: 150,000 gas
- Operator contract: 100,000 gas
- Card contract: 150,000 gas
- Market contract: 200,000 gas
- PatronClaim contract: 200,000 gas
- LiquidityLauncher contract: 150,000 gas

**Total**: Approximately 1,100,000 gas

**Cost at different gas prices**:
- 10 gwei: $4.40 (at $2,000 ETH)
- 20 gwei: $8.80
- 50 gwei: $22.00
- 100 gwei: $44.00

Average deployment: $15 at typical gas prices.

### Gas Savings vs Traditional

Traditional deployment without templates:
- Full ERC20 deployment: 1,200,000 gas
- Full ERC721 deployment: 2,500,000 gas
- Full market contract: 800,000 gas
- Full staking contract: 1,500,000 gas

**Traditional total**: 6,000,000 gas minimum

**Traditional cost at 20 gwei**: $240

**Opals cost at 20 gwei**: $8.80

**Savings**: 96.3%

## Three Cost Scenarios

### Small Project: $100k Raise

**Scenario**: Community-focused DeFi project raising $100k

**Platform fee**: $100,000 × 2% = $2,000
**Creator rebate**: $100,000 × 1% = $1,000
**Net platform cost**: $1,000

**Gas costs**: $15

**Total cost**: $1,015

**Cost as percentage**: 1.015%

**Compare to alternatives**:
- VC funding: Would take $20,000-$40,000 in equity value (20-40%)
- Other launchpads: Would charge $10,000-$20,000 (10-20%)
- DIY launch: $240 gas + weeks of dev time + security risk

**Savings vs VC**: $19,000-$39,000
**Savings vs launchpads**: $9,000-$19,000

### Medium Project: $500k Raise

**Scenario**: Gaming platform with established community

**Platform fee**: $500,000 × 2% = $10,000
**Creator rebate**: $500,000 × 1% = $5,000
**Net platform cost**: $5,000

**Gas costs**: $15

**Total cost**: $5,015

**Cost as percentage**: 1.003%

**Compare to alternatives**:
- VC funding: Would take $100,000-$200,000 in equity value
- Other launchpads: Would charge $50,000-$100,000
- DIY launch: $240 gas + months of dev time + security risk

**Savings vs VC**: $95,000-$195,000
**Savings vs launchpads**: $45,000-$95,000

### Large Project: $5M Raise

**Scenario**: DeFi protocol with significant traction

**Platform fee**: $5,000,000 × 2% = $100,000
**Creator rebate**: $5,000,000 × 1% = $50,000
**Net platform cost**: $50,000

**Gas costs**: $15

**Total cost**: $50,015

**Cost as percentage**: 1.0003%

**Compare to alternatives**:
- VC funding: Would take $1M-$2M in equity value
- Other launchpads: Would charge $500k-$1M
- DIY launch: $240 gas + months of dev time + significant security risk

**Savings vs VC**: $950,000-$1,950,000
**Savings vs launchpads**: $450,000-$950,000

## ROI Calculations

### Conservative Scenario

**Assumptions**:
- Raise $500k
- Token launches at $0.001
- Price 2x within 6 months
- You allocated 30% to team (150M tokens)

**Your costs**: $5,015

**Your token value at launch**: 150M × $0.001 = $150,000

**Your token value at 2x**: 150M × $0.002 = $300,000

**ROI**: 300,000 / 5,015 = 59.8x on your initial investment

**Compare**: VC would have taken 20-40% equity, leaving you with $300k-$400k instead of $500k raised plus $300k in tokens.

### Moderate Scenario

**Assumptions**:
- Raise $500k
- Token launches at $0.001
- Price 5x within 6 months
- You allocated 30% to team

**Your costs**: $5,015

**Your token value at 5x**: 150M × $0.005 = $750,000

**ROI**: 750,000 / 5,015 = 149.5x

**Total value to project**: $500k raised + $750k token value = $1.25M

**VC alternative**: Would have taken $100k-$200k upfront, leaving you with only 60-80% control

### Optimistic Scenario

**Assumptions**:
- Raise $500k
- Token launches at $0.001
- Price 10x within 6 months
- You allocated 30% to team

**Your costs**: $5,015

**Your token value at 10x**: 150M × $0.01 = $1,500,000

**ROI**: 1,500,000 / 5,015 = 299x

**Total value to project**: $500k raised + $1.5M token value = $2M

**VC alternative**: Would have taken significant equity and board control

**Note**: These are illustrative scenarios. Token price performance depends on execution, market conditions, and many other factors. Past performance does not indicate future results.

## Token Allocation Best Practices

The most successful projects allocate tokens strategically:

### Recommended Allocation

**40% to Liquidity Pool**:
- Ensures deep liquidity on Uniswap
- Reduces slippage for traders
- Creates stable price floor
- Locked permanently (unruggable)

**30% to Reward Distribution**:
- Funds PatronClaim rewards
- Rewards long-term supporters
- Creates sustainable yield
- Distributed over time

**30% to Team and Development**:
- Funds ongoing development
- Compensates team
- Enables strategic partnerships
- Optional vesting for credibility

### Why This Works

**Deep liquidity** attracts traders. More volume means more fees, which can fund ongoing rewards.

**Substantial rewards** create loyalty. Supporters become evangelists when they earn consistently.

**Adequate team allocation** funds execution. You need resources to build what you promised.

### Alternative Allocations

Some projects use different splits:

**Conservative** (50% LP, 25% rewards, 25% team):
- Deepest liquidity
- Lower reward yield
- Smaller team allocation

**Aggressive** (30% LP, 35% rewards, 35% team):
- Higher reward yield
- More team resources
- Less initial liquidity

**Community-focused** (35% LP, 45% rewards, 20% team):
- Maximum supporter rewards
- Strong community alignment
- Smaller team allocation

Choose based on your priorities.

## Hidden Costs to Consider

While Opals costs are transparent, factor in these related expenses:

### Marketing and Community Building

**Essential**:
- Website development: $500-$5,000
- Social media presence: Free-$1,000
- Community tools (Discord bots, etc.): $50-$200/month

**Recommended**:
- Paid advertising: $1,000-$10,000
- Influencer partnerships: $500-$5,000
- Content creation: $500-$3,000

**Total typical marketing budget**: $3,000-$25,000

### Team Time Investment

**Pre-launch**: 10-20 hours for tokenomics design, marketing, community building

**Launch week**: 10-15 hours for monitoring, engagement, support

**Post-launch**: 5-10 hours weekly for ongoing management

Value this time appropriately. Founder time is valuable.

### Ongoing Operations

**After launch, budget for**:
- Community management: $2,000-$5,000/month
- Marketing: $1,000-$10,000/month
- Development: $10,000-$50,000/month
- Reward token purchases: Varies based on performance

These costs are not Opals-specific. Every project needs these resources.

## Fee Comparison Matrix

| Provider | Upfront Fee | Success Fee | Equity Taken | Timeline | Support |
|----------|-------------|-------------|--------------|----------|---------|
| **Opals** | $15 gas | 2% of raise (1% net) | 0% | 1 week | Full |
| **CoinList** | $50k-$100k | 10-15% | 0-2% | 2-3 months | Limited |
| **Polkastarter** | $10k-$30k | 5-10% | 0-1% | 1-2 months | Limited |
| **VC Funding** | $0 | 0% | 20-40% | 6+ months | Strategic |
| **DIY Uniswap** | $240 gas | 0% | 0% | Weeks-months | None |

**Opals advantage**: Lowest total cost, fastest timeline, full support, zero equity.

## When Opals Makes Sense

### Ideal For

**Community-first projects**: You have an engaged audience that wants to support you.

**Capital-efficient launches**: You need funds without giving up equity.

**Speed-focused founders**: You want to launch quickly without months of VC meetings.

**Transparent projects**: You're comfortable with on-chain verification and public contracts.

### Less Ideal For

**Projects with zero community**: Build audience first, then raise funds.

**Projects needing strategic VC value**: If you need VC expertise more than capital, traditional funding may be better.

**Projects unable to ship**: If you can't execute on your roadmap, don't raise funds.

**Projects avoiding transparency**: All contracts are open source and verifiable.

## Financial Planning

### Budget Template

**Raise target**: $________
**Platform fee (2%)**: $________
**Creator rebate (1%)**: $________
**Net platform cost (1%)**: $________
**Gas costs**: $15

**Total Opals cost**: $________ + $15

**Marketing budget**: $________
**Team time value**: $________
**Ongoing operations**: $________ / month

**Total capital needed**: $________

**Capital available after raise**: (Raise - Net Platform Cost - Marketing - 6 months operations)

### Runway Calculation

**Example**: Raise $500k
- Platform cost: $5,015
- Marketing: $10,000
- Operations: $15,000/month

**Runway**: ($500,000 - $5,015 - $10,000) / $15,000 = 32 months

This assumes you use 100% of raised funds for operations. Most projects allocate differently.

### Token Value Inclusion

If you allocate 30% of supply to team and price appreciates:

**At launch**: 150M tokens × $0.001 = $150,000
**At 2x**: 150M tokens × $0.002 = $300,000
**At 5x**: 150M tokens × $0.005 = $750,000

This significantly extends runway if you choose to sell team tokens strategically.

## Tax Considerations

Consult a tax professional. Generally:

**Token sales**: May be taxable as income when received.

**Platform fees**: Deductible as business expenses.

**Team token allocations**: May create taxable events on vest or sale.

**Rewards distributed**: May be deductible as incentive payments.

Tax treatment varies by jurisdiction. Get professional advice.

## Common Questions

**Q: Can the 2% fee ever change?**
A: No. It's hardcoded as a constant in the smart contracts. Immutable.

**Q: Are there discounts for larger raises?**
A: No. 2% applies regardless of size. But your effective cost drops (1% net after creator rebate).

**Q: Do I pay gas for my supporters' mints?**
A: No. Each supporter pays their own gas when minting. You only pay deployment gas.

**Q: What if my raise fails to meet minimum?**
A: Supporters can reclaim their ETH. You lose only the $15 deployment gas.

**Q: Are there ongoing fees?**
A: No. You pay once at launch. No monthly or recurring fees.

## Next Steps

Ready to calculate your specific costs?

**Simple formula**:
- Take your raise target
- Multiply by 1% (net after creator rebate)
- Add $15 gas
- Add marketing budget
- Result: Your total launch cost

**Example**: $300k raise
- $300,000 × 1% = $3,000
- Plus $15 gas
- Plus $5,000 marketing
- Total: $8,015 to launch

Compare that to:
- VC taking 20-30% equity worth $60k-$90k
- Other launchpads charging $30k-$60k
- DIY costing months of time plus security risk

[Start your launch](./launch-process.md) →

[Compare to alternatives](./competitive-advantages.md) →

[View success stories](./success-stories.md) →

---

**Remember**: Transparency is core to Opals. Every fee is verifiable on-chain. Every cost is disclosed upfront. No surprises.
