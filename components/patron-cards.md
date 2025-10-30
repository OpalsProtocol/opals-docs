# Patron Cards

Patron Cards are ERC721 NFTs that represent permanent ownership stakes in a project's liquidity pool. They're the core component that ties everything together.

## What Patron Cards Do

**Simple view**: You buy a Patron Card → Receive a claim on project's permanent liquidity → Earn rewards forever.

**Technical view**: ERC721 NFT with LP allocation rights. Card holder gets:
1. Permanent claim on LP tokens (via PatronClaim contract)
2. PatronPower multiplier (10x for card holders)
3. Trading fee distribution (from Distributor)
4. Protocol fee rewards (from project)

## How They Work in the System

**During launch phase**:
- Cards minted by Market contract
- Each card = 1 entry in allocation system
- Cards sit in buyer's wallet

**After Uniswap launch**:
- PatronClaim allocates LP tokens proportionally to card holders
- Each card's share = (card weight / total weight) × total LP tokens
- Rewards distribute based on PatronPower

**Permanently**:
- Cards tradeable on secondary markets
- Economic rights stay with card owner
- New holder gets all rewards going forward

## The Permanent Lock Guarantee

**What's locked**: LP tokens in PatronClaim contract

**Why locked**:
- PatronClaim contract has no withdrawal function
- No admin keys exist
- Cannot be removed by anyone, ever
- Mathematical guarantee, not a promise

**What this means for card holders**:
- Liquidity cannot be rugged
- Rewards flow in perpetuity
- Project cannot remove LP later
- Your share is protected by smart contract

## Card Economics

### Allocation Example

100 projects raises 100 ETH, allocates 40% to liquidity.

Patron Cards:
- Total supply: 1,000 cards
- Total LP allocation: 40 ETH worth of tokens + 40 ETH

Per card allocation:
- Each card gets: 40 ETH ÷ 1,000 = 0.04 ETH worth of LP tokens
- If you hold 10 cards: 0.4 ETH worth

### PatronPower Multiplier

Cards get 10x multiplier by default (vs 0.024x for 7-day stakers).

Your reward share = (LP tokens × 10) / total PatronPower

Example:
- You: 10 cards × base weight = 1,000 PatronPower
- Whale: 1M worth locked 7 days = 10,000 PatronPower
- Your share: 1,000 / 11,000 = 9% of rewards
- Whale's share: 10,000 / 11,000 = 91% of rewards

Despite whale having 100x more capital, you get 10% of rewards. This is PatronPower in action.

## Secondary Market Trading

Cards are fully transferable NFTs.

- Trade on OpenSea, Rarible, or other NFT markets
- Buyer gets all economic rights going forward
- Price determined by market (often above/below intrinsic LP value)
- No lock periods - instant liquidity

Example: Buy card for 1 ETH, later sell for 2 ETH on secondary market. Profit taken, but miss out on future rewards from that card.

## Technical Implementation

**Contract**: PatronCard.sol (ERC721 extension)

**Minting**: Market contracts mint during sale phase

**Burning**: Not supported (cards permanent)

**Metadata**: Card metadata can include rarity tiers or custom attributes set by projects

**Integration**: Works with PatronClaim for reward calculations
