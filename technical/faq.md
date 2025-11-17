# Frequently Asked Questions

## For Founders

**Q: Why should I launch on Opals instead of other platforms?**

Other platforms charge upfront fees plus token percentages, then maybe list you after committee approval. Opals charges nothing upfront, claims zero tokens, and deploys your complete launch infrastructure in one atomic transaction. The difference isn't marketing promises, it's immutable code that does exactly what it says with no possibility of human interference.

**Q: Do I need to know Solidity to deploy on Opals?**

No. Fill out a form specifying your token name, supply, card pricing, and capital split. Click deploy. Nine smart contracts clone from audited templates using EIP-1167 minimal proxies. You need to understand Solidity to use Opals the same way you need to understand TCP/IP to use the internet, which is to say not at all.

**Q: How efficient is deployment?**

The EIP-1167 minimal proxy pattern creates highly efficient deployments by referencing master contracts rather than redeploying identical logic. Deployment happens in a single atomic transaction and takes about five minutes from form submission to live ecosystem. Layer 2 networks like Base or Arbitrum offer even greater efficiency.

**Q: Can I customize my token launch?**

You configure token supply, card pricing strategy (stepped, linear, fixed), capital allocation split, vesting schedules, and reward multipliers during deployment. These parameters become immutable once set. The templates cover 95% of use cases because 95% of projects need the same fundamental mechanisms: fair distribution, permanent liquidity locks, and sustainable reward systems.

**Q: What happens to the liquidity after launch?**

Eighty percent of raised capital converts to permanent liquidity through OpalSwap. The resulting LP tokens lock forever in claim contracts with no withdrawal function. This isn't a promise or policy, it's a mathematical impossibility. The smart contract code lacks any function to extract locked liquidity. Rug pulls become impossible, not difficult.

## For Supporters & Investors

**Q: What do I get when I buy a Patron Card?**

Permanent ownership of locked LP tokens that generate trading fee rewards forever. Your card represents both token allocation rights through vesting plus perpetual fee distribution through PatronPower. Cards are tradeable NFTs on OpenSea. Sell the card and economic rights transfer automatically. Hold the card and rewards accumulate continuously.

**Q: How do I earn rewards from my cards?**

Every trade on OpalSwap pays a 1% fee. These fees flow to the Distributor contract and accumulate continuously. Your share depends on your PatronPower relative to total PatronPower across all participants. Claim anytime by calling the claim function. Rewards come from real trading activity, not token inflation.

**Q: What is PatronPower and why does it matter?**

PatronPower is the time-weighted multiplier that determines your share of fee distribution. Lock LP tokens for seven days: 1.024x multiplier. Lock for one year: 3.75x. Lock for four years: 10x. Lock permanently: 10x. A supporter with one thousand dollars locked permanently earns more than a whale with forty-one thousand locked for seven days. Time defeats capital.

**Q: Can I sell my Patron Card?**

Yes. Patron Cards are standard ERC-721 NFTs tradeable on OpenSea or any NFT marketplace. When you sell, all economic rights transfer to the new owner: LP allocation, token claims, fee distribution. The card-level accounting means no migration or contract interaction required. Ownership transfer happens automatically through the NFT transfer.

**Q: What happens if I claim my tokens early?**

Diamond hand vesting penalizes early claims. If only 25% of your allocation has vested and you claim, you receive that 25% but forfeit the remaining 75% to holders who wait. Forfeited tokens redistribute to remaining card holders proportionally. Wait until full vesting completes and you receive your complete allocation plus bonuses from those who claimed early.

**Q: How does WorkLock provide risk-free participation?**

Deposit USDC into WorkLock. Your principal immediately stakes in Aave V3 to earn interest. You can withdraw your full USDC deposit anytime with zero penalty. The accumulated interest (not your principal) converts to LP tokens that generate PatronPower rewards. Your downside: zero. Your upside: Aave interest plus PatronPower fee distribution from LP conversion.

## Technical

**Q: Can the contracts be upgraded or changed?**

Core economic logic is immutable. Token supply, fee percentages, liquidity locks, and distribution mechanisms freeze at deployment. No admin keys exist to modify these fundamental rules. Some operational aspects like adding operators or pausing markets in emergencies remain configurable. But promises enforced by code cannot be broken because the code cannot be changed.

**Q: What blockchains does Opals support?**

Contracts are deployed on Monad and Mainnet but are EVM-compatible. Gas costs vary significantly by network: fifty dollars on mainnet versus fifty cents on Layer 2 for the same transactions.

**Q: How does OpalSwap differ from Uniswap?**

OpalSwap is Opals' custom DEX with built-in zap functionality. Deposit single-sided ETH or USDC, OpalSwap automatically swaps 50% for project tokens and creates LP in one transaction. No manual balancing required. Additionally, OpalSwap charges 1% trading fees versus Uniswap's 0.3%, with all fees flowing to the tokens distributor contracts.

## Economic

**Q: What fees does Opals charge?**

Four percent fee on Patron Card sales during the market phase, split equally: 25% to project creator (immediate operational runway), 25% to Opals protocol, 25% to platform referrer, 25% to order referrer. One percent trading fee on OpalSwap distributed to PatronPower holders. No deployment fees. No token percentage claims. Ever.

**Q: Where do rewards come from?**

Trading fees, not token inflation. Every swap on OpalSwap pays 1% to the Distributor. These are real fees from real trading activity. If volume drops, rewards drop proportionally. If volume grows, rewards grow sustainably. This honesty prevents the fake yields that attract mercenary capital and collapse when inflation stops.

**Q: What are the risks?**

Project failure (most projects fail). Token price decline even if the project succeeds. Low trading volume meaning low fee distribution. Smart contract risk despite audits and testing. Opportunity cost from locked capital. What's not on the list: rug pulls (impossible), token dilution (fixed supply), liquidity removal (no function exists), team dumping (they own maximum 20%).

**Q: Can I get a refund if I change my mind?**

Patron Card holders can claim 80% of their investment back before token launch by burning their card. This exit mechanism provides liquidity for supporters who need capital before the project completes. After token launch, cards represent vested token claims and locked LP positions, not refundable ETH.

## Process

**Q: How long does the launch process take?**

Deployment: 5 minutes. Card sales: hours to weeks depending on community demand and capital threshold. Token launch: automatic when threshold reached. First fee distributions: immediate once trading begins. The entire process is event-driven, not time-driven. Progress depends on market response, not arbitrary calendars.

**Q: What happens if we don't reach the funding threshold?**

Markets can be configured with minimum thresholds. If the threshold isn't reached, supporters can claim refunds. Alternatively, projects can launch with whatever capital accumulated. The smart contract enforces the rules set during deployment. No human intervention required.

**Q: How do I track my rewards?**

Call the view functions on Distributor and Claim contracts to see accumulated rewards. Most projects will build dashboards showing real-time earnings, PatronPower calculations, and claim history. The blockchain data is public and verifiable. You can independently verify your rewards at any time.

**Q: Can multiple people collaborate on one project?**

Yes. Set operator roles during deployment or add them later. Operators can create markets, pause sales in emergencies, and manage operational aspects. But operators cannot modify economic rules, unlock liquidity, or change token supply. The separation between operational flexibility and economic immutability is enforced by the smart contracts.
