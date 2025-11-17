# Claims

After three market cycles, one pattern became clear: token vesting is theater. Founders promise lockups, then quietly unlock early. Teams claim four-year vesting, then find creative ways to liquidate immediately. Investors negotiate cliffs, then dump the moment their tokens unlock. The promises mean nothing when they're not enforced by code.

Claim contracts change everything. These aren't promises. These aren't trust-based agreements. These are immutable smart contracts deployed from day one that enforce token distribution exactly as specified, forever. When tokens are allocated to claim contracts, they're locked until conditions are met. No founders can change it. No governance can override it. No market conditions can alter it. The code is law.

## Patience Becomes Profitable

Most projects fail because early supporters dump immediately after token launch. The team raises capital, builds for months, launches the token, and within hours the price collapses as everyone exits. This isn't because the project is bad, it's because the incentives are broken.

Claim contracts solve this by making patience profitable and conviction rewarding. When tokens are allocated to a claim contract, Cards can only claim them if certain conditions are met. These conditions are programmed from day one, trustless and immutable.

For example, when the token launcher raises enough capital to meet the project's threshold, the claim contracts unlock. Projects can set this threshold at deployment, maybe $100K, maybe $5M, whatever ensures sufficient liquidity for a healthy launch. If the threshold isn't met, tokens remain locked. If it is, claims become available.

This creates certainty. Card holders know exactly when they can claim. Projects know exactly when distribution begins. There's no guessing, no governance votes to extend vesting, no founder discretion to change terms. The smart contract enforces what was promised.

## The Two Core Claim Types

Opals v2 launches with two claim contracts, each serving a different role in the token distribution system.

### Presale Claim: Diamond Hand Vesting

The Presale Claim is where tokens allocated to Presale Cards are held. This is diamond hand vesting in its purest form.

Here's how it works: You can claim your tokens at any time after launch, but you can only claim once. If you claim early during the vesting period, you forfeit your unvested tokens to the remaining Card holders who haven't claimed yet.

Let's say you hold a Presale Card with 1,000 tokens vesting over four years. Claim at year one when only 25% has vested, and you receive 250 tokens while forfeiting 750 to those still waiting. Claim at year four when fully vested, and you receive your full 1,000 tokens plus your share of what others forfeited.

This creates mathematical incentive alignment. Early claimers subsidize diamond hands. Weak hands strengthen strong hands. Natural selection operates through smart contract logic.

But there's more. Presale Cards don't just get their vested allocation, they also receive tokens from the distributor contract. As trading happens on OpalSwap, 1% fees flow to the distributor, and a portion of those fees get converted to tokens and allocated to Presale Card holders.

These tokens accumulate in the Presale Claim contract until you decide to claim them. Once you claim, you receive everything that's vested plus everything that's accumulated from fees. But you can't claim again. This creates a powerful dynamic: the longer you wait, the more you accumulate, but you must choose the moment wisely because there's no second chance.

### Vault Claim: Locked LP Rewarder

The second claim contract is the Vault Claim. This is where all tokens allocated to locked liquidity providers are held.

Unlike the Presale Claim which is for Presale Cards only, the Vault Claim distributes tokens to anyone who has locked LP tokens in vaults. This includes Presale Card holders who have LP allocations, but also anyone who missed the presale and instead provided liquidity on OpalSwap and locked it.

The Vault Claim distributes tokens based on PatronPower. The longer your LP is locked, the higher your PatronPower multiplier (from 1.024x for 7 days to 10x for 4 years), and the more tokens you can claim from the Vault.

The key difference: Vault Claims are only for locked LPs. You either need to have been allocated LP through a Presale Card, or you need to have provided liquidity yourself and locked it in a vault. No LP lock, no Vault Claim.

This ensures that token distribution flows to those who contribute liquidity to the ecosystem, not just those who hold tokens. It's alignment through capital commitment, not speculation.

## Code as Constitution

This is the fundamental shift Opals brings to token launches. Vesting isn't a promise, it's code. Distribution isn't at the discretion of founders, it's programmed. Claims aren't managed by administrators, they're enforced by immutable smart contracts.

When you hold a Card on Opals, you know exactly what you're getting and when you can get it. The Presale Claim rewards patience through diamond hand vesting. The Vault Claim rewards liquidity through PatronPower multipliers. Both are immutable, both are trustless, both are there forever.

This is how you build projects that outlast their founders. This is how you create digital institutions, not exit liquidity. Smart contracts as actual contracts, unbreakable commitments that outlive their creators.
