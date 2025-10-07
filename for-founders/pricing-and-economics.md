# Pricing and Economics

This guide shows exactly what launching on Opals costs. Every number is verifiable in the smart contracts. No hidden fees.

## The Simple Version

**Platform fee**: 2% of ETH raised

**Gas costs**: Approximately $15 for deployment

**That's it.** No setup fees, no monthly costs, no hidden charges.

## Platform Fee Breakdown

The 2% fee is hardcoded in the smart contracts and distributed transparently:

**Fee split**:
- 50% to token creator (you)
- 20% to protocol treasury
- 15% to platform referrer
- 15% to order referrer

**Net cost to you**: 1% of your raise back as the creator fee. Your net cost is 1% plus gas.

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

**Total gas**: ~1,100,000 gas

**At 20 gwei and $2,000 ETH**: ~$15 total

**At 50 gwei and $2,000 ETH**: ~$35 total

**At 100 gwei and $2,000 ETH**: ~$70 total

## Cost Comparison

### Opals vs Traditional Deployment

**Traditional deployment**:
- Full contract deployment: ~5,000,000 gas per contract
- 7 contracts: ~35,000,000 gas total
- At 20 gwei and $2,000 ETH: ~$500
- At 50 gwei and $2,000 ETH: ~$1,250
- At 100 gwei and $2,000 ETH: ~$2,500

**Opals deployment**:
- Minimal proxy clones: ~1,100,000 gas total
- At 20 gwei and $2,000 ETH: ~$15
- At 50 gwei and $2,000 ETH: ~$35
- At 100 gwei and $2,000 ETH: ~$70

**Savings**: 95%+ reduction in gas costs

### Opals vs VC Funding

**VC funding costs**:
- Legal fees: $50,000-$200,000
- Equity dilution: 20-40% of company
- Time cost: 6-12 months
- Ongoing obligations: Board meetings, reporting

**Opals costs**:
- Platform fee: 1% of raise
- Gas costs: ~$15
- Time cost: 1 week
- Ongoing obligations: None

**Example**: $2M raise
- VC cost: $100,000 legal + 30% equity ($600,000 value) = $700,000 total
- Opals cost: $20,000 platform fee + $15 gas = $20,015 total
- **Savings**: $680,000 + 30% equity retained

### Opals vs Other Launchpads

**Other launchpad costs**:
- Platform fee: 5-20% of tokens
- Upfront cost: $50,000-$500,000
- Legal fees: $10,000-$50,000
- Time cost: 2-8 weeks

**Opals costs**:
- Platform fee: 1% of raise
- Gas costs: ~$15
- Legal fees: $0 (standard contracts)
- Time cost: 1 week

**Example**: $1M raise
- Other launchpad: 10% tokens ($100,000 value) + $100,000 upfront + $25,000 legal = $225,000 total
- Opals: $10,000 platform fee + $15 gas = $10,015 total
- **Savings**: $215,000 + 10% tokens retained

## Real-World Examples

### Small Project ($100k raise)

**Opals cost**:
- Platform fee: $1,000 (1% of $100k)
- Gas cost: $15
- **Total**: $1,015

**VC alternative**:
- Legal fees: $50,000
- Equity dilution: 25% ($25,000 value)
- **Total**: $75,000

**Savings**: $74,000 + 25% equity retained

### Medium Project ($1M raise)

**Opals cost**:
- Platform fee: $10,000 (1% of $1M)
- Gas cost: $15
- **Total**: $10,015

**VC alternative**:
- Legal fees: $100,000
- Equity dilution: 30% ($300,000 value)
- **Total**: $400,000

**Savings**: $390,000 + 30% equity retained

### Large Project ($10M raise)

**Opals cost**:
- Platform fee: $100,000 (1% of $10M)
- Gas cost: $15
- **Total**: $100,015

**VC alternative**:
- Legal fees: $200,000
- Equity dilution: 35% ($3.5M value)
- **Total**: $3.7M

**Savings**: $3.6M + 35% equity retained

## Fee Structure Details

### Platform Fee (2%)

**Creator fee (50%)**: 1% of raise returned to you
**Protocol treasury (20%)**: 0.4% of raise for protocol development
**Platform referrer (15%)**: 0.3% of raise for platform growth
**Order referrer (15%)**: 0.3% of raise for order flow

### Gas Costs

**Deployment gas**: ~1,100,000 gas (~$15 at 20 gwei)
**Transaction gas**: ~65,000 gas per Patron Card mint (~$1 at 20 gwei)
**Claiming gas**: ~45,000 gas per reward claim (~$0.70 at 20 gwei)

### Additional Costs

**Legal fees**: $0 (standard contracts)
**Setup fees**: $0
**Monthly fees**: $0
**Hidden fees**: $0

## Cost Optimization

### Gas Optimization

**Deploy during low gas periods**: Gas costs vary significantly
**Use gas optimization tools**: MetaMask and other wallets show gas estimates
**Batch operations**: Some operations can be batched to save gas

### Fee Optimization

**Referrer programs**: Use referrer codes to reduce net costs
**Volume discounts**: Larger raises have better fee economics
**Efficient pricing**: Better pricing strategies reduce overall costs

## Transparency and Verification

### On-Chain Verification

**Fee structure**: All fees are defined in smart contracts
**Gas costs**: All gas costs are visible on block explorer
**No hidden fees**: Every cost is transparent and verifiable

### Community Verification

**Open source**: All code is publicly available
**Audit reports**: All contracts are audited and verified
**Community reviews**: Anyone can review and verify costs

## Common Questions

**Q: Are there any hidden fees?**
A: No. All fees are transparent and defined in smart contracts.

**Q: Can fees change after deployment?**
A: No. All fees are immutable once deployed.

**Q: What if gas prices are high?**
A: Gas costs are typically $15-$70 depending on network conditions.

**Q: Do I need to pay anything upfront?**
A: Only gas costs for deployment (~$15). Platform fees are collected during sales.

**Q: What if my project fails to raise funds?**
A: You only pay gas costs. No platform fees are charged if you don't raise funds.

**Q: Can I get a refund?**
A: Gas costs are non-refundable, but platform fees are only charged on successful raises.

## Best Practices

### Cost Management

**Plan your raise carefully**: Set realistic targets to avoid overpaying
**Optimize your pricing**: Better pricing strategies reduce overall costs
**Use referrer programs**: Take advantage of referrer discounts
**Monitor gas costs**: Deploy during low gas periods when possible

### Value Maximization

**Focus on value creation**: Build something people actually want
**Engage your community**: Strong communities raise more effectively
**Be transparent**: Transparency builds trust and reduces costs
**Deliver on promises**: Success reduces long-term costs

## Next Steps

Ready to launch your project?

1. **[Design your tokenomics](./pricing-and-economics.md)** - Plan your token distribution
2. **[Choose your market type](./choosing-market-type.md)** - Select the right mechanism
3. **[Deploy your project](./launch-process.md)** - Launch your token
4. **[Monitor your progress](./launch-checklist.md)** - Track your success

---

**Remember**: The cost of launching on Opals is transparent and minimal. Focus on building something great and let the economics work in your favor. The platform fee is small compared to the value you'll create.