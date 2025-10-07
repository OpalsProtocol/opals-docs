# Integration Guide

This guide provides step-by-step instructions for integrating with the Opals Protocol, from environment setup through production deployment.

## Environment Setup

### Prerequisites

**Required Tools:**
- [Foundry](https://book.getfoundry.sh/) - Solidity development toolkit
- [Node.js](https://nodejs.org/) v18+ - JavaScript runtime
- [Git](https://git-scm.com/) - Version control

**Install Foundry:**

```bash
# Install Foundry
curl -L https://foundry.paradigm.xyz | bash
foundryup

# Verify installation
forge --version
cast --version
anvil --version
```

**Clone Repository:**

```bash
git clone https://github.com/OpalsProtocol/opals-contracts.git
cd opals-contracts

# Install dependencies
forge install
yarn install  # Optional, for deployment scripts
```

### Configuration

**Create .env file:**

```bash
# Private key for deployments (NEVER commit this)
PRIVATE_KEY=0x...

# RPC endpoints
BASE_SEPOLIA_RPC=https://sepolia.base.org
MONAD_TESTNET_RPC=https://testnet-rpc.monad.xyz

# Etherscan API key (for verification)
ETHERSCAN_API_KEY=your_key_here

# Admin addresses
DEPLOYER_ADDRESS=0x...
TREASURY_ADDRESS=0x...
```

**Load environment:**

```bash
source .env
```

### Build and Test

```bash
# Compile all contracts
forge build

# Run full test suite (375 tests)
forge test

# Run with verbosity for debugging
forge test -vvvv

# Run specific test
forge test --match-test testPatronClaimRewards

# Run specific test file
forge test --match-path test/templates/core/PatronClaim.t.sol

# Gas reporting
forge test --gas-report

# Coverage analysis
forge coverage
```

## Deployment Patterns

### Pattern 1: Recipe-Based Deployment (Recommended)

Deploy a complete project ecosystem in a single transaction using `OpalsRecipe`.

**Use Case:** Standard token launch with crowdfunding, staking, and liquidity.

**Code Example:**

```solidity
// Get factory and recipe contracts
OpalsFactory factory = OpalsFactory(FACTORY_ADDRESS);
OpalsRecipe recipe = OpalsRecipe(RECIPE_ADDRESS);

// Define market configuration
OpalsRecipe.MarketConfig memory marketConfig = OpalsRecipe.MarketConfig({
    basePrice: 0.01 ether,           // Starting price
    priceIncrement: 0.001 ether,     // Price increase per batch
    itemsPerPackage: 10,             // Items per batch
    numberOfPackages: 100,           // Total batches
    maxSupply: 1000,                 // Total NFTs
    patronCardBaseUri: "ipfs://...", // Metadata URI
    launcherAllocation: 5000         // 50% to liquidity
});

// Define launcher configuration
OpalsRecipe.LauncherConfig memory launcherConfig = OpalsRecipe.LauncherConfig({
    tokenSupplyForLP: 500_000 * 1e18,  // Tokens for LP
    uniswapRouter: UNISWAP_ROUTER,      // Router address
    uniswapFactory: UNISWAP_FACTORY     // Factory address
});

// Deploy complete project
(
    address project,
    address market,
    address patronClaim,
    address vaultClaim,
    address launcher,
    address distributor
) = recipe.deployProject(
    "MyProject",        // Project name
    admin,              // Admin address
    marketConfig,
    launcherConfig
);

console.log("Project deployed:", project);
console.log("Market deployed:", market);
console.log("PatronClaim deployed:", patronClaim);
```

**What Gets Deployed:**

1. Project (coordination hub)
2. Token (ERC20 with 1e27 supply)
3. Operator (access control)
4. SteppedMarket (NFT sales)
5. PatronClaim (10x multiplier rewards)
6. VaultClaim (0-5x flexible staking)
7. Patron Card (ERC721 for PatronClaim)
8. Vault Card (ERC721 for VaultClaim)
9. LiquidityLauncher (Uniswap integration)
10. Distributor (protocol fee distribution)

**Gas Cost:** ~2M gas (~$200 at 100 gwei)

### Pattern 2: Custom Template Deployment

Deploy specific components for custom configurations.

**Use Case:** Unique economic models or integration with existing infrastructure.

**Code Example:**

```solidity
OpalsFactory factory = OpalsFactory(FACTORY_ADDRESS);

// Deploy project
bytes memory projectInit = abi.encode("ProjectName", admin);
address project = factory.deployContract(
    keccak256("PROJECT"),
    projectInit
);

// Deploy token
bytes memory tokenInit = abi.encode("MyToken", "TKN", project);
address token = factory.deployContract(
    keccak256("TOKEN"),
    tokenInit
);

// Deploy custom market with specific parameters
bytes memory marketInit = abi.encodeWithSignature(
    "init(address,address,uint256,uint256,uint256,uint256,uint256,string,uint256)",
    project,
    card,
    0.05 ether,     // basePrice
    0.01 ether,     // priceIncrement
    5,              // itemsPerPackage
    20,             // numberOfPackages
    100,            // maxSupply
    "ipfs://...",   // baseUri
    7500            // launcherAllocation (75%)
);
address market = factory.deployContract(
    keccak256("STEPPED_MARKET"),
    marketInit
);

// Wire components together
Project(project).addMarket(market, card);
Project(project).addClaim(patronClaim, card);
```

**Benefits:**
- Maximum control over parameters
- Custom component selection
- Integration with existing contracts
- Granular gas optimization

### Pattern 3: Integration with Existing Projects

Add Opals features to existing projects.

**Use Case:** Existing NFT collection wants to add staking rewards.

**Code Example:**

```solidity
// Existing NFT contract
IERC721 existingNFT = IERC721(0x...);

// Deploy PatronClaim for existing NFT
bytes memory claimInit = abi.encode(
    project,          // New project for tracking
    existingNFT,      // Existing NFT contract
    lpToken           // LP token to distribute
);
address patronClaim = factory.deployContract(
    keccak256("PATRON_CLAIM"),
    claimInit
);

// Add card set for existing NFT collection
IPatronClaim(patronClaim).addCardSet(
    address(existingNFT),  // Card contract
    1000,                   // Weight per card
    10000                   // Max supply
);

// Set LP tokens for distribution
IPatronClaim(patronClaim).setLPTokensForCardSet(
    0,                      // Card set index
    lpTokenAmount           // LP tokens to allocate
);

// Users can now claim rewards
uint256[] memory tokenIds = new uint256[](1);
tokenIds[0] = myTokenId;
IPatronClaim(patronClaim).claimTokensForNFTs(tokenIds, tokenToWithdraw);
```

**Benefits:**
- No migration needed for existing NFTs
- Adds value to existing community
- Gradual feature rollout possible
- Maintains existing contracts

## Configuration Best Practices

### Market Configuration

**Stepped Market Pricing:**

```solidity
// Bot-resistant configuration
MarketConfig({
    basePrice: 0.01 ether,          // Entry price
    priceIncrement: 0.005 ether,    // 50% increase per batch
    itemsPerPackage: 10,             // Batch size
    numberOfPackages: 50,            // Total batches
    maxSupply: 500,                  // Total supply
    patronCardBaseUri: "ipfs://Qm...",
    launcherAllocation: 5000         // 50% to LP
});
```

**Rationale:**
- Small batches (10) reduce bot advantage
- Large price increments (50%) discourage speculation
- 50% to LP ensures healthy initial liquidity
- 500 total supply balances scarcity with accessibility

**Fixed Market Pricing:**

```solidity
// Simple membership model
FixedMarketConfig({
    price: 0.1 ether,               // Fixed price
    maxSupply: 1000,                 // Total members
    patronCardBaseUri: "ipfs://Qm...",
    launcherAllocation: 6000         // 60% to LP
});
```

### Liquidity Configuration

**Conservative (High Liquidity):**

```solidity
LauncherConfig({
    tokenSupplyForLP: 600_000 * 1e18,  // 60% of supply
    uniswapRouter: router,
    uniswapFactory: factory
});
```

**Benefits:** Lower slippage, better price stability, less volatility

**Aggressive (Low Liquidity):**

```solidity
LauncherConfig({
    tokenSupplyForLP: 200_000 * 1e18,  // 20% of supply
    uniswapRouter: router,
    uniswapFactory: factory
});
```

**Benefits:** Higher price appreciation potential, more tokens for rewards/team

**Recommended:** 40-60% of supply to LP

### Staking Configuration

**VaultClaim Lock Periods:**

```solidity
// Allow flexible staking
uint256[] memory lockPeriods = [
    7 days,      // 0.024x multiplier
    30 days,     // 0.104x multiplier
    90 days,     // 0.308x multiplier
    180 days,    // 0.616x multiplier
    365 days,    // 1.25x multiplier
    730 days,    // 2.5x multiplier
    1460 days    // 5x multiplier
];

// Users choose lock duration for desired multiplier
vaultClaim.stakeLP(amount, lockPeriods[userChoice]);
```

**Design Considerations:**
- Longer locks = higher multipliers (0-5x)
- Early exit available with 0-50% penalty
- Penalties redistribute to diamond hands
- Permanent locks get 10x multiplier

## Event Listening and Monitoring

### Critical Events to Monitor

**Project Lifecycle:**

```javascript
const ethers = require('ethers');
const provider = new ethers.providers.JsonRpcProvider(RPC_URL);

// Monitor factory for new projects
const factory = new ethers.Contract(FACTORY_ADDRESS, FACTORY_ABI, provider);

factory.on("ContractCreated", async (owner, addr, template, event) => {
    // Decode template ID
    const templateId = await factory.getContractTemplateId(addr);

    if (templateId === ethers.utils.id("PROJECT")) {
        console.log(`New project created by ${owner}: ${addr}`);

        // Initialize monitoring for this project
        await monitorProject(addr);
    }
});

async function monitorProject(projectAddr) {
    const project = new ethers.Contract(projectAddr, PROJECT_ABI, provider);

    // Get all components
    const token = await project.token();
    const markets = await project.getMarkets();
    const claims = await project.getClaims();
    const launcher = await project.launcher();

    console.log(`Project components:`, {
        token,
        markets,
        claims,
        launcher
    });

    // Set up monitoring for each component
    monitorMarket(markets[0]);
    monitorLauncher(launcher);
    monitorClaim(claims[0]);
}
```

**Market Sales:**

```javascript
async function monitorMarket(marketAddr) {
    const market = new ethers.Contract(marketAddr, MARKET_ABI, provider);

    market.on("Collected", (buyer, tokenId, price, referrer, event) => {
        console.log(`Sale: NFT #${tokenId} to ${buyer} for ${ethers.utils.formatEther(price)} ETH`);

        // Update analytics
        updateSalesMetrics({
            buyer,
            tokenId: tokenId.toString(),
            price: ethers.utils.formatEther(price),
            referrer,
            timestamp: event.blockNumber
        });
    });

    market.on("Finalized", async (totalRaised, lpAmount, treasuryAmount) => {
        console.log(`Market finalized: ${ethers.utils.formatEther(totalRaised)} ETH raised`);

        // Notify that trading will open soon
        await notifyTradingOpening(marketAddr, totalRaised);
    });
}
```

**Liquidity Launch:**

```javascript
async function monitorLauncher(launcherAddr) {
    const launcher = new ethers.Contract(launcherAddr, LAUNCHER_ABI, provider);

    launcher.on("LiquidityLaunched", async (pair, tokenAmount, ethAmount, lpTokens) => {
        console.log(`Liquidity launched!`);
        console.log(`Pair: ${pair}`);
        console.log(`Tokens: ${ethers.utils.formatEther(tokenAmount)}`);
        console.log(`ETH: ${ethers.utils.formatEther(ethAmount)}`);
        console.log(`LP: ${ethers.utils.formatEther(lpTokens)}`);

        // Enable trading interface
        await enableTrading(pair);

        // Start price tracking
        await trackPairPrice(pair);
    });
}
```

**Claim Activity:**

```javascript
async function monitorClaim(claimAddr) {
    const claim = new ethers.Contract(claimAddr, CLAIM_ABI, provider);

    claim.on("TokensDeposited", (token, amount, event) => {
        console.log(`Rewards deposited: ${ethers.utils.formatEther(amount)} of ${token}`);
    });

    claim.on("TokensClaimed", (claimer, token, amount, tokenIds) => {
        console.log(`${claimer} claimed ${ethers.utils.formatEther(amount)} with NFTs ${tokenIds}`);

        // Update user balances
        updateUserRewards(claimer, token, amount);
    });

    claim.on("LPStaked", (staker, tokenId, amount, lockEndTime) => {
        console.log(`${staker} staked ${ethers.utils.formatEther(amount)} until ${new Date(lockEndTime * 1000)}`);
    });

    claim.on("EarlyExit", (user, tokenId, lpReturned, penalty) => {
        console.log(`${user} exited early, penalty: ${ethers.utils.formatEther(penalty)}`);

        // Track penalty for redistribution
        trackPenalty(user, tokenId, penalty);
    });
}
```

## Testing Strategies

### Unit Testing

Test individual contract functions in isolation:

```solidity
// test/templates/markets/SteppedMarket.t.sol
contract SteppedMarketTest is Test {
    SteppedMarket market;
    address admin = address(1);
    address buyer = address(2);

    function setUp() public {
        // Deploy market
        market = new SteppedMarket();
        market.init(
            project,
            card,
            0.01 ether,  // basePrice
            0.001 ether, // priceIncrement
            10,          // itemsPerPackage
            10,          // numberOfPackages
            100,         // maxSupply
            "ipfs://",   // baseUri
            5000         // launcherAllocation
        );
    }

    function testCollect() public {
        vm.deal(buyer, 1 ether);
        vm.prank(buyer);

        uint256 price = market.getCurrentPrice();
        market.collect{value: price}(address(0));

        assertEq(market.totalSold(), 1);
    }

    function testPriceIncreases() public {
        uint256 initialPrice = market.getCurrentPrice();

        // Buy entire first batch
        for (uint i = 0; i < 10; i++) {
            buyOne();
        }

        uint256 newPrice = market.getCurrentPrice();
        assertGt(newPrice, initialPrice, "Price should increase after batch");
    }
}
```

### Integration Testing

Test cross-contract interactions:

```solidity
// test/integration/ProjectFlow.t.sol
contract ProjectFlowTest is DeployProjectSetup {
    function testCompleteProjectFlow() public {
        // 1. Users purchase NFTs
        uint256 price = market.getCurrentPrice();
        vm.deal(user1, 10 ether);
        vm.prank(user1);
        market.collect{value: price}(address(0));

        // 2. Market reaches success threshold
        buyUntilSuccess();

        // 3. Liquidity launches
        launcher.launch();
        assertTrue(launcher.isLaunched());

        // 4. Users can claim rewards
        vm.prank(user1);
        uint256[] memory tokenIds = new uint256[](1);
        tokenIds[0] = 0;
        patronClaim.claimTokensForNFTs(tokenIds, address(token));

        // 5. Verify user received rewards
        assertGt(token.balanceOf(user1), 0);
    }
}
```

### Fuzz Testing

Test with random inputs to find edge cases:

```solidity
function testFuzz_StakeLP(uint256 amount, uint256 lockDuration) public {
    // Bound inputs to valid ranges
    amount = bound(amount, 1e18, 1000e18);
    lockDuration = bound(lockDuration, 7 days, 4 * 365 days);

    // Setup
    vm.deal(user, amount);
    vm.startPrank(user);
    lpToken.approve(address(vaultClaim), amount);

    // Test staking
    vaultClaim.stakeLP(amount, lockDuration);

    // Verify state
    assertEq(vaultClaim.getStakedAmount(0), amount);
}
```

## Production Deployment Checklist

### Pre-Deployment

- [ ] All tests passing (`forge test`)
- [ ] Gas optimization reviewed (`forge test --gas-report`)
- [ ] Code coverage analyzed (`forge coverage`)
- [ ] Security audit completed
- [ ] Multi-sig configured for admin operations
- [ ] Monitoring infrastructure ready
- [ ] Event indexing configured (subgraph/indexer)
- [ ] Frontend integration tested

### Deployment

```bash
# Deploy to testnet first
forge script script/Deploy.s.sol \
    --rpc-url $BASE_SEPOLIA_RPC \
    --broadcast \
    --verify \
    --private-key $PRIVATE_KEY

