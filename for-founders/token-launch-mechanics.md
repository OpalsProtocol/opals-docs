# Token Launch Mechanics

Your token launch on Uniswap happens automatically. No manual steps. No admin intervention. No possibility of error.

This guide explains how the LiquidityLauncher works without diving into code.

<figure><img src="../.gitbook/assets/image (1).png" alt="Token Launcher Interface"><figcaption><p>Total raised is 45 ETH out of a target of 100</p></figcaption></figure>

## The Three Phases

### Phase 1: Accumulation

During your NFT sale, the LiquidityLauncher accumulates resources:

**ETH collection**: Every Patron Card mint sends ETH to the market contract. After fees, ETH goes to LiquidityLauncher.

**Token allocation**: Your Token contract mints total supply. The percentage you allocated for liquidity (typically 40%) is held for Uniswap launch.

**Waiting for threshold**: LiquidityLauncher waits until your sale completes or hits minimum threshold.

No trading possible yet. Everything is accumulating.

### Phase 2: Atomic Launch

When threshold is reached, launch happens in a single transaction:

**Step 1**: LiquidityLauncher receives accumulated ETH

**Step 2**: Token contract transfers LP allocation to LiquidityLauncher

**Step 3**: LiquidityLauncher creates Uniswap V2 pair for your token + ETH

**Step 4**: LiquidityLauncher adds all ETH + all LP tokens as liquidity

**Step 5**: Uniswap mints LP tokens representing the liquidity position

**Step 6**: LiquidityLauncher sends LP tokens to PatronClaim

**Step 7**: PatronClaim locks LP tokens permanently (no withdrawal function)

All steps happen atomically. If any step fails, entire transaction reverts. Either everything succeeds or nothing happens.

### Phase 3: Trading

Once liquidity is added:

**Immediate trading**: Anyone can buy or sell your token on Uniswap

**Price discovery**: Market determines price through supply and demand

**Permanent liquidity**: LP tokens locked forever in PatronClaim

**Fee distribution**: Trading fees start flowing to Patron Card holders

## Why Atomic Launch Matters

Atomic launches prevent partial failures. Either your token launches completely or it doesn't launch at all.

This eliminates common problems:
- Liquidity added but tokens not distributed
- Tokens distributed but liquidity not added
- Partial launches that leave projects in limbo

The atomic nature also prevents manipulation. No one can interfere with the launch process. No admin can stop it. No external force can disrupt it.

## Liquidity Protection

Once LP tokens are locked in PatronClaim, they cannot be withdrawn. Ever.

The PatronClaim contract has no withdrawal function. No admin keys exist. No timelock can unlock them. The liquidity is mathematically guaranteed to stay in the pool.

This creates unbreakable trust. Your supporters know their investment is protected. They can't be rugged. The liquidity can't disappear.

## Price Discovery

The initial price is determined by the ratio of ETH raised to tokens allocated for liquidity.

If you raise 100 ETH and allocate 1,000,000 tokens (40% of 2.5M total), the initial price is 0.0001 ETH per token.

This creates fair price discovery. The price reflects actual demand from your community, not artificial manipulation.

## Automatic Distribution

LP tokens are distributed to Patron Card holders based on their card allocation.

Each Patron Card entitles the holder to a specific amount of LP tokens. These tokens represent their permanent share of the liquidity pool.

Distribution happens automatically. No manual intervention required. No admin approval needed.

## Trading Begins

Once liquidity is added, trading begins immediately. Anyone can buy or sell your token on Uniswap.

The custom Uniswap V2 fork charges 1% trading fees instead of the standard 0.3%. These fees flow to the Distributor contract for PatronPower-weighted distribution.

This creates sustainable rewards for Patron Card holders. The more people trade, the more everyone earns.

## Monitoring Your Launch

You can monitor your launch progress in real-time:

**Funding progress**: Track how much ETH has been raised

**Card sales**: See how many Patron Cards have been sold

**Time remaining**: Know how much time is left in the sale

**Community engagement**: Monitor social media and community activity

## What Happens If You Don't Reach Threshold

If your sale doesn't reach the minimum threshold, the launch doesn't happen. Patron Card holders can reclaim their ETH.

This protects supporters from failed launches. They don't lose their money if the project doesn't succeed.

## Post-Launch Activities

After your token launches:

**Monitor trading**: Watch volume, price, and community activity

**Engage community**: Keep supporters excited about the project

**Deliver value**: Focus on building your product and delivering on promises

**Distribute rewards**: Help Patron Card holders understand how to claim rewards

## Common Questions

**Q: Can I change the launch parameters after deployment?**
A: No. All parameters are immutable once deployed. This prevents manipulation and builds trust.

**Q: What if I want to add more liquidity later?**
A: You can't. The liquidity is locked permanently. This is by design to prevent rug pulls.

**Q: Can I pause or stop the launch?**
A: No. Once the threshold is reached, the launch happens automatically. This prevents manipulation.

**Q: What happens to unsold Patron Cards?**
A: They remain available for purchase until the sale ends or the threshold is reached.

**Q: Can I change the token allocation after deployment?**
A: No. The allocation is set at deployment and cannot be changed.

## Best Practices

### Set Realistic Targets

Don't set your threshold too high. It's better to launch with a smaller amount than to fail to launch at all.

### Build Community First

Start building your community before you need to raise funds. Relationships take time to build.

### Be Transparent

Share your progress openly. Show your work. Build trust through transparency.

### Focus on Value

Build something people actually want. Solve real problems. Create real value.

### Stay Committed

Launching is just the beginning. Stay committed to your vision. Keep building. Keep growing.

## Next Steps

Ready to launch your token?

1. **[Design your tokenomics](./pricing-and-economics.md)** - Plan your token distribution
2. **[Choose your market type](./choosing-market-type.md)** - Select the right mechanism
3. **[Deploy your project](./launch-process.md)** - Launch your token
4. **[Monitor your progress](./launch-checklist.md)** - Track your success

---

**Remember**: The LiquidityLauncher handles everything automatically. Your job is to build something great and let the system work. The math does the rest.