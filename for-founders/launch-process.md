# Launch Process: Your End-to-End Journey

This guide walks you through launching your token on Opals from pre-launch planning to post-launch growth. Most founders complete the entire process in about 10 days.

## Timeline Overview

**Pre-Launch** (2-3 days): Design tokenomics, build community, prepare marketing

**Configuration** (30 minutes): Set up wallet, choose market type, configure pricing

**Deployment** (5 minutes): Deploy contracts through factory

**Active Sale** (1 week typical): Monitor progress, engage community

**Automatic Launch** (instant): Liquidity provision happens automatically at threshold

**Post-Launch** (ongoing): Track metrics, distribute rewards, grow project

Total time from decision to trading: 10 days average.

## Phase 1: Pre-Launch (2-3 Days)

### Design Your Tokenomics

Before deploying anything, design your token distribution:

**Recommended allocation**:
- 40% to liquidity pool
- 30% to reward distributions
- 30% to team and development

This creates healthy liquidity, rewards supporters, and funds development.

**Set your raise target**: How much ETH do you need?
- Small projects: $50k-$250k
- Medium projects: $250k-$2M
- Large projects: $2M+

Your target determines your Patron Card supply and pricing.

### Choose Your Market Type

Three market types available:

**SteppedMarket**: Batch-based pricing with increases. Best for most launches. Creates FOMO while staying bot-resistant.

**FixedMarket**: Same price for every NFT. Simplest option. Best for established communities.

**MembersMarket**: Requires existing NFT ownership to participate. Best for exclusive club launches.

[Full comparison guide](./choosing-market-type.md)

### Design Your Pricing Strategy

**For SteppedMarket**:
- Starting price: What early supporters pay
- Price increment: How much price increases per batch
- Batch size: How many NFTs per batch

Example: 100 NFTs, 10 per batch, start at 0.5 ETH, increase 0.05 ETH per batch.
- Batch 1: 0.50 ETH
- Batch 2: 0.55 ETH
- Batch 10: 0.95 ETH

Total raised: 70 ETH (approximately $140k at $2k ETH)

**For FixedMarket**:
- Fixed price: What every NFT costs
- Total supply: How many NFTs to sell

Example: 200 NFTs at 0.5 ETH each = 100 ETH raised (approximately $200k)

### Build Your Community

Launch success depends on community:

**2-3 weeks before launch**:
- Announce project vision and roadmap
- Explain why community funding matters
- Share tokenomics and distribution
- Create Discord/Telegram community

**1 week before launch**:
- Explain how Patron Cards work
- Share pricing details
- Announce launch date and time
- Build anticipation

**Critical**: Don't launch to zero audience. Even 50-100 engaged supporters is enough for smaller raises.

### Prepare Your Marketing

**Required materials**:
- Project website with clear value proposition
- Twitter account with regular updates
- Discord/Telegram for community
- Launch announcement post
- Explainer thread about Patron Cards

**Optional but helpful**:
- Video explaining the project
- Detailed tokenomics document
- Roadmap with milestones
- Team bios and credentials

### Legal Considerations

Check local regulations:
- Securities laws in your jurisdiction
- Know Your Customer requirements
- Tax implications for token sales
- Terms of service for your platform

Opals provides the infrastructure. Legal compliance is your responsibility.

## Phase 2: Configuration (30 Minutes)

### Set Up Your Wallet

You'll need an Ethereum wallet with:
- Approximately $50 worth of ETH for deployment gas
- MetaMask, WalletConnect, or similar Web3 wallet
- Wallet on the network you're deploying to (Ethereum mainnet, Base, Optimism, etc.)

Deployment costs around $15 in gas at normal network conditions.

### Access the Opals Dashboard

Navigate to the Opals launch dashboard. Connect your wallet. This wallet becomes the project admin.

**Security note**: The wallet you connect has admin privileges. Use a hardware wallet or secure multisig for production launches.

### Configure Project Parameters

**Basic information**:
- Project name: What your project is called
- Token symbol: 3-5 character ticker (e.g., "OPALS")
- Token supply: How many tokens to mint (standard: 1,000,000,000)

**Market configuration**:
- Market type: Stepped, Fixed, or Members
- Pricing parameters: Based on your pre-launch strategy
- Sale duration: How long the sale runs (typical: 7 days)
- Minimum threshold: Minimum ETH to reach for launch (optional)

**Liquidity configuration**:
- LP token percentage: How much goes to Uniswap (recommended: 40%)
- Initial price calculation: Based on ETH raised and LP tokens
- Slippage tolerance: 2% default (protects against price manipulation)

**Reward distribution**:
- Reward token percentage: How much for PatronClaim rewards (recommended: 30%)
- Vesting parameters: Time-lock options for supporters
- Diamond hands bonuses: Multipliers for long-term holders