# Test on testnet for 1-2 weeks
# - Full user flow testing
# - Load testing
# - Monitor for issues

# Deploy to mainnet with multi-sig
forge script script/Deploy.s.sol \
    --rpc-url $BASE_MAINNET_RPC \
    --broadcast \
    --verify \
    --ledger \
    --sender $MULTISIG_ADDRESS
```

### Post-Deployment

- [ ] Verify all contracts on Etherscan
- [ ] Transfer admin to multi-sig
- [ ] Set up monitoring alerts
- [ ] Initialize analytics tracking
- [ ] Document all addresses
- [ ] Announce deployment to community
- [ ] Enable frontend access
- [ ] Set up incident response plan

## Common Integration Patterns

### Pattern: Progressive Rewards

Gradually increase rewards over time:

```solidity
// Deposit rewards incrementally
for (uint i = 0; i < 12; i++) {
    // Monthly deposits
    uint256 monthlyRewards = totalRewards / 12;
    patronClaim.depositRewards{value: monthlyRewards}();
    wait(30 days);
}
```

### Pattern: Multi-Tier Membership

Different NFT tiers with different weights:

```solidity
// Bronze tier: 100 weight
patronClaim.addCardSet(bronzeCard, 100, 1000);

// Silver tier: 250 weight (2.5x bronze)
patronClaim.addCardSet(silverCard, 250, 500);

