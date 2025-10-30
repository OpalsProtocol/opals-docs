# Markets

Markets are where Patron Cards get sold. They determine how many cards sell, at what price, and to whom.

Opals offers three market types as ingredients. Each serves different founder goals and community dynamics.

## Ingredient 1: Stepped Market

The most popular market type.

**How it works**: Cards sell in price tiers. Each tier increases in price.

**Example**: 1M raise, 10k cards total
- Tier 1: First 2,000 cards at 0.1 ETH = 200 ETH
- Tier 2: Next 5,000 cards at 0.25 ETH = 1,250 ETH
- Tier 3: Final 3,000 cards at 0.5 ETH = 1,500 ETH
- Total: 2,950 ETH (~$4.4M at $1500/ETH)

**Price increases**: Enforced by smart contracts. Can't buy Tier 2 price until Tier 1 sells out.

**Psychology**:
- Early supporters get better deals (FOMO works both ways)
- "Beat the price increase" creates urgency
- Fair to everyone in same tier
- Bots get no advantage (can't front-run tier cutoffs)

**Gas costs**: Minimal. Standard Uniswap V2 paired deployment.

**Best for**:
- Projects building hype
- Founders wanting rapid initial sales
- Communities with FOMO-driven engagement

**Example projects**: Most successful Opals launches use Stepped pricing

## Ingredient 2: Fixed Market

Predictable, democratic pricing.

**How it works**: One price for all cards. First-come, first-served basis.

**Example**: 1M raise, 10k cards total at fixed 0.2 ETH
- Anyone can buy at 0.2 ETH until 10k sold
- Total raised: 10,000 × 0.2 = 2,000 ETH (~$3M)
- No price increases
- No tier gaming

**Psychology**:
- Fair and transparent
- No "best time to buy" strategy
- Feels democratic
- Less exciting than stepped (lower FOMO)

**Best for**:
- Established projects with strong communities
- Founders wanting pure first-come-first-served fairness
- Projects avoiding manipulation concerns

**Comparison to Stepped**:
- Same total raised: Depends on pricing
- Stepped: Front-loads revenue, ends fast
- Fixed: Linear revenue over duration
- Stepped: Creates urgency, Fixed: Creates fairness

## Ingredient 3: Members Market

Exclusive, invite-based access via vouching.

**How it works**:
1. Project starts with initial members
2. Existing members can vouch for new participants
3. Only vouched members can buy cards

**Example**: 1M raise, 10k cards, members market
- Start: 100 core members
- Month 1: 100 members buy, can vouch for 500 new
- Month 2: 600 members can buy, vouch for more
- Month 3: Market expands organically through trust network

**Psychology**:
- Creates web of trust
- Bots can't participate (require real vouching)
- Community feels exclusive and curated
- Members take ownership ("I brought in my friend")

**Vouching mechanics**:
- Member A can vouch for Member B
- Vouching is a signal of trust
- Malicious vouchers can get de-vouched by project
- Creates accountability (your vouches reflect on you)

**Best for**:
- Exclusive launches (limited supply)
- Community-first projects
- Projects wanting quality > quantity participants
- Preventing bot participation

## Recipe: Which Market Type?

**Use Stepped Market if**:
- You want fast initial sales
- Your community likes momentum/FOMO
- You want tiered reward incentives
- You're raising a large amount quickly

**Use Fixed Market if**:
- You want perfect fairness
- Your community is already strong
- You want no perception of manipulation
- You're raising steadily over time

**Use Members Market if**:
- You want high-quality participants
- You're building an exclusive community
- You want to prevent bot attacks
- You prefer vouching-based network effects

## Technical Implementation

All three market types use the same Market contract template with different configurations:

### Stepped Market Contract

**Key state**:
- `tiers[]`: Array of price tiers
- `tiersSold[]`: How many sold per tier
- `currentTier`: Current active tier based on sold count

**Example configuration**:
```
tiers = [0.1 ETH, 0.25 ETH, 0.5 ETH]
tierSizes = [2000, 5000, 3000]  // How many cards per tier
```

**Buying logic**:
1. Buyer submits: "Buy 5 cards"
2. Contract checks: Which tier are we in?
3. If tier 1 has 100 spots left, buy 5 at 0.1 ETH
4. If tier 1 full, buy at tier 2 price
5. Process payment, mint cards

### Fixed Market Contract

**Key state**:
- `fixedPrice`: Single price for all cards
- `cardsSold`: Total cards sold so far
- `maxCards`: Maximum cards this market can sell

**Buying logic**:
1. Buyer submits: "Buy 5 cards"
2. Contract checks: Are we under max?
3. If yes, charge 5 × fixedPrice
4. Process payment, mint cards

### Members Market Contract

**Key state**:
- `members[]`: Approved member list
- `memberCanVouch[]`: Can this member vouch for others?
- `vouchees[]`: Who vouched for whom

**Buying logic**:
1. Buyer submits: "Buy 5 cards" + "Voucher: 0x123"
2. Contract checks: Is buyer approved OR has valid voucher?
3. If valid, apply member price (may be better than public)
4. Process payment, mint cards
5. New buyer gets added to members list

## Real-World Examples

### Example 1: Fast-Growing DeFi Project (Stepped Market)

**Goal**: Raise $5M in 2 weeks

**Configuration**:
- Tier 1: 0.1 ETH, 15k cards
- Tier 2: 0.2 ETH, 20k cards
- Tier 3: 0.3 ETH, 15k cards
- Total: 50k cards, ~4,750 ETH raised

**Result**:
- Tier 1 sells out in 24 hours (FOMO kicks in)
- Tier 2 sells in 1 week
- Tier 3 sells in final week
- Momentum builds, community engagement high

### Example 2: Established Protocol (Fixed Market)

**Goal**: Steady participation over 1 month

**Configuration**:
- Fixed price: 0.15 ETH
- Max cards: 40k
- Duration: 30 days

**Result**:
- Steady daily sales
- No price urgency
- Fair to everyone
- Total raised: ~6,000 ETH

### Example 3: Exclusive Community (Members Market)

**Goal**: High-quality, long-term community

**Configuration**:
- 100 initial members (founders + advisors)
- Members can vouch for 5 new members each
- No maximum cards (until vouchers run out)

**Result**:
- Network grows organically
- Only trusted community members
- Strong long-term bonds
- Bot-proof participation

## Gas Costs by Market Type

**Stepped Market**: Standard (~21k gas per purchase)
- More complex tier logic costs minimal extra gas

**Fixed Market**: Minimal (~15k gas per purchase)
- Simplest logic, lowest gas

**Members Market**: Higher (~50k gas per purchase)
- Vouching verification adds cost
- Worth it for bot prevention

## Pricing Formulas

### Stepped Market

```
Price = tiers[getCurrentTierIndex()]
currentTier = tierIndex where cumSold < tierSize sum
```

### Fixed Market

```
Price = fixedPrice (always)
```

### Members Market

```
Price = memberPrice if vouched and isApprovedMember()
Price = publicPrice if in public launch phase
```

## Navigation: Choosing Your Market Type

**Decision tree**:
1. Do you want fast initial sales with momentum?
   - Yes → Stepped Market
   - No → Continue

2. Do you want exclusive, vouching-based community?
   - Yes → Members Market
   - No → Fixed Market

3. Want to prevent bot participation?
   - Yes → Members Market
   - No → Stepped or Fixed (Stepped has other bot protection)

## Next Steps

- **[Tokens](./tokens.md)** - Token distribution matching your market
- **[Patron Cards](./patron-cards.md)** - NFT mechanics and ownership
- **[Choosing Your Market](../for-founders/choosing-market-type.md)** - Founder decision guide