### Review and Confirm

Double-check all parameters. These settings are immutable after deployment. Verify:

- Token supply and symbol
- Pricing strategy
- Sale duration
- Liquidity allocation
- Reward distribution

Once confirmed, you cannot change these values.

## Phase 3: Deployment (5 Minutes)

### Deploy Via Factory

Click "Deploy Project" in the dashboard. The OpalsFactory deploys your entire ecosystem:

**Contracts deployed**:
- Project (coordination hub)
- Token (ERC20 with your symbol)
- Operator (access control)
- Card (Patron Card NFTs)
- Market (NFT sale contract)
- PatronClaim (reward distribution)
- LiquidityLauncher (Uniswap integration)

All contracts deployed via EIP-1167 minimal proxies. Total gas cost: approximately $15.

### Verify Deployment

Transaction confirms in about 30 seconds. Verify on block explorer:

- All 7+ contracts deployed successfully
- Your wallet is listed as project admin
- Market contract has correct pricing
- Token supply matches your configuration

Block explorers automatically verify the contracts.

### Announce Launch

Share contract addresses with your community:
- Market contract address (where supporters mint Patron Cards)
- Token contract address (for adding to wallets)
- Project dashboard link

Create an announcement post with:
- Launch time (be specific: "November 15, 2025 at 12:00 UTC")
- Pricing details
- How to participate
- Benefits of being a Patron Card holder

## Phase 4: Active Sale (1 Week Typical)

### Monitor Sale Progress

Track metrics in real-time:
- NFTs minted
- ETH raised
- Current price (for SteppedMarket)
- Time remaining
- Progress toward minimum threshold

Dashboard updates automatically. No manual intervention needed.

### Engage Your Community

During the sale:

**Daily**: Post updates on progress, highlight milestones reached, answer questions in Discord

**When batches sell out**: Celebrate with community, create urgency for next batch

**If sales slow**: Share more about project vision, bring in team for AMAs, explain long-term value

**Critical milestones**: 25% sold, 50% sold, 75% sold, minimum threshold reached

### Handle Common Scenarios

**Sales slower than expected?**
- Increase marketing efforts
- Host community events
- Explain PatronPower benefits
- Share team credentials and roadmap
- Extend sale duration if needed (requires redeployment)

**Sales faster than expected?**
- Prepare for Uniswap launch sooner
- Scale up community management
- Have liquidity monitoring ready
- Communicate post-launch plans

**Technical questions from supporters?**
- Point to documentation
- Explain PatronPower calculations
- Clarify reward distribution timelines
- Share contract addresses for verification

### Manage Expectations

Be transparent about:
- Where you are in the sale
- What happens if minimum threshold isn't reached
- When Uniswap launch occurs
- How rewards will be distributed

Avoid:
- Guaranteeing price performance
- Making unrealistic promises
- Changing terms mid-sale
- Creating false urgency

## Phase 5: Automatic Launch (Instant)

### Threshold Reached

When your sale completes or reaches minimum threshold, launch happens automatically.

**LiquidityLauncher contract**:
1. Accumulates all ETH raised
2. Transfers LP token allocation from Token contract
3. Creates Uniswap V2 pair
4. Adds liquidity (ETH + tokens)
5. Sends LP tokens to PatronClaim
6. LP tokens locked permanently

This happens in a single atomic transaction. No manual intervention possible.

### Initial Price Calculation

Your token's initial Uniswap price:

**Formula**: Price = ETH Raised / LP Token Supply

**Example**: Raised 100 ETH, allocated 40% of 1B tokens to LP
- LP tokens: 400,000,000
- ETH: 100
- Initial price: 100 ETH / 400M tokens = 0.00000025 ETH per token

At $2,000 per ETH, that's $0.0005 per token.

### Liquidity Is Permanent

LP tokens go directly to PatronClaim contract. PatronClaim has no withdrawal function for LP tokens. The liquidity is locked forever.

**This means**:
- You cannot rug pull (no admin keys exist)
- Supporters cannot rug pull (LP tokens distributed by weight, not directly)
- External attackers cannot rug pull (no withdrawal functions)

Rug pulls are mathematically impossible.

### Trading Begins

Once liquidity is added:
- Token is immediately tradeable on Uniswap
- Anyone can buy or sell
- Price determined by supply and demand
- 2% slippage protection built into initial add

Announce to your community that trading is live.

## Phase 6: Post-Launch (Ongoing)

### Monitor Launch Day

First 24 hours are critical:

**Watch for**:
- Initial price movement
- Trading volume
- Liquidity depth
- Any technical issues

**Be present**:
- Answer community questions
- Celebrate the launch
- Thank early supporters
- Share next steps

### Distribute Rewards

PatronClaim handles reward distribution automatically:

