# Keys

Every successful token launch faces a bot problem. The moment your market opens, automated scripts flood in, front-running real supporters, extracting value before community members even connect their wallets. By the time humans arrive, bots have claimed the best prices, the best allocations, the best positions. Your community launch becomes a bot harvest.

Keys solve this by making market participation conditional on NFT ownership. Set a Membership Card as the key for a market, and only Membership Card holders can participate in that sale round. Want to reward contributors first? Set Contributor Cards as the key. Want to create exclusive access for existing NFT communities? Set Azuki, Pudgy Penguins, or Bored Ape as the key. Own the right NFT, access the market. Don't own it, wait your turn.

## Access Control Becomes Composable

Traditional whitelists require backend databases, merkle trees, and trust in whoever controls the list. Projects manually verify addresses, update lists, hope they didn't miss anyone or include bots. It's labor-intensive, error-prone, and ultimately centralized. One person controls who gets access.

Keys make access control a composable primitive. The smart contract checks: does this wallet hold the required NFT? Yes means proceed, no means revert. No backend. No manual verification. No central authority deciding who belongs. Just on-chain NFT ownership enforcing market access automatically. NFTs are perfect for this cause they are unique and trivial to verify that Card #4 has claimed, and #5 has not.


## Natural Tiering Through NFT Ownership

When projects create markets, they configure which NFT collections can participate. Maybe the first market is members-only: only wallets holding Membership Cards can buy. After that sells out, open a second market to contributors: only Contributor Card holders. Finally, open a third market to the public with no key required.

This creates natural tiering. Early believers who earned Membership Cards get first access at the best prices. Contributors who built value get second access. The broader public gets third access at higher prices. Everyone knows the rules upfront. No favoritism. No surprise allocations. Just transparent prioritization based on verifiable on-chain credentials.

Projects can even use external NFT collections as keys. Want Bored Ape holders to have priority access? Set BAYC as the key. Want to target Pudgy Penguins community? Use PENGU as the key. This creates composability across the NFT ecosystem, your existing NFT holdings unlock opportunities in new projects launching on Opals.

## The Bot Filter

Bots can't fake NFT ownership. They can't mint Membership Cards without participating in the community. They can't earn Contributor Cards without doing actual work. They can't acquire Bored Apes just to bot your presale, the economic barrier is too high.

Keys turn NFTs into proof-of-participation. If you hold the key NFT, you proved yourself somehow: joined early, contributed value, or bought into an established community. That proof costs time, effort, or capital that bots typically won't invest for marginal arbitrage opportunities.

This doesn't make bot attacks impossible, but it makes them economically irrational for most small-scale launches. The barrier to entry for keys is high enough to deter automated farming while low enough that genuine community members can participate.

## Multiple Markets, Multiple Keys

Projects aren't limited to one market or one key. Launch multiple markets over time, each with different keys and different pricing. Members-only market first at stepped prices starting at 0.1 ETH. Contributors market second at linear pricing from 0.2 ETH. Public market third at fixed 0.3 ETH. Each tier rewards different community segments appropriately.

This flexibility lets projects adapt distribution strategy to their community dynamics. If your project values early community formation, use Membership Cards as keys for 80% of supply. If you value builders, allocate significant supply to Contributor-keyed markets. If you want broad distribution, save substantial allocation for public markets with no keys.

Different markets can even have different capital splits. Members market might send 90% to the launcher because those believers want liquidity. Public market might send 50/50 because the launcher threshold is nearly met. Keys don't just control who participates, they're part of a broader distribution architecture that shapes how your community forms and how your capital flows.

## The Composable Primitive

Keys transform access control from an operational problem into a composable protocol feature. Instead of managing whitelist spreadsheets and merkle trees, projects simply configure which NFT collections unlock which markets. The blockchain handles verification. The smart contracts enforce access. The system runs itself.

This is access control that scales, from member-only presales to cross-community collaborations to public launches. All enforced by the same primitive: own the key NFT, access the market. Simple, trustless, and impossible to fake.
