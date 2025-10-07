# Choosing Your Market Type

Your market type determines how Patron Cards are sold. This decision affects pricing, FOMO dynamics, and community perception.

Three market types available: SteppedMarket, FixedMarket, and MembersMarket.

## Quick Comparison

| Feature | SteppedMarket | FixedMarket | MembersMarket |
|---------|---------------|-------------|---------------|
| **Pricing** | Increases per batch | Same for everyone | Variable or fixed |
| **Bot Resistance** | High | Medium | High |
| **FOMO Factor** | High | Medium | Very high |
| **Complexity** | Medium | Low | Medium |
| **Best For** | Most launches | Established projects | Exclusive clubs |
| **Fairness** | Early bird rewards | Equal access | Member-only |

**Most founders choose SteppedMarket**. It balances FOMO, fairness, and bot resistance.

<figure><img src="../.gitbook/assets/image (3).png" alt="Stepped Pricing Example"><figcaption></figcaption></figure>

## SteppedMarket: Batch-Based Pricing

### How It Works

Cards sell in batches. Price increases after each batch sells out.

**Example configuration**:
- Total supply: 100 cards
- Batch size: 10 cards
- Starting price: 0.5 ETH
- Price increment: 0.05 ETH per batch

**Resulting prices**:
- Batch 1 (cards 1-10): 0.50 ETH each
- Batch 2 (cards 11-20): 0.55 ETH each
- Batch 3 (cards 21-30): 0.60 ETH each
- ...
- Batch 10 (cards 91-100): 0.95 ETH each

**Total raised**: 70 ETH (approximately $140k at $2k ETH)

### Key Benefits

**Early bird advantage without bot dominance**: First supporters save money, but bots can't buy everything instantly because batch pricing removes urgency within each batch.

**Creates sustained FOMO**: As batches sell, latecomers see price increasing and feel urgency to buy now.

**Rewards commitment level**: Supporters who act fast get better prices. Higher prices later mean higher LP allocation and PatronPower weight.

**Psychological pricing power**: Watching batches sell out creates momentum. "Batch 7 is 80% sold!" drives action.

<figure><img src="../.gitbook/assets/image.png" alt="Pricing Mechanism Comparison" width="375"><figcaption></figcaption></figure>

### When to Choose SteppedMarket

**Ideal for**:
- New projects building community
- Projects wanting to reward early supporters
- Launches needing sustained momentum
- Most general-purpose launches

**Not ideal for**:
- Projects with established, small communities
- Launches where equal pricing is critical
- Projects with very high or very low price sensitivity

## FixedMarket: Equal Pricing

### How It Works

All Patron Cards sell at the same price. First-come, first-served.

**Example configuration**:
- Total supply: 100 cards
- Price: 0.75 ETH each
- No batches, no price changes

**Result**: 100 cards × 0.75 ETH = 75 ETH raised

### Key Benefits

**Simplicity**: Easy to understand and explain. No complex pricing logic.

**Fairness**: Everyone pays the same price. No advantage for early buyers.

**Predictability**: Supporters know exactly what they'll pay. No surprises.

**Equal access**: No artificial scarcity within price tiers.

### When to Choose FixedMarket

**Ideal for**:
- Established projects with strong communities
- Projects where equal pricing is important
- Simple launches without complex marketing
- Projects with very price-sensitive audiences

**Not ideal for**:
- New projects needing momentum
- Launches wanting to reward early supporters
- Projects with high FOMO potential

## MembersMarket: Exclusive Access

### How It Works

Only existing NFT holders can participate. Requires vouching from current members.

**Example configuration**:
- Total supply: 50 cards
- Price: 1.0 ETH each
- Requires: Ownership of specific NFT collection
- Vouching: 3 existing members must vouch for new participants

**Result**: Exclusive community of committed supporters

### Key Benefits

**Bot resistance**: Human verification required. Bots can't participate.

**Community curation**: Only genuine supporters get access. Quality over quantity.

**Exclusivity**: Creates premium feel and FOMO among non-members.

**Web of trust**: Vouching system builds strong community bonds.

### When to Choose MembersMarket

