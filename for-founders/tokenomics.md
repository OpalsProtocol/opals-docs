# Tokenomics Example

This walkthrough demonstrates a complete token launch using Opals with specific numbers. Follow the mathematics to understand how capital flows, tokens distribute, and holders earn.

## The Setup

**Project**: DeFi protocol raising capital for development
**Target raise**: $200,000 (80 ETH at $2,500/ETH)
**Target FDV**: $1,000,000
**Total supply**: 1,000,000,000 tokens (fixed, no inflation)

**Allocation**:
- 800,000,000 tokens (80%) � Patron Card holders
- 150,000,000 tokens (15%) � Liquidity pool
- 30,000,000 tokens (3%) � Team (4-year vesting)
- 20,000,000 tokens (2%) � Treasury operations

## Card Sales: Three Rounds

**Round 1 - Members Only** (Membership Card required as Key)
- Cards available: 2,000
- Price per card: 0.008 ETH ($20)
- Total raised: 16 ETH ($40,000)
- Tokens per card: 100,000

**Round 2 - Contributors** (Contributor Card required as Key)
- Cards available: 3,000
- Price per card: 0.011 ETH ($27.50)
- Total raised: 33 ETH ($82,500)
- Tokens per card: 100,000

**Round 3 - Public** (No Key required)
- Cards available: 3,000
- Price per card: 0.0103 ETH ($25.75)
- Total raised: 31 ETH ($77,500)
- Tokens per card: 100,000

**Total**: 8,000 cards sold, 80 ETH raised ($200,000)

Each card represents 100,000 tokens that vest over 4 years. Early round supporters pay less per card, rewarding commitment and early belief.

## Capital Split After Launch

**Gross raise**: 80 ETH
**Platform fees** (4%): 3.2 ETH
- Creator: 0.8 ETH (25%)
- Protocol: 0.8 ETH (25%)
- Platform referrer: 0.8 ETH (25%)
- Order referrer: 0.8 ETH (25%)

**Net to project**: 76.8 ETH

**80/20 Split**:
- To launcher (liquidity): 61.44 ETH (80%)
- To treasury (operations): 15.36 ETH (20%)

The 20% treasury allocation provides immediate operational runway. The 80% liquidity allocation ensures deep, permanent liquidity.

## Token Launch

When the 8,000 card threshold is reached, the Launcher executes automatically:

**Liquidity pool creation**:
- ETH deposited: 61.44 ETH ($153,600)
- Tokens deposited: 150,000,000 tokens
- Initial price: 61.44 ETH / 150,000,000 tokens = 0.0000004096 ETH per token
- In USD: $0.001024 per token
- LP tokens: Locked permanently in claim contracts

**Market cap at launch**:
- Circulating supply: ~150M tokens (in LP)
- Price: $0.001024
- Market cap: $153,600
- Fully diluted valuation: $1,024,000

Close to target $1M FDV with slight premium due to rounding.

## Diamond Hand Vesting Examples

All Patron Card holders receive 100,000 tokens vesting over 4 years (linear). Claiming early forfeits unvested tokens to remaining holders.

**Alice - The Impatient (Year 1)**
- Vesting progress: 25%
- Tokens vested: 25,000
- Tokens forfeited: 75,000
- Token price: $0.002 (2x from launch)
- Value received: $50
- Value forfeited: $150

**Bob - The Patient (Year 4)**
- Vesting progress: 100%
- Tokens from allocation: 100,000
- Bonus from forfeited: ~75,000 (if half claim early)
- Total tokens: 175,000
- Token price: $0.01 (10x from launch)
- Value received: $1,750

**The Mathematics**:
If 4,000 card holders (50%) claim at year 1:
- Each forfeits: 75,000 tokens
- Total forfeited: 300,000,000 tokens
- Remaining holders: 4,000
- Bonus per holder: 300M / 4,000 = 75,000 tokens

Diamond hands earn 75% more tokens simply by waiting. Combined with price appreciation, the patient earn exponentially more.

## Price Discovery and Trading

**Month 1 - Initial volatility**:
- Launch price: $0.001024
- Speculators buy: Price rises to $0.002
- Some early claimers sell: Price stabilizes at $0.0015
- Trading volume: $500k monthly
- Fees generated: $5,000 (1% of volume)
- Distributed to PatronPower holders

**Month 6 - Product traction**:
- Protocol launches beta
- Community grows, usage increases
- Price: $0.005 (5x)
- Trading volume: $2M monthly
- Fees: $20,000
- PatronPower holders earn: Proportional to locked LP

**Year 2 - Market maturity**:
- Protocol achieves product-market fit
- Price: $0.015 (15x from launch)
- Trading volume: $10M monthly
- Fees: $100,000 monthly
- Sustainable yield for long-term holders

## Investor Return Scenarios

**Scenario A - Round 1 Member, Immediate Claim**:
- Investment: 0.008 ETH ($20)
- Claim at launch: 0 tokens (0% vested)
- Forfeit: 100,000 tokens
- Loss: $20

Never claim immediately. Wait at minimum for partial vesting.

**Scenario B - Round 1 Member, Year 1 Claim**:
- Investment: 0.008 ETH ($20)
- Tokens received: 25,000
- Token price: $0.002
- Value: $50
- ROI: 150%
- Forfeited upside: 75,000 tokens worth $150

**Scenario C - Round 1 Member, Year 4 Diamond Hands**:
- Investment: 0.008 ETH ($20)
- Tokens received: 175,000 (100k + 75k bonus)
- Token price: $0.01
- Value: $1,750
- ROI: 8,650%

**Scenario D - Round 3 Public, Year 4 Diamond Hands**:
- Investment: 0.0103 ETH ($25.75)
- Tokens received: 175,000
- Token price: $0.01
- Value: $1,750
- ROI: 6,696%

Round 1 members paid less for same allocation, demonstrating stepped pricing benefits.

## Fee Distribution Mechanics

With 61.44 ETH locked in liquidity forever, PatronPower holders earn from trading fees.

**PatronPower calculation**:
- Patron Cards (permanent lock): 10x multiplier
- Total locked value: 61.44 ETH
- Total PatronPower: 614.4 ETH-equivalent

**Monthly fee distribution** (assuming $10M volume):
- Fees generated: $100,000
- Your PatronPower: 6.144 (from 1 card)
- Your share: 6.144 / 614.4 = 1%
- Your monthly earnings: $1,000
- Annual yield: $12,000 on $20-$26 investment

These fees come from real trading activity, not token inflation. Sustainable as long as the protocol generates volume.

## Token Price Drivers

**Positive pressure**:
- Protocol adoption increasing
- Trading fees attract LP providers
- Diamond hands reduce circulating supply
- Bull market sentiment

**Negative pressure**:
- Early claimers selling vested tokens
- Broader market downturn
- Protocol usage declining
- Competitive products launching

The permanent liquidity lock prevents the worst-case scenario (rug pull) while allowing natural price discovery.

## Why This Model Works

**For early members**: Pay less ($20), wait longer, earn more (175k tokens at $0.01 = $1,750)

**For late participants**: Pay market rate ($26), same allocation if patient, immediate liquidity to exit

**For the project**: 20% ($40k) operational capital immediately, 80% permanent liquidity ensures tradability forever

**For long-term holders**: Fee distribution creates perpetual income, diamond vesting multiplies tokens, fixed supply prevents dilution. 

The mathematics align every participant toward the same outcome: long-term protocol success.
