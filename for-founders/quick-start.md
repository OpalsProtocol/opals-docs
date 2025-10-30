# Quick Start: Launch in 5 Minutes

You want to deploy your token. You don't want to read twenty pages. Here's the absolute fastest path from "I want to launch" to "my token is live."

**Time: 5 minutes**
**Cost: ~$15**
**Knowledge required: None**

---

## Before You Deploy (Read This First)

Three decisions determine your entire launch. Get these right:

### 1. How Much Do You Want to Raise?

This is your target. Example: "I want to raise 1,000 ETH."

Your answer determines:
- How many Patron Cards you create
- Card pricing
- Liquidity depth at launch

**Pick a number. Stick with it.** You can end the sale early or extend it, but know your target.

### 2. How Should You Price Cards?

Two options:

**Fixed Price** (Simpler): Every card costs the same. Example: 1 ETH per card.
- Easiest to explain
- Best for: Small raises, tight-knit communities
- Bot resistance: Low

**Stepped Price** (Better): Price increases in batches. Example: First 100 cards at 0.5 ETH, next 100 at 0.55 ETH, etc.
- Prevents bots from exploiting first-mover advantage
- Creates mild FOMO as price increases
- Best for: Most projects
- Bot resistance: High

**Decision**: If unsure, choose Stepped. It's better.

### 3. How Should You Split Raised ETH?

Your team gets some. Liquidity gets the rest.

Example split:
- 30% to your team wallet (immediately after sale)
- 70% to liquidity pool (locked forever)

**More to team** = Cash now, but smaller liquidity pool = higher token price volatility
**More to liquidity** = Deeper pool, better price stability, but less cash for team

**Decision**: If you need runway capital, do 30-50% to team. If you want stable token price, do 10-20%.

---

## The Actual Deployment Process

You fill out a form. Contracts deploy automatically. That's it.

### Step 1: Connect Your Wallet

Go to the Opals dashboard. Connect your Ethereum wallet.

**Requirements**:
- Wallet with some ETH (for gas, ~$20 worth at 50 gwei)
- You'll be the project admin
- This wallet will receive team's share of funds when sale completes

**Time: 1 minute**

### Step 2: Fill Out Project Details

```
Project Name:        MyToken
Token Symbol:        $MYTOKEN
Total Token Supply:  1,000,000,000
Patron Cards:        5,000
```

These values are locked forever after deployment. Choose carefully.

**Rule**: Most projects use 1 billion tokens and 1,000-10,000 cards.

**Time: 2 minutes**

### Step 3: Configure Your Sale

```
Market Type:         Stepped
Starting Price:      0.5 ETH
Price Increment:     0.05 ETH per 100 cards
Sale Duration:       14 days (max)
Minimum Raise:       500 ETH (optional safety net)
```

If you hit your target before 14 days, you can manually end the sale early.

**Time: 1 minute**

### Step 4: Set the ETH Split

```
Liquidity Percentage:  70%
Team Percentage:       30%
Team Wallet Address:   [your wallet address]
```

**Time: 1 minute**

### Step 5: Deploy

Click "Deploy Contracts"

You'll see transaction confirmation. Gas cost: ~$15.

Contracts deploy and wire together automatically.

**Time: On-chain confirmation (varies, usually < 5 minutes)**

**Total so far: 6 minutes. You're done.**

---

## What Happens Next (You Don't Do Anything)

1. **Your market goes live immediately.** Supporters can buy Patron Cards using the button "Buy Patron Card."

2. **ETH accumulates automatically** in smart contracts.

3. **Your sale runs for the duration you set** (or until you manually stop it).

