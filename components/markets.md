# Markets

Every token launch faces the same question: how do you distribute ownership fairly while raising the capital you need? Traditional launches handle this poorly. VCs restrict youy to offchain SAFTs, Bonding curves turn communities into PvP arenas where everyone's trying not to be the greater fool.

Markets change this. Opals's Markets are the core mechanism that raise capital, giving projects the flexibility to choose how, when, and to whom they distribute ownership. At their heart, Opals' Markets are smart contracts that sell digital assets and issue Cards in return. But unlike traditional launchpads, Opals' Markets are modular. 

## Why Markets Matter

The way you distribute Cards determines the community you create. Sell too fast, and you reward speed over conviction. Use bonding curves, and you create front-running wars. Launch without considerations for the community, and bots extract all the value before real supporters can participate.

Opals Markets solve this by making distribution programmable. Want to reward early believers with better prices? Use stepped pricing. Need to ensure only community members can participate? Implement key-based access control. Want to split proceeds between operations and the token launcher? Configure multiple destination addresses. Every market decision shapes the community you're building.

## Keys: Controlling Who Participates

Not every market should be open to everyone. Sometimes you want to reward existing community members. Sometimes you need to prevent bot participation. Sometimes exclusivity creates value.

Keys solve this by gating market access based on Card ownership. If you set a Membership Card as the key for a market, only existing members can participate in that sale round. This lets projects create tiered launches: maybe members-only for the first week, then public after that. Or contributor-only presales before opening to the broader community. We have wrapper contracts that can add more than one collection as keys, so you can have a members-only market for one market, and Azuki, Pudgy and Bored Apes holders as keys for the other.

Keys turn access control from a backend problem into a composable primitive. Own the right Card, participate in the market. Don't own it, wait your turn or acquire one through other means.

## Pricing Strategies: 

Markets support multiple pricing strategies, each solving different problems:

**Stepped Pricing** Cards sell in fixed rounds at increasing prices. First 1,000 at 0.1 ETH, next 1,000 at 0.3ETH, final 1,000 at 0.5 ETH. This rewards early believers with better prices while creating natural urgency. Front-running doesn't work because you can't skip rounds. Bots can't game, if they did, they would have to buy the entire round, and becomes economically irrational when combined with diamond hand vesting. 

**Linear Pricing** is coming next. Instead of fixed rounds, contributors can buy whatever amount they want whenever they want, with price increasing linearly based on total sold. No artificial cutoffs. No round boundaries. Just smooth price discovery that rewards earlier participation without the race to be first on an exponential price curve. Vesting periods need to be longer, and the price increase capped to 5x the minimum price, but allows for more flexibility in contributions of any size, and suitable for projects with a larger community.

**Dutch Auctions** will enable true price discovery. Start high, decrease over time until all Cards sell. Everyone who participates pays the final clearing price. This finds fair market value without speculation or gaming. The community collectively determines what the Cards are worth. We have some interesting ideas to make this more exciting, but it's not ready yet.


## Multiple Markets: Phased Distribution

Projects don't launch once they raise capital in rounds. Maybe you do a stepped pricing presale for early supporters, then six months later run a Dutch auction to distribute remaining Cards at fair market value. Or a members-only market, followed by a public round.

Opals supports multiple markets per project. Each market can have its own pricing strategy, its own access keys, its own capital split between operations and the launcher. This lets projects adapt their distribution strategy as they grow, running new markets when they need fresh capital or want to expand the community.

## Capital Allocation: Operations and Launch

Every market splits proceeds between two destinations: project operations and the token launcher. Projects configure this split when they create the market. Maybe 80% goes to the launcher to ensure deep liquidity, 20% to operations for runway. Or 50/50 if the project needs more immediate capital.

Different markets can have different splits. Early presale might send 20% to the launcher because runway matters most. Later rounds might send 80% to the launcher because the threshold is nearly met and the token is ready to launch.

This flexibility ensures capital flows where it's needed most.

