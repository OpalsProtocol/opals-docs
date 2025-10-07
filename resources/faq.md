# Frequently Asked Questions

Quick answers to common questions. Each answer links to detailed documentation.

## General Questions

### What is Opals?

A token launch platform for deploying complete crypto projects. Founders launch in 5 minutes for $15 with no coding required.

Community members fund projects by buying Patron Cards. Cards unlock permanent token rewards based on trading fees.

[Learn more about Opals →](../overview/what-is-opals.md)

### How is Opals different from launchpads?

Opals is infrastructure, not a marketplace. You deploy directly through smart contracts. Launchpads are listing services where you apply and pay fees.

Platform fee: 2% on NFT sales only. Launchpad fees: $500K+ upfront plus 7% of tokens.

[Compare Opals to alternatives →](../overview/why-opals.md)

### Is Opals open source?

Yes, completely. All contracts are public on GitHub. Licensed under MIT.

375 tests passing. Full audit trail available. Anyone can verify the code.

[View the repository →](https://github.com/opals-xyz/contracts)

### Which blockchains does Opals support?

Base, Optimism, Arbitrum, and Ethereum mainnet. More chains coming soon.

Testnet deployments available on Base Sepolia and Monad testnet.

[See deployment addresses →](../technical/deployments.md)

### Has Opals been audited?

Yes. Comprehensive security audit completed. All HIGH severity issues resolved.

375 tests maintain 100% pass rate. CEI pattern enforced. Reentrancy protection throughout.

[Read the audit report →](../for-founders/security-and-trust.md)

### How much does it cost to use Opals?

Deployment: $15 in gas costs. Platform fee: 2% on NFT sales only. No hidden fees.

50% of the 2% fee goes back to you. Effective cost: 1%.

[See detailed pricing →](../for-founders/pricing-and-economics.md)

## For Founders

### Do I need coding skills to launch?

No. Fill out a form with your project parameters. One-click deployment handles everything.

The platform deploys 15+ smart contracts automatically. No Solidity knowledge required.

[Follow the launch process →](../for-founders/launch-process.md)

### How long does it take to launch?

5 minutes from start to finish. Deployment happens in one transaction.

Preparation time varies. Allow 1-2 hours for planning parameters and preparing marketing.

[See the complete timeline →](../for-founders/launch-process.md)

### Can I customize the smart contracts?

No. All projects use pre-audited templates. No custom code allowed.

This limitation is a feature. Prevents custom vulnerabilities. Inherits proven security.

[Learn about templates →](../core-concepts/template-factory.md)

### What if I need a feature that doesn't exist?

Templates cover 95% of use cases. Stepped pricing, fixed pricing, staking, rewards, governance.

For truly custom needs, fork the contracts and audit separately. Or wait for new templates.

[See available features →](../for-founders/choosing-market-type.md)

### How do I set my NFT price?

Choose between stepped pricing (increases each batch), fixed pricing (constant), or members-only.

Recommended: Start at 0.05-0.1 ETH for community projects. 0.5-1 ETH for premium launches.

[Learn pricing strategies →](../for-founders/choosing-market-type.md)

### How many Patron Cards should I sell?

Balance scarcity and accessibility. 100-500 cards for small communities. 1,000-5,000 for large projects.

More cards = more funding but less exclusivity. Consider your community size.

[See the launch checklist →](../for-founders/launch-checklist.md)

### Can I rug the liquidity?

No. Mathematically impossible. LP tokens lock in PatronClaim with no withdrawal function.

Not a timelock. Not a promise. Cannot be changed after deployment.

[Understand unruggable design →](../for-founders/security-and-trust.md)

### What happens to the ETH raised?

Goes directly to Uniswap V2 liquidity. Paired with project tokens. Creates tradeable market.

LP tokens distributed to Patron Card holders. They earn trading fees forever.

[See token launch mechanics →](../for-founders/token-launch-mechanics.md)

### Can I raise more funds later?

Yes. Deploy additional card sets. Each set can have different pricing.

Original supporters maintain their benefits. New supporters earn proportionally based on PatronPower.

[Learn about multiple rounds →](../for-founders/launch-process.md)

### Do I keep control of my project?

Yes, 100%. No board seats. No veto rights. No investor approval required.

You control the admin role. Can add operators. Cannot change core economics.

[Learn about sovereign startups →](../overview/why-opals.md)

## For Investors

### How do I buy Patron Cards?

Connect your wallet. Browse projects. Select card quantity. Approve transaction. Receive NFTs.

You'll need ETH in your wallet plus gas for the transaction.

[Get started investing →](../for-investors/getting-started.md)

### What do Patron Cards give me?

Permanent ownership rights. LP token allocation. Trading fee rewards forever. Governance participation (if enabled).

The earlier you buy, the better your price. Later batches cost more in stepped markets.

[Understand Patron Cards →](../for-investors/understanding-patron-cards.md)

### How do I earn rewards?

Trading fees accumulate in your LP tokens. Claim anytime through PatronClaim contract.

Additional rewards available through VaultClaim staking. Lock LP for multiplied rewards.

[Learn about staking →](../for-investors/staking-rewards-guide.md)

### What is PatronPower?

The system that determines reward distribution. Multiplies rewards by commitment level.

Permanent locks: 10x multiplier. 7-day locks: 0.024x multiplier. Lock longer, earn more.

[Deep dive on PatronPower →](../core-concepts/patronpower-system.md)

### Can I sell my Patron Cards?

Yes. They're ERC721 NFTs. Tradeable on OpenSea or any NFT marketplace.

Selling transfers both the NFT and accumulated rewards. Buyer inherits your benefits.

[Understand secondary markets →](../for-investors/understanding-patron-cards.md)

### How much can I earn?

Depends on trading volume, your PatronPower, and total LP locked. No guaranteed returns.

Example: $1M daily volume, 1% custom fee (not standard 0.3%), 10x multiplier = substantial rewards. But volume varies.

[See return scenarios →](../for-investors/understanding-patron-cards.md)

### What are the risks?

Project failure. Token price decline. Low trading volume. Smart contract risk (mitigated by audits).

Diversify across projects. Only invest what you can lose. Do your own research.

[Learn risk management →](../for-investors/risk-management.md)

### Can I unstake my LP tokens?

Only if staked in VaultClaim. PatronClaim locks are permanent. No unstaking option.

VaultClaim allows early exit via OVL. Penalty: (Remaining Time / Total Time) × 50%.

[Understand OVL →](../core-concepts/open-vested-liquidity.md)

### Should I lock permanently or flexibly?

Depends on your commitment level. Permanent: 10x rewards but no exit. Flexible: 0.024x-5x rewards with exit option.

Risk-averse: flexible locks. High conviction: permanent locks. Can split across both.

[Maximize your returns →](../for-investors/maximizing-returns.md)

### How do I claim my rewards?

Call the claim function on PatronClaim or VaultClaim. Rewards transfer to your wallet.

Gas cost: ~$2-5. Claim whenever accumulated rewards exceed gas costs.

[See claiming guide →](../for-investors/staking-rewards-guide.md)

## Technical Questions

### What is the Template Factory?

The central deployment system. Uses EIP-1167 minimal proxy pattern. Creates lightweight contract clones.

Reduces gas from $1,000 to $15. Each clone is 300 bytes. Delegates to shared implementation.

[Learn the architecture →](../core-concepts/template-factory.md)

### What is EIP-1167?

Ethereum standard for minimal proxies. Creates tiny contracts that delegate to implementations.

74.7% gas savings. Battle-tested pattern. Used by major protocols.

[Technical details →](../technical/architecture-overview.md)

### What is the CEI pattern?

Checks-Effects-Interactions. Security pattern that prevents reentrancy attacks.

All Opals contracts follow CEI. Check conditions first. Update state second. Call externals last.

[Security architecture →](../for-founders/security-and-trust.md)

### How does the multiplier formula work?

For VaultClaim: multiplier = (lockDuration / 4 years) × 5x. For PatronClaim: multiplier = 10x always.

Linear scaling from 7 days (0.024x) to 4 years (5x). Permanent locks get 10x.

[See the math →](../core-concepts/patronpower-system.md)

### Can the contracts be upgraded?

No. Immutable after deployment. No admin can change core logic.

Only mutable parts: operator roles, pausing (emergency only). Economics cannot change.

[Understand immutability →](../for-founders/security-and-trust.md)

### What happens if there's a bug?

New projects would use fixed templates. Existing projects continue with deployed contracts.

Emergency pause available for critical issues. But core economics remain unchanged.

[See security measures →](../for-founders/security-and-trust.md)

### How is this different from bonding curves?

Bonding curves have continuous pricing. Opals uses discrete batches or fixed prices.

Prevents MEV exploitation. Reduces bot advantage. Better for community-first launches.

[Learn about anti-gaming →](../core-concepts/anti-gaming-mechanisms.md)

### Does Opals use oracles?

No. All pricing and mechanics are on-chain. No external data dependencies.

Reduces attack surface. No oracle manipulation possible. Simpler and more secure.

[Technical architecture →](../technical/architecture-overview.md)

### Can I integrate with Opals?

Yes. All contracts have standard interfaces. Build on top of deployed projects.

Example: Analytics dashboards, portfolio trackers, aggregators, governance tools.

[Developer documentation →](../technical/README.md)

### What testing framework does Opals use?

Foundry. 375 tests covering all contracts. Unit tests, integration tests, fuzz tests.

Run tests yourself: `forge test`. All tests public on GitHub.

[See the test suite →](../technical/testing.md)

## Troubleshooting

### My transaction failed. What happened?

Check error message. Common causes: insufficient gas, wrong price, sold out market, already claimed.

Most errors are self-explanatory. See detailed solutions below.

[Troubleshooting guide →](./troubleshooting.md)

### I can't claim my rewards. Why?

Possible reasons: Nothing to claim yet, not the NFT owner, claim period not open, lock not expired.

Check your PatronPower balance first. Verify you own the required NFTs.

[Claim troubleshooting →](./troubleshooting.md)

### Gas price seems too high. Is this normal?

Gas varies by network. Ethereum: $50-200. Base/Optimism: $2-10. Arbitrum: $1-5.

Deploy on L2s for lowest costs. Wait for low gas periods if possible.

[Gas optimization tips →](../for-investors/maximizing-returns.md)

### I sent ETH but didn't receive NFTs. Help?

Check transaction status. If confirmed, you should have NFTs. Check your wallet's NFT section.

If transaction failed, ETH was refunded (minus gas). Check error message.

[Transaction troubleshooting →](./troubleshooting.md)

### Can I get a refund on my Patron Cards?

Depends on market type. Stepped markets allow refunds before launch. Fixed markets generally don't.

After liquidity launch, no refunds. Cards are tradeable on secondary markets.

[Refund policies →](./troubleshooting.md)

## Advanced Questions

### How does OVL work mathematically?

Penalty = (Remaining Time / Total Time) × 50%. Redistributed to remaining stakers pro-rata.

Example: Exit at 50% of lock period = 25% penalty. You keep 75%, lose 25% to others.

[OVL deep dive →](../core-concepts/open-vested-liquidity.md)

### What prevents mercenary capital?

Exponential multiplier difference. 7-day lock: 0.024x. Permanent: 10x. That's 416x difference.

Makes quick flips economically worthless. Only long-term commitment earns real rewards.

[Anti-gaming mechanisms →](../core-concepts/anti-gaming-mechanisms.md)

### How does weight-based allocation work?

Each Patron Card has a weight. Usually 1, but can be higher for special cards.

Your share = (Your Weight × Your Multiplier) / Total PatronPower. Claim that percentage of LP.

[PatronPower formula →](../core-concepts/patronpower-system.md)

### Can projects have multiple tokens?

No. One project = one token. Keeps ecosystem simple and focused.

Launch separate projects if you need multiple tokens. Each gets its own liquidity.

[Tokenomics guide →](../core-concepts/tokenomics.md)

### How does WorkLock generate yield?

Deposits ETH into Aave V3. Earns lending interest. Claims periodically.

Interest converts to LP tokens. Distributed based on WorkLock participation.

[WorkLock mechanics →](../for-investors/staking-rewards-guide.md)

### What is the Distributor contract?

Collects protocol fees. Distributes to PatronClaim and VaultClaim holders. Weighted by PatronPower.

Permissionless. Anyone can trigger distribution. Gas-efficient batch operations.

[Distributor details →](../technical/contracts/Distributor.md)

### How are LP tokens allocated?

PatronClaim receives LP from liquidity launcher. Calculates each card's share by weight.

Supporters claim their allocation. LP stays in contract, earning fees. Claim fees, not LP.

[Token launch mechanics →](../for-founders/token-launch-mechanics.md)

### Can I vote with PatronPower?

Not built-in by default. Projects can add governance contracts that read PatronPower.

PatronPower is a primitive. Voting, proposals, execution are separate systems.

[Governance options →](../for-founders/launch-process.md)

## Still Have Questions?

Check the full documentation. Most questions are answered in detail.

**For Founders**: Start with the [Launch Process](../for-founders/launch-process.md)

**For Investors**: Start with [Getting Started](../for-investors/getting-started.md)

**For Developers**: Start with [Technical Docs](../technical/README.md)

**Can't find your answer?** Join the community Discord or submit a GitHub issue.