// Gold tier: 500 weight (5x bronze)
patronClaim.addCardSet(goldCard, 500, 100);
```

### Pattern: Referral Rewards

Track and reward referrers:

```solidity
// Market automatically tracks referrers
market.collect{value: price}(referrerAddress);

// Referrer receives 0.3% of sale (15% of 2% fee)
// Automatically distributed via EthRewarder
```

## Troubleshooting

### Issue: Transaction Reverts on collect()

**Possible causes:**
- Insufficient ETH sent
- Market sold out
- Paused state

**Debug:**

```solidity
uint256 currentPrice = market.getCurrentPrice();
uint256 totalSold = market.totalSold();
uint256 maxSupply = market.maxSupply();

console.log("Price:", currentPrice);
console.log("Sold:", totalSold);
console.log("Max:", maxSupply);
```

### Issue: Liquidity launch fails

**Possible causes:**
- Market not successful
- Already launched
- Insufficient token balance

**Debug:**

```solidity
bool isSuccessful = market.isSuccessful();
bool isLaunched = launcher.isLaunched();
uint256 tokenBalance = token.balanceOf(address(launcher));

require(isSuccessful, "Market not successful");
require(!isLaunched, "Already launched");
require(tokenBalance > 0, "No tokens for LP");
```

### Issue: Claims not working

**Possible causes:**
- No rewards deposited
- NFT not eligible
- Card set not configured

**Debug:**

```solidity
uint256 claimable = patronClaim.getClaimableAmountForNFT(tokenId, rewardToken);
uint256 cardSetCount = patronClaim.getCardSetCount();
uint256 totalLP = patronClaim.getTotalLPTokens();

console.log("Claimable:", claimable);
console.log("Card sets:", cardSetCount);
console.log("Total LP:", totalLP);
```

## Next Steps

- Review [Contracts Reference](./contracts-reference.md) for detailed function documentation
- Study [Security](./security.md) for security best practices
- Explore [Architecture Overview](./architecture-overview.md) for system design
- Join Discord for developer support

You're now ready to integrate with Opals Protocol and launch your project!
