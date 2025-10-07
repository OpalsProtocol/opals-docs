# PatronPower: Rewarding True Believers

PatronPower is a time-weighted reward system. Lock longer, earn more.

## Why PatronPower Exists

Crypto projects die from mercenary capital.

Whales buy tokens, pump the price, dump within days. Early believers get rugged. Projects lose momentum before they ship anything real.

PatronPower flips this. Short-term staking earns almost nothing. Long-term commitment earns exponentially more. The difference is so extreme that mercenary capital becomes economically pointless.

## The Core Innovation

PatronPower multiplies your rewards based on commitment duration.

Seven-day lock: 0.024x multiplier. One-year lock: 1.25x multiplier. Four-year lock: 5x multiplier. Permanent lock: 10x multiplier.

That creates a 416x difference between minimum and maximum commitment. A whale staking $1 million for 7 days earns 24,000 PatronPower. A small holder staking $1,000 permanently earns 10,000 PatronPower.

The small holder wins.

## How Multipliers Work

The system uses two commitment types with different multiplier ranges.

Flexible staking allows exit with time-locked positions. You choose a lock duration between 7 days and 4 years. Your multiplier scales linearly from 0.024x to 5x based on that duration.

Permanent locks remove the exit option entirely. Your liquidity is locked forever. In exchange, you earn the maximum 10x multiplier regardless of stake size.

## Why This Prevents Mercenary Capital

Traditional staking rewards everyone equally per token. $1 million for one day earns the same rate as $1,000 for one year. That invites exploitation.

PatronPower makes short-term plays worthless through exponential scaling. The 0.024x multiplier at 7 days creates such poor returns that mercenaries must either commit long-term or go elsewhere.

Consider the economics. A whale with $1 million locked for 7 days competes against small holders with permanent locks. The whale needs to restake constantly, paying gas each time, to maintain their position. Small holders set and forget.

Mercenaries optimize for efficiency. PatronPower makes genuine commitment the most efficient strategy.

## Strategic Implications for Founders

PatronPower changes how you think about token distribution.

You want true believers, not tourists. PatronPower mathematically enforces this by making tourist rewards negligible. You don't need KYC. You don't need whitelist politics. The math does the work.

Early distribution becomes critical. The first supporters to lock permanently earn maximum rewards forever. This creates network effects around commitment, not speculation.

You can also structure your tokenomics to reward specific behaviors. Want to incentivize liquidity providers? Direct more protocol fees to PatronClaim holders. Want to reward governance participation? Weight voting by PatronPower.

The system is composable. You control the inputs through project design. PatronPower handles fair distribution automatically.

## Strategic Implications for Supporters

PatronPower rewards conviction at the expense of opportunism.

If you believe in a project long-term, permanent locks give you 10x advantages. You earn more protocol fees. You gain more governance influence. You receive larger airdrops if the project does retroactive distributions.

If you're unsure, flexible staking lets you participate with less commitment. Lock for one year instead of forever. Your 1.25x multiplier still beats speculators at 0.024x, but you maintain exit optionality.

The key insight: your commitment multiplier compounds over time through reward accumulation. Early permanent locks compound the longest. Waiting to lock permanently means missing early reward cycles.

This creates interesting game theory. Small holders who lock early and permanently can accumulate more total rewards than whales who enter later with larger capital but shorter commitments.

## Comparison with Traditional Staking

Traditional staking treats all commitments equally.

Stake 100 tokens for 7 days? Same APR as 100 tokens for 4 years. The only variable is duration, not commitment level. This invites mercenaries who rotate capital across protocols seeking the highest short-term APR.

Traditional staking also lacks permanent commitment options. Maximum lock periods are typically 1-4 years. Capital eventually unlocks. Projects can never rely on permanent liquidity.

PatronPower changes both dynamics. Commitment level determines rewards, not just duration. Permanent locks create unruggable liquidity foundations.

## The Three PatronPower Tiers

Opals implements PatronPower through three claim contracts with different multiplier profiles.

### PatronClaim: 10x Multiplier, Permanent Lock

PatronClaim represents founding patron support. You receive Patron Cards during NFT sales or as founder allocations. These cards represent permanently locked LP tokens with fixed 10x multipliers.

Patron Cards never expire. The underlying LP tokens can never be withdrawn. Your 10x PatronPower persists forever. This creates the unruggable liquidity foundation every project needs.