4. **When sale completes**, liquidity automatically launches:
   - All ETH (minus your team's share) combines with tokens
   - Uniswap V2 pair created
   - Trading goes live
   - LP tokens lock forever in PatronClaim

5. **Card holders can start claiming rewards** from trading fees.

---

## You Need to Do These Things

### Before Sale Starts
- [ ] **Build community awareness** - Announce launch date, share why supporters should buy cards
- [ ] **Set card image/metadata** - Make cards visually distinctive
- [ ] **Plan your distribution** - Decide how to allocate remaining tokens (team, ecosystem, future launches, etc.)

### During Sale
- [ ] **Monitor progress** - Check dashboard weekly
- [ ] **Engage community** - Answer questions, build hype
- [ ] **Tweet/announce milestones** - "50% sold!", "We're live on Uniswap!", etc.

### After Launch
- [ ] **Nothing required** - LP is locked automatically, rewards distribute automatically
- [ ] **Optional: Build your product** - Your supporters are now permanent stakeholders

---

## Common Questions (Before You Deploy)

### "What if nobody buys cards?"

Your sale runs for the duration you set (up to 14 days). If you don't hit minimum raise, you can:
1. Extend the sale
2. Manually refund supporters
3. Still launch with smaller liquidity (contracts allow this)

No penalty. Completely reversible.

### "Can I change the price after starting?"

No. Price is locked in the smart contract.

**This is intentional.** It prevents manipulation and protects early supporters.

### "What about my other tokens (airdrop, team allocation, etc.)?"

You set total supply during deployment (e.g., 1 billion).

Example split:
- 500M → Liquidity pool (via LP tokens)
- 200M → Team vesting (mint from token contract manually)
- 200M → Airdrop to community
- 100M → Reserve for future

You control how the remaining tokens get distributed after liquidity locks.

### "How do I prevent bots?"

Choose **Stepped Market** instead of Fixed Market.

Batch-based pricing eliminates bot advantage. All purchases in the same batch pay the same price. No first-mover advantage. Bots can't extract value.

### "What if my launch fails?"

Then you failed to build community.

Opals doesn't fail. Its contracts are proven. Liquidity is locked. Rewards distribute correctly.

Launches fail because projects lack product-market fit or community enthusiasm. Opals makes everything else automatic so you can focus on the hard part: building something people want.

---

## Troubleshooting Deployment

### "Transaction reverted"

Common causes:
1. **Insufficient gas** - Increase gas limit to 3,000,000
2. **Wallet doesn't have enough ETH** - Need ~$30 worth at 50 gwei
3. **Network is congested** - Try again in 5 minutes or increase gas price

### "Contracts won't deploy"

Make sure:
- [ ] Wallet is connected to correct network (usually Ethereum mainnet)
- [ ] You have ETH in wallet
- [ ] All form fields are filled correctly
- [ ] Numbers are whole numbers (no decimals)

### "Dashboard shows pending but nothing happened"

Wait 10 minutes. Blockchain is slow sometimes.

Check the transaction hash on Etherscan to verify it actually mined.

---

## The Actual Launch Sequence

Once deployed, here's what your supporters see:

```
[BUY PATRON CARD]
↓
Wallet connects
↓
Select lock duration (7 days, 1 year, 4 years, permanent)
↓
Pay ETH (price shown)
↓
"Purchase complete!"
↓
Card appears in wallet
↓
Rewards start accumulating (based on PatronPower multiplier)
```

Your supporters make one decision: How long to lock their commitment.

Permanent lock = 10x rewards
1-year lock = 1.25x rewards
7-day lock = 0.024x rewards (basically nothing)

Most believers choose permanent. Mercenaries choose 7 days (and earn almost nothing).

---

## Success Indicators

### Healthy Sale
- [ ] Multiple purchases in first 24 hours (not all in first minute)
- [ ] Mix of lock durations (not everyone choosing shortest lock)
- [ ] Price increasing smoothly (stepped market only)
- [ ] Community engagement (Discord activity, Twitter mentions)

### Healthy Launch
- [ ] Trading volume in first hour (shows real interest)
- [ ] LP value stable or increasing (not being manipulated)
- [ ] Holder claiming rewards (dashboard shows activity)
- [ ] Strong secondary market (cards trading on OpenSea)

### Unhealthy Signs
- [ ] Zero purchases for 24+ hours (no community interest)
- [ ] Extreme price swings (possible manipulation)
- [ ] Everyone doing 7-day locks (no long-term believers)
- [ ] No trading volume after launch (token has no utility)

---

## What to Tell Your Community

Share this with supporters before they buy Patron Cards:

**"Patron Cards are permanent ownership. You earn rewards from trading fees forever. The longer you commit, the more you earn.**

- **Permanent lock**: 10x multiplier (1000% bonus)
- **1-year lock**: 1.25x multiplier (25% bonus)
- **7-day lock**: 0.024x multiplier (basically nothing)

**Liquidity is locked forever. We can't rug. Price stability comes from commitment, not empty promises."**

---

## Next Steps

1. **Make your three decisions** (funding goal, pricing strategy, ETH split)
2. **Go to dashboard and deploy** (fill form, click deploy, wait 5 minutes)
3. **Share your launch link** with community
4. **Monitor progress** for a week
5. **Celebrate your launch** (you made it to Uniswap without VC or launchpad)

**You're done.** Everything else is automatic.

---

## Need More Details?

- **How does PatronPower math work?** → [PatronPower System](../mechanisms/patronpower-system.md)
- **What are Patron Cards exactly?** → [Understanding Patron Cards](../for-investors/understanding-patron-cards.md)
- **How is liquidity actually locked?** → [How It Works](../overview/how-it-works.md)
- **What contracts were deployed?** → [Technical Architecture](../technical/architecture-overview.md)

---

**That's it. You now know everything you need to launch.**

The hardest part isn't the infrastructure. It's building a community that believes in your vision enough to lock capital permanently.

Opals handles the infrastructure so you can focus on the hard part.

Go build something great.