**How it works**:
- Supporters stake their Patron Card NFTs
- They choose lock duration (7 days to permanent)
- PatronPower calculated: LP Amount × Multiplier
- Rewards distributed pro-rata by PatronPower

Your role: Send reward tokens to PatronClaim contract periodically.

### Track Key Metrics

**Trading metrics**:
- Daily volume
- Price performance
- Liquidity depth
- Holder count

**Community metrics**:
- Active Discord/Telegram members
- Social media engagement
- Patron Card holders
- Staked cards percentage

**Reward metrics**:
- Total PatronPower
- Average lock duration
- Permanent locks percentage
- Rewards claimed vs available

### Grow Your Project

Post-launch focus:

**Month 1**: Stabilize price, distribute initial rewards, build on roadmap

**Month 2-3**: Ship first major features, grow holder base, maintain community engagement

**Month 4-6**: Evaluate success, plan next phases, consider additional raises if needed

### Handle Post-Launch Challenges

**Price volatility?**
- Expected in early days
- Focus on building, not price
- Remind community of long-term vision

**Low trading volume?**
- List on additional DEXs
- Increase marketing
- Ship compelling features

**Community questions about rewards?**
- Explain PatronPower clearly
- Show calculations
- Point to smart contract verification

## Resources Required

### Time Investment

**Pre-launch**: 10-20 hours (tokenomics, marketing, community building)

**Configuration and deployment**: 1 hour (actual deployment is 5 minutes)

**Active sale**: 1-2 hours daily (monitoring, engagement)

**Post-launch**: 2-4 hours daily (ongoing management)

### Financial Investment

**Deployment costs**:
- Gas fees: approximately $15
- Platform fees: 2% of ETH raised (charged automatically during sale)

**Example scenarios**:
- Raise $100k: $2,000 platform fee + $15 gas = $2,015 total
- Raise $500k: $10,000 platform fee + $15 gas = $10,015 total
- Raise $2M: $40,000 platform fee + $15 gas = $40,015 total

**Marketing costs** (optional but recommended):
- Website development: $500-$5,000
- Social media advertising: $1,000-$10,000
- Community management tools: $50-$500/month

### Team Requirements

**Minimum viable team**:
- 1 technical founder (handles deployment, answers technical questions)
- 1 marketing/community person (builds pre-launch hype, manages during sale)

**Recommended team**:
- Technical founder
- Marketing lead
- Community manager
- Content creator

Larger teams can move faster but aren't required for success.

## Common Mistakes to Avoid

### Pre-Launch Mistakes

**Launching to zero audience**: Build community first. Even 50 engaged supporters is enough.

**Unclear tokenomics**: Supporters need to understand distribution. Be transparent.

**Unrealistic pricing**: Don't overprice early batches. Start low, create FOMO naturally.

**No marketing plan**: Hope is not a strategy. Plan your announcements.

### During Sale Mistakes

**Radio silence**: Daily updates are critical. Community needs to see progress.

**Overselling rewards**: Don't guarantee returns. Explain PatronPower but avoid promises.

**Changing terms mid-sale**: You can't anyway (immutable contracts), but don't try to verbally reframe things.

**Ignoring questions**: Answer everything. Transparency builds trust.

### Post-Launch Mistakes

**Focusing only on price**: Build your product. Price follows execution.

**Forgetting reward distribution**: Send reward tokens regularly. Supporters are stakeholders.

**Abandoning community**: Maintain engagement. These people funded you.

**Failing to deliver on roadmap**: Do what you said you'd do. Reputation matters.

## Success Indicators

### During Sale

**Healthy launch**:
- 50%+ of supply sold within first 3 days
- Active community engagement
- Questions answered quickly
- Steady purchase velocity

**Struggling launch**:
- Less than 25% sold in first 3 days
- Low community activity
- Repeated questions going unanswered
- Purchase velocity declining

### Post-Launch

**Successful project**:
- 60%+ of Patron Cards staked
- Average lock duration over 1 year
- Regular reward distributions
- Active development

**Warning signs**:
- Less than 30% of cards staked
- Average lock duration under 30 days
- Irregular reward distributions
- Inactive development

## Next Steps

Ready to start? Here's your checklist:

1. Design tokenomics (40% LP, 30% rewards, 30% team)
2. Choose market type (Stepped recommended for most)
3. Set pricing strategy
4. Build community (2-3 weeks)
5. Prepare marketing materials
6. Deploy contracts (5 minutes)
7. Run sale (1 week typical)
8. Celebrate automatic launch
9. Distribute rewards
10. Build your project

[View detailed checklist](./launch-checklist.md)

[Calculate your costs](./pricing-and-economics.md)

[Compare market types](./choosing-market-type.md)

---

**Remember**: Thousands of founders have done this successfully. The process is proven. The infrastructure is battle-tested. Your job is to build something people want. Opals handles the rest.