Use PatronClaim for early believers, founding teams, and community members who commit regardless of price. The permanent lock signals conviction. The 10x multiplier rewards it.

### VaultClaim: 0-5x Multiplier, Flexible Exit

VaultClaim serves regular supporters who want participation with optionality. You stake LP tokens directly into VaultClaim and choose your lock duration between 7 days and 4 years.

Your multiplier scales linearly: 7 days gives 0.024x, 1 year gives 1.25x, 4 years gives 5x. You can unstake after your lock expires. Or you can exit early using the OVL penalty system.

Use VaultClaim when you believe in the project but want flexibility. Lock longer for better rewards. Lock shorter to maintain liquidity. The choice is yours.

### VaultClaim Permanent: 10x Multiplier, Permanent Lock

VaultClaim also supports permanent locks matching PatronClaim's 10x multiplier. The difference: VaultClaim permanent locks happen post-launch, not during the initial sale.

This creates a path for later supporters to achieve founding patron status. You missed the Patron Card sale? Acquire LP tokens on Uniswap and lock them permanently in VaultClaim. Same 10x multiplier.

The permanent lock flag uses maximum uint256 value, making it impossible to unlock through integer overflow or expiration logic. Once locked, forever locked.

## How PatronPower Affects Reward Distribution

Reward distribution happens pro-rata by PatronPower, not by token balance.

When protocol fees flow into claim contracts, the system calculates your share as: your PatronPower divided by total PatronPower, multiplied by total rewards.

Example: 100 ETH in protocol fees flows into VaultClaim. Total PatronPower is 1,000,000. Your PatronPower is 10,000. Your reward: (10,000 / 1,000,000) × 100 ETH = 1 ETH.

Two holders with identical LP amounts earn different rewards if they have different lock durations. The 4-year lock earns 208x more than the 7-day lock with the same capital.

This proportional distribution is critical. It means whale capital doesn't dilute diamond hands rewards if the whale locks short-term. The whale's 0.024x multiplier barely moves the denominator.

## PatronPower and Governance

PatronPower enables commitment-weighted governance.

Traditional token voting has a problem: whales borrow tokens, vote, return them. This flash loan governance attack bypasses stake requirements. The attacker never risked anything.

PatronPower-weighted voting prevents this. Voting power derives from locked LP tokens, not circulating tokens. You can't flash loan locked positions. The commitment itself becomes the vote.

Projects can implement quadratic voting, conviction voting, or simple majority using PatronPower as the weight. The key benefit: only committed stakeholders participate. Tourists are mathematically excluded.

## PatronPower Validation

Every PatronPower claim is cryptographically verifiable on-chain.

VaultClaim stores lock duration, LP amount, and lock expiration for every staked position. PatronClaim stores LP allocation per Patron Card. The multiplier formulas are immutable constants in the smart contracts.

Anyone can verify your PatronPower by reading these public variables and applying the standard formula. No trusted party. No off-chain calculation. Pure math.

The VaultClaim formula: multiplier = (lock duration / maximum duration) × 5x, capped at 5x for non-permanent locks. Permanent locks return the hardcoded 10x multiplier.

The PatronClaim formula: multiplier = 10x for all Patron Cards, applied to the LP allocation assigned to that card.

## Common PatronPower Misconceptions

### "Whales always win anyway"

False. PatronPower inverts traditional capital dominance.

A whale with $10 million locked for 7 days has 240,000 PatronPower. One hundred small holders with $10,000 each locked permanently have 10,000,000 PatronPower. The small holders control 97.7% of rewards.

Capital matters less than commitment. Many small believers beat one large speculator.

### "This discriminates against new supporters"

False. New supporters can still lock permanently for 10x multipliers.

You missed the Patron Card sale. Acquire LP tokens on Uniswap. Lock them permanently in VaultClaim. Achieve the same 10x multiplier as founding patrons.

Yes, you enter after initial rewards have been distributed. That's true for every project. The permanent lock option ensures you can catch up through superior future rewards.

### "Long locks trap people in bad projects"

True, by design. That's the point.

PatronPower rewards commitment despite volatility. If you believe a project is good long-term, commit long-term. If you're unsure, don't maximum lock. The system offers flexible durations for this reason.

The penalty is not "being trapped." The penalty is missing rewards if you choose short locks and the project succeeds. Risk and reward scale together.

### "Permanent locks are too extreme"

For speculators, yes. For believers, no.

