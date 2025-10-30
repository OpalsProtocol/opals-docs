# How Opals Works

Your project launches in four simple phases. Each phase is automated. No manual intervention. No trust required. Just code and math.

## The Four Phases (At A Glance)

1. **Deploy** (5 minutes): Fill out a form. Smart contracts deploy automatically.
2. **Sell** (hours to days): Community buys Patron Cards. ETH accumulates. You keep some, rest goes to liquidity.
3. **Launch** (instant): Uniswap pair created. LP tokens locked forever. Trading begins.
4. **Reward** (forever): Each trade generates fees. Card holders claim rewards based on their commitment.

That's it. You don't touch anything after deployment. Contracts handle everything else.

## Phase 1: Deploy Your Project

You fill out a simple form with your project details:

- **Token name and supply** (e.g., "MyToken", 1 billion total)
- **How many Patron Cards** you want to sell (e.g., 5,000 cards)
- **Card pricing** (e.g., fixed price of 1 ETH, or graduated pricing starting at 0.5 ETH increasing by 0.05 ETH)
- **How to split raised ETH** between your team and liquidity (e.g., 30% to team, 70% to liquidity)
- **Optional features** like staking rewards or ETH staking through Aave

Click deploy. Done.

Smart contracts automatically deploy and wire together. No Solidity knowledge needed. No manual configuration of individual contracts.

Everything you set during deployment is locked in. You can't change token supply after launch. You can't change the split percentage. This is intentional - immutable rules prevent rug pulls.

**Time**: 5 minutes from form to live contracts.
**Cost**: ~$15 in gas (EIP-1167 minimal proxies save 74.7% vs custom contracts).
**Result**: Your complete token ecosystem ready for Phase 2.

## Phase 2: Community Buys Patron Cards

Your market is live. Community members can buy Patron Cards.

Each card costs ETH (the price you set). Card holders earn LP rewards forever. They can hold, sell on secondary markets, or stake for extra rewards.

The sale runs on your timeline. Stop it manually whenever you want. Or set an automatic timeout.

**What happens:**
- Supporters buy cards → ETH collects in smart contracts
- Your team receives 50% of the 2% sales fee (~1% of each sale) immediately
- Rest goes to liquidity pool creation
- No one removes liquidity. Ever. It's locked by contract, not by promise

**Typical timeline**: 1-3 days for projects with good demand. Some finish in hours. Some take a week.

The longer the sale runs, the more funding you raise. More funding = deeper liquidity = better token price stability.

## Phase 3: Uniswap Pair Launches Automatically

When your NFT sale ends, the smart contracts automatically:

1. **Take the ETH raised** (minus your team's share)
2. **Combine it with your tokens** in a Uniswap V2 liquidity pool
3. **Lock the LP tokens forever** in the PatronClaim contract

This takes one transaction. It happens instantly.

The result: Your token is live on Uniswap. Price is determined by the math: ETH in pool ÷ Tokens in pool = Initial price.

**Example**:
- Raise: 1,400 ETH from Patron Card sales
- Tokens for liquidity: 500 million
- Initial price: 1,400 ETH ÷ 500M tokens = 0.0000028 ETH per token

The LP tokens (proving the liquidity exists) sit permanently in the PatronClaim contract. No team member can withdraw them. No timelock that expires. Mathematically impossible to rug.

Supporters can now trade your token freely. The liquidity you created remains forever.

## Phase 4: Card Holders Earn Rewards (Forever)

Every time someone trades your token on Uniswap, a 1% fee is generated (not the standard 0.3%).

Patron Card holders earn their share of these fees. The bigger your believer (longer they committed their capital), the more they earn.

**How it works:**
- Someone buys 1 million tokens for $10,000 → $100 fee generated
- That $100 goes to reward Patron Card holders
- Distribution is based on PatronPower: how much they bought and how long they committed

**The multiplier:**
- Lock for 7 days: 0.024x multiplier (minimal reward)
- Lock for 1 year: 1.25x multiplier (25% bonus)
- Lock for 4 years: 5x multiplier (500% bonus)
- **Lock permanently: 10x multiplier (1,000% bonus)**

A supporter with $1,000 locked permanently earns more than a whale with $1 million locked for 7 days.

Commitment beats capital. This prevents mercenary capital from dominating.

**Claiming rewards:**
Card holders claim anytime by clicking a button. Claim or let them compound. Your choice.

This continues forever. As long as trading happens, fees accumulate. As long as you hold a card, you earn rewards.

No team member can stop it. No governance vote can change it. Mathematical formula, enforced by smart contracts.

## The Full Picture

All four phases work together:

1. You deploy (5 minutes)
2. Community buys cards (hours to days)
3. Liquidity launches automatically (instant)
4. Rewards flow forever (as long as trading happens)

Each phase is automatic. You're not actively managing anything. Contracts enforce the rules. Math ensures fairness.

**The key innovation**: Liquidity is locked by code, not by promise. PatronPower ensures commitment is rewarded. Supporters who believe most earn most.

This changes the dynamic completely. Traditional launches reward capital. Opals rewards conviction.

## Next Steps

Want to launch your own project? [Read the founder's guide](../for-founders/quick-start.md).

Want to understand the economic model? [Learn about PatronPower](../mechanisms/patronpower-system.md).

Want technical details? [Explore the architecture](../technical/README.md).

Want to invest in projects? [Start with the investor guide](../for-investors/README.md).