**Ideal for**:
- Exclusive club launches
- Projects with existing NFT communities
- High-value, low-supply launches
- Projects wanting curated supporters

**Not ideal for**:
- Public launches needing broad participation
- Projects without existing communities
- Launches wanting maximum reach
- Projects with small existing communities

## Decision Framework

### Ask These Questions

**What's your community size?**
- Large, established community → FixedMarket or SteppedMarket
- Small, exclusive community → MembersMarket
- New project, building community → SteppedMarket

**How important is early supporter rewards?**
- Very important → SteppedMarket
- Not important → FixedMarket
- Exclusivity more important → MembersMarket

**What's your FOMO strategy?**
- High FOMO, momentum building → SteppedMarket
- Moderate FOMO → FixedMarket
- Exclusivity-driven FOMO → MembersMarket

**How complex can your launch be?**
- Simple, straightforward → FixedMarket
- Moderate complexity → SteppedMarket
- Complex, curated → MembersMarket

### Common Mistakes

**Choosing FixedMarket for new projects**: New projects need momentum. SteppedMarket creates better FOMO.

**Choosing MembersMarket without community**: Don't use exclusive access if you don't have an existing community to vouch.

**Overcomplicating SteppedMarket**: Keep batch sizes reasonable. Too many small batches create confusion.

**Underpricing in any market**: Better to raise less with higher prices than to raise more with lower prices. Price signals value.

## Configuration Tips

### SteppedMarket Configuration

**Batch sizes**: 10-20% of total supply per batch. Too small creates confusion. Too large reduces FOMO.

**Price increments**: 10-20% increase per batch. Too small reduces urgency. Too large creates barriers.

**Starting price**: Set based on your minimum viable raise. Don't start too low.

**Total supply**: Match your funding target. More cards = lower individual prices.

### FixedMarket Configuration

**Price setting**: Research similar projects. Don't underprice. Price signals value.

**Supply**: Match your funding target. Don't create artificial scarcity.

**Timing**: Consider market conditions. Launch when your community is most active.

### MembersMarket Configuration

**Vouching requirements**: 3-5 vouches per new member. Too few reduces quality. Too many reduces participation.

**NFT requirements**: Choose collections that align with your project. Don't be too restrictive.

**Price**: Can be higher due to exclusivity. Don't overprice.

## Monitoring and Adjustments

### Track These Metrics

**Sales velocity**: How fast are cards selling?

**Community engagement**: Are people talking about your launch?

**Price sensitivity**: Are people complaining about prices?

**Bot activity**: Are you seeing suspicious buying patterns?

### Common Adjustments

**If sales are too slow**:
- Lower prices (if using FixedMarket)
- Reduce batch sizes (if using SteppedMarket)
- Increase marketing efforts
- Lower your funding target

**If sales are too fast**:
- Raise prices
- Increase batch sizes
- Extend sale period
- Increase total supply

**If you're getting botted**:
- Switch to MembersMarket
- Add more verification requirements
- Implement rate limiting

## Success Examples

### SteppedMarket Success

**Project**: DeFi Protocol
**Configuration**: 1000 cards, 100 per batch, 0.1 ETH starting price, 0.05 ETH increments
**Result**: Sold out in 3 days, raised 75 ETH
**Key factors**: Strong community, reasonable pricing, good marketing

### FixedMarket Success

**Project**: Established DAO
**Configuration**: 500 cards, 0.5 ETH each
**Result**: Sold out in 1 week, raised 250 ETH
**Key factors**: Existing community, fair pricing, clear value proposition

### MembersMarket Success

**Project**: Exclusive NFT Community
**Configuration**: 100 cards, 1.0 ETH each, 3 vouches required
**Result**: Sold out in 2 days, raised 100 ETH
**Key factors**: Strong existing community, high exclusivity, premium positioning

## Next Steps

Ready to choose your market type?

1. **[Design your tokenomics](./pricing-and-economics.md)** - Plan your token distribution
2. **[Deploy your project](./launch-process.md)** - Launch your token
3. **[Monitor your progress](./launch-checklist.md)** - Track your success

---

**Remember**: The market type you choose shapes your entire launch experience. Choose based on your community, goals, and strategy. The right choice can make the difference between success and failure.