Founding teams lock tokens for years in traditional equity. Permanent LP locks apply the same logic to community funding. If you believe in the mission, permanent commitment makes sense.

If you want trading optionality, use VaultClaim with flexible durations. The 5x maximum is still strong. Reserve permanent locks for core conviction positions.

## PatronPower vs. Vote-Escrowed Models

Traditional ve-tokenomics lock tokens for voting power. Opals locks LP tokens for reward multipliers. This difference matters.

Vote-escrowed tokens (like Curve's veCRV) lock the native token. This removes tokens from circulation, creating supply squeeze. But it doesn't guarantee liquidity. Projects can still rug by removing LP.

PatronPower locks the LP tokens themselves. This guarantees liquidity can never be rugged. The trade-off: supply remains circulating. But who cares about circulating supply if liquidity is permanent?

Ve-tokenomics also concentrate power in the largest lockers. PatronPower balances size with commitment through the multiplier system. Small permanent locks compete with large temporary locks.

Finally, ve-tokenomics decay over time. Lock for 4 years, your voting power decays as expiration approaches. PatronPower remains constant. A 4-year lock maintains 5x multiplier throughout the entire term.

## PatronPower and Project Treasury Management

PatronPower creates interesting treasury dynamics.

Projects earn protocol fees from NFT sales and other sources. Those fees flow to claim contracts for distribution to PatronPower holders. This creates a fee-sharing model similar to traditional profit-sharing equity.

The project can allocate different fee percentages to different claim types. Send 50% to PatronClaim holders, 30% to VaultClaim holders, 20% to treasury. Adjust these percentages through governance.

Founders can also lock their own allocations to signal commitment. Mint Patron Cards for team members. Lock founder LP tokens permanently. Demonstrate alignment through cryptographic proof, not promises.

Treasury tokens can also stake for PatronPower. Hold native tokens? Convert to LP, lock permanently, earn perpetual protocol fees. This aligns treasury incentives with community incentives.

## The Math Behind 416x Advantage

The 416x multiplier difference between minimum and maximum comes from simple division.

Maximum multiplier: 10x (permanent lock). Minimum multiplier: 0.024x (7-day lock). Ratio: 10 / 0.024 = 416.67.

Seven days represents 0.48% of 4 years (7 / 1,460 days). The linear scaling formula: 0.0048 × 5x = 0.024x for 7-day locks.

This linear progression from 0.024x to 5x creates smooth scaling without cliffs. Every additional day locked increases your multiplier slightly. No gaming the system by locking 6 days 23 hours instead of 7 days.

Permanent locks jump to 10x as a binary decision. Either you commit forever for maximum multipliers, or you maintain optionality with the 0-5x range. No middle ground.

## Why Projects Choose PatronPower

PatronPower solves the fundamental crowdfunding problem: how do you reward early believers more than late speculators?

Traditional token launches use price as the signal. Early price = early believers. But this invites front-running, bot exploitation, and whale dominance. Price alone doesn't prove commitment.

PatronPower uses time as the signal. Early permanent locks prove conviction. Late temporary locks prove opportunism. The multiplier system quantifies this difference.

Projects adopting PatronPower gain three benefits:

First, unruggable liquidity foundation through permanent locks. No project can rug if LP is permanently locked. This builds trust immediately.

Second, aligned incentives between founders and supporters. Everyone competes for PatronPower through commitment. Diamond hands earn more together.

Third, natural bot resistance. Bots optimize for short-term profits. PatronPower makes short-term plays worthless. Bots go elsewhere.

## The Future of PatronPower

PatronPower currently governs reward distribution. Future versions could expand its utility.

Potential applications include commitment-weighted voting, protocol access tiers, priority transaction ordering, or cross-project reputation. Any system that benefits from sybil resistance and commitment signaling could integrate PatronPower.

The core innovation remains: using time commitment as proof of genuine support. This principle extends beyond DeFi into any community coordination problem.

For now, PatronPower focuses on its primary mission: ensuring true believers win.

## Next Steps

Ready to earn PatronPower?

Founders: Launch your project with built-in PatronPower reward distribution. Every supporter automatically gets fair allocation based on commitment.

Supporters: Acquire Patron Cards or stake LP tokens with long lock periods. Earn maximum multipliers through genuine commitment.

Developers: Integrate PatronPower-weighted logic into your governance systems. Use commitment as the trust anchor.

PatronPower is live. The contracts are immutable. The multipliers are fixed. Start earning today.
