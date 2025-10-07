# Contracts Reference

Complete technical reference for all core Opals Protocol contracts, including function signatures, events, and usage examples.

## Core Contracts

### OpalsFactory

Central registry and deployment system using EIP-1167 minimal proxies.

**Address:** Varies by network (see deployment documentation)

**Key Functions:**

#### deployContract

Deploy a new contract from a template.

```solidity
function deployContract(
    bytes32 templateId,
    bytes memory initData
) external payable returns (address clone)
```

**Parameters:**
- `templateId`: Template identifier (e.g., `keccak256("PROJECT")`)
- `initData`: Initialization data (ABI-encoded constructor arguments)

**Returns:** Address of the deployed clone

**Example:**

```solidity
bytes memory initData = abi.encode("ProjectName", adminAddress);
address project = factory.deployContract(keccak256("PROJECT"), initData);
```

#### getContractsByTemplateId

Get all contracts deployed from a specific template.

```solidity
function getContractsByTemplateId(bytes32 templateId)
    external view returns (address[] memory)
```

**Parameters:**
- `templateId`: Template identifier

**Returns:** Array of deployed contract addresses

#### addContractTemplate

Add a new template to the factory (operator only).

```solidity
function addContractTemplate(
    bytes32 templateId,
    address contractAddr,
    uint128 minimumFee,
    address feeAddr,
    uint32 integratorFeePct
) external
```

**Events:**

```solidity
event ContractCreated(
    address indexed owner,
    address indexed addr,
    address contractTemplate
);

event ContractTemplateAdded(
    address newContract,
    bytes32 templateId
);
```

---

### Project

Central coordination hub managing relationships between all project components.

**Template ID:** `keccak256("PROJECT")`

**Key Functions:**

#### addMarket

Add a market to the project and optionally link to a card.

```solidity
function addMarket(address _market, address _card) public
```

**Access:** Operator or Admin only

**Parameters:**
- `_market`: Market contract address
- `_card`: Optional card to link (use `address(0)` to skip)

**Example:**

```solidity
IProject(project).addMarket(marketAddress, cardAddress);
```

#### addClaim

Add a claim contract to the project.

```solidity
function addClaim(address _claim, address _card) public
```

**Access:** Operator or Admin only

**Parameters:**
- `_claim`: Claim contract address
- `_card`: Optional card to link

#### batchWireProject

Batch wiring function to reduce gas usage (saves ~500,000 gas).

```solidity
function batchWireProject(
    address patronClaim,
    address vaultClaim,
    address patronCard,
    address vaultCard
) external
```

**Access:** Operator or Admin only

**Gas Savings:** ~500,000 gas (17% reduction vs. individual calls)

#### getClaims

Get all claim addresses for this project.

```solidity
function getClaims() external view returns (address[] memory)
```

**Returns:** Array of claim contract addresses

#### getMarkets

Get all market addresses for this project.

```solidity
function getMarkets() external view returns (address[] memory)
```

**Returns:** Array of market contract addresses

#### transferTokens

Transfer tokens from the project to a specified address.

```solidity
function transferTokens(
    address _token,
    address _to,
    uint256 _amount
) external
```

**Access:** Admin only

**Events:**

```solidity
event MarketAdded(address indexed market);
event ClaimAdded(address indexed claim);
event CardAdded(address indexed card);
event ProjectWired(
    address patronClaim,
    address vaultClaim,
    address patronCard,
    address vaultCard,
    uint256 timestamp
);
event TokenSet(address indexed token);
event LauncherSet(address indexed launcher);
event DistributorSet(address indexed distributor);
```

---

### Token

ERC20 token with minting capabilities and 1e27 initial supply.

**Template ID:** `keccak256("TOKEN")`

**Key Functions:**

#### mint

Mint new tokens to a specified address.

```solidity
function mint(address to, uint256 amount) external
```

**Access:** MINTER_ROLE or DEFAULT_ADMIN_ROLE

**Parameters:**
- `to`: Recipient address
- `amount`: Amount to mint (in wei, 18 decimals)

**Example:**

```solidity
IToken(token).mint(recipientAddress, 1000 * 1e18); // Mint 1000 tokens
```

**Standard ERC20 Functions:**

```solidity
function transfer(address to, uint256 amount) external returns (bool);
function approve(address spender, uint256 amount) external returns (bool);
function transferFrom(address from, address to, uint256 amount) external returns (bool);
function balanceOf(address account) external view returns (uint256);
function totalSupply() external view returns (uint256);
```

---

### Operator

Role-based access control for project operations.

**Template ID:** `keccak256("OPERATOR")`

**Roles:**
- **Admin**: Full control (equivalent to project owner)
- **Operator**: Can manage markets, claims, and cards
- **Moderator**: Can approve/reject membership requests

**Key Functions:**

#### isAdmin

Check if an address has admin role.

```solidity
function isAdmin(address account) external view returns (bool)
```

#### isOperator

Check if an address has operator role.

```solidity
function isOperator(address account) external view returns (bool)
```

#### addOperator

Grant operator role to an address.

```solidity
function addOperator(address account) external
```

**Access:** Project or Admin only

#### removeOperator

Revoke operator role from an address.

```solidity
function removeOperator(address account) external
```

**Access:** Project or Admin only

**Events:**

```solidity
event OperatorRoleGranted(address indexed account);
event OperatorRoleRemoved(address indexed account);
event ModeratorRoleGranted(address indexed account);
event ModeratorRoleRemoved(address indexed account);
event AdminRoleGranted(address indexed account);
event AdminRoleRemoved(address indexed account);
```

---

## Market Contracts

### SteppedMarket

Batch-based NFT sales with increasing prices for bot resistance.

**Template ID:** `keccak256("STEPPED_MARKET")`

**Key Functions:**

#### collect

Purchase an NFT with optional referrer.

```solidity
function collect(address referrer) external payable nonReentrant
```

**Parameters:**
- `referrer`: Optional referrer address (use `address(0)` if none)

**Payment:** ETH sent with transaction must equal or exceed current price

**Example:**

```solidity
uint256 price = market.getCurrentPrice();
market.collect{value: price}(referrerAddress);
```

#### getCurrentPrice

Get the current price for the next NFT.

```solidity
function getCurrentPrice() public view returns (uint256)
```

**Returns:** Price in wei

**Formula:** `basePrice + (priceIncrement × currentPackageId)`

#### getCurrentPackageId

Get the current package (batch) ID.

```solidity
function getCurrentPackageId() public view returns (uint256)
```

**Returns:** Package ID (0-indexed)

**Formula:** `totalSold / itemsPerPackage`

#### emergencyBurn

Burn an NFT and receive 70% refund before trading opens.

```solidity
function emergencyBurn(uint256 tokenId) external nonReentrant
```

**Access:** NFT owner only

**Conditions:**
- Trading not yet open (before liquidity launch)
- Refund is 70% of purchase price

**Events:**

```solidity
event Collected(
    address indexed buyer,
    uint256 indexed tokenId,
    uint256 price,
    address referrer
);

event EmergencyBurned(
    address indexed owner,
    uint256 indexed tokenId,
    uint256 refundAmount
);

event Finalized(
    uint256 totalRaised,
    uint256 lpAmount,
    uint256 treasuryAmount
);
```

---

### FixedMarket

Fixed-price NFT sales for simple membership models.

**Template ID:** `keccak256("FIXED_MARKET")`

**Key Functions:**

#### collect

Purchase a fixed-price membership NFT.

```solidity
function collect(address referrer) external payable nonReentrant
```

**Parameters:**
- `referrer`: Optional referrer address

**Payment:** ETH sent must equal fixed price

---

### MembersMarket

Membership market with approval workflow and group management.

**Template ID:** `keccak256("MEMBERS_MARKET")`

**Key Functions:**

#### requestToJoin

Request to join the membership market with prepayment.

```solidity
function requestToJoin() external payable nonReentrant
```

**Payment:** Full membership cost (price + fees)

#### approveRequest

Approve a membership request and mint NFT.

```solidity
function approveRequest(address user) external nonReentrant
```

**Access:** Operator or Moderator only

#### rejectRequest

Reject a membership request and issue refund.

```solidity
function rejectRequest(address user) external nonReentrant
```

**Access:** Operator or Moderator only

#### inviteMember

Allow a member to invite a new person with potential discount.

```solidity
function inviteMember(address invitee) external
```

**Access:** Existing members only

**Events:**

```solidity
event MembershipRequested(address indexed user, uint256 amount);
event MembershipApproved(address indexed user, uint256 tokenId);
event MembershipRejected(address indexed user, uint256 refundAmount);
event MemberInvited(address indexed inviter, address indexed invitee);
```

---

## Claim Contracts

### PatronClaim

Permanent lock claim with 10x multiplier for early supporters.

**Template ID:** `keccak256("PATRON_CLAIM")`

**Key Functions:**

#### addCardSet

Add a card set with per-card weight and max supply.

```solidity
function addCardSet(
    address card,
    uint256 weightPerCard,
    uint256 maxSupply
) external
```

**Access:** Project operator only

**Parameters:**
- `card`: Card contract address
- `weightPerCard`: Weight allocated per card
- `maxSupply`: Maximum supply for this card set

**Example:**

```solidity
IPatronClaim(patronClaim).addCardSet(
    patronCardAddress,
    1000,  // 1000 weight per card
    500    // Max 500 cards
);
```

#### claimTokensForNFTs

Claim protocol fees for specific NFT token IDs.

```solidity
function claimTokensForNFTs(
    uint256[] calldata tokenIds,
    address token
) external nonReentrant
```

**Parameters:**
- `tokenIds`: Array of NFT token IDs to claim for
- `token`: Token address to claim (use WETH for ETH rewards)

**Returns:** Tokens transferred to caller

**Example:**

```solidity
uint256[] memory myTokenIds = new uint256[](2);
myTokenIds[0] = 1;
myTokenIds[1] = 5;

IPatronClaim(patronClaim).claimTokensForNFTs(myTokenIds, wethAddress);
```

#### getClaimableAmountForNFTs

Calculate claimable amount for specific NFT token IDs.

```solidity
function getClaimableAmountForNFTs(
    uint256[] calldata tokenIds,
    address token
) external view returns (uint256)
```

**Returns:** Amount claimable in wei

#### getPatronPower

Get PatronPower for a specific NFT (LP amount × 10x).

```solidity
function getPatronPower(uint256 tokenId)
    external view returns (uint256)
```

**Returns:** PatronPower value

**Formula:** `lpAmount × 10`

#### depositRewards

Deposit protocol fees to be distributed to patron card holders.

```solidity
function depositRewards() external payable nonReentrant
```

**Payment:** ETH to deposit

**Access:** Permissionless (anyone can deposit)

**Events:**

```solidity
event CardSetAdded(
    address indexed card,
    uint256 weightPerCard,
    uint256 maxSupply,
    uint256 index
);

event TokensDeposited(
    address indexed token,
    uint256 amount
);

event TokensClaimed(
    address indexed claimer,
    address indexed token,
    uint256 amount,
    uint256[] tokenIds
);
```

---

### VaultClaim

Flexible staking with time-based multipliers (0-5x) and OVL early exit.

**Template ID:** `keccak256("VAULT_CLAIM")`

**Key Functions:**

#### stakeLP

Stake LP tokens with a specified lock duration.

```solidity
function stakeLP(
    uint256 amount,
    uint256 lockDuration
) external nonReentrant returns (uint256 tokenId)
```

**Parameters:**
- `amount`: LP token amount to stake
- `lockDuration`: Lock duration in seconds (7 days to 4 years, or max uint256 for permanent)

**Returns:** NFT token ID representing the stake

**Example:**

```solidity
// Approve LP tokens first
IERC20(lpToken).approve(address(vaultClaim), amount);

// Stake for 1 year (1.25x multiplier)
uint256 tokenId = IVaultClaim(vaultClaim).stakeLP(
    1000 * 1e18,
    365 days
);
```

#### unstakeLP

Unstake LP tokens after lock expiration.

```solidity
function unstakeLP(uint256 tokenId) external nonReentrant
```

**Parameters:**
- `tokenId`: NFT token ID to unstake

**Conditions:**
- Lock period must have expired
- Burns NFT and returns LP tokens
- Grants 20% diamond hands bonus

#### earlyExit

Exit early with penalty before lock expires (OVL).

```solidity
function earlyExit(uint256 tokenId) external nonReentrant
```

**Parameters:**
- `tokenId`: NFT token ID to exit

**Penalty:** 0-50% based on remaining time

**Formula:** `penalty = lpAmount × (remainingTime / totalDuration) × 50%`

**Example:**

```solidity
// Exit early (penalty applies)
IVaultClaim(vaultClaim).earlyExit(tokenId);

// Penalty redistributed to remaining stakers
// User receives reduced LP amount
```

#### getPatronPower

Get PatronPower for a staked position.

```solidity
function getPatronPower(uint256 tokenId)
    external view returns (uint256)
```

**Returns:** PatronPower value

**Formula:**
- Permanent: `lpAmount × 10`
- Time-based: `lpAmount × min(5, lockDuration / 4years × 5)`

#### claimTokensForNFTs

Claim protocol fees for staked positions.

```solidity
function claimTokensForNFTs(
    uint256[] calldata tokenIds,
    address token
) external nonReentrant
```

**Parameters:**
- `tokenIds`: Array of NFT token IDs
- `token`: Token to claim

**Events:**

```solidity
event LPStaked(
    address indexed staker,
    uint256 indexed tokenId,
    uint256 amount,
    uint256 lockEndTime
);

event LPUnstaked(
    address indexed staker,
    uint256 indexed tokenId,
    uint256 amount,
    uint256 bonus
);

event EarlyExit(
    address indexed user,
    uint256 indexed tokenId,
    uint256 lpReturned,
    uint256 penalty
);

event PenaltyRedistributed(
    uint256 indexed tokenId,
    uint256 penaltyAmount,
    uint256 totalPowerBefore
);
```

---

### DiamondClaim

Vesting claim with penalty redistribution for early redemption.

**Template ID:** `keccak256("DIAMOND_CLAIM")`

**Key Functions:**

#### redeem

Claim tokens for one or multiple NFT token IDs.

```solidity
function redeem(uint256[] calldata tokenIds) external nonReentrant
```

**Parameters:**
- `tokenIds`: Array of NFT token IDs to redeem

**Behavior:**
- Before vesting: No tokens available
- During vesting: Partial tokens with penalty for early claim
- After vesting: Full tokens with no penalty

---

## Launcher Contracts

### LiquidityLauncher

Accumulates tokens and launches Uniswap V2 liquidity pool.

**Template ID:** `keccak256("LIQUIDITY_LAUNCHER")`

**Key Functions:**

#### launch

Launch the liquidity pool by creating Uniswap V2 pair.

```solidity
function launch() external nonReentrant
```

**Access:** Permissionless (anyone can trigger after market success)

**Actions:**
1. Creates Uniswap V2 pair (Token/WETH)
2. Adds liquidity with 2% slippage protection
3. Transfers LP tokens to PatronClaim
4. Permanently locks liquidity

**Example:**

```solidity
// After market reaches success threshold
ILauncher(launcher).launch();

// Trading is now open on Uniswap
address pair = ILauncher(launcher).pair();
```

#### isLaunched

Returns whether the launcher has been launched.

```solidity
function isLaunched() external view returns (bool)
```

**Returns:** True if liquidity has been launched

**Events:**

```solidity
event LiquidityLaunched(
    address indexed pair,
    uint256 tokenAmount,
    uint256 ethAmount,
    uint256 lpTokens
);

event LPTokensTransferred(
    address indexed recipient,
    uint256 amount
);
```

---

## Vault Contracts

### WorkLock

ETH staking with Aave V3 yield generation converted to LP.

**Template ID:** `keccak256("WORKLOCK")`

**Key Functions:**

#### stake

Stake ETH and receive a Card NFT.

```solidity
function stake() external payable nonReentrant returns (uint256 tokenId)
```

**Payment:** ETH to stake

**Returns:** NFT token ID representing stake

**Actions:**
1. Wraps ETH to WETH
2. Deposits WETH to Aave V3
3. Receives aWETH (interest-bearing)
4. Mints Card NFT to user

**Example:**

```solidity
uint256 tokenId = IWorklock(worklock).stake{value: 10 ether}();
```

#### unstake

Unstake ETH by burning Card NFT.

```solidity
function unstake(uint256 tokenId) external nonReentrant
```

**Parameters:**
- `tokenId`: Card NFT to burn

**Returns:** Original ETH + any unclaimed interest

#### zapInterest

Zap interest to LP tokens (permissionless).

```solidity
function zapInterest(uint256 tokenId) external nonReentrant
```

**Parameters:**
- `tokenId`: Card NFT to zap interest for

**Access:** Permissionless (anyone can trigger)

**Actions:**
1. Claims Aave interest
2. Takes 30% treasury fee
3. Converts 70% to LP (50% swap to token, add liquidity)
4. Sends LP to VaultClaim with permanent lock (10x multiplier)

**Events:**

```solidity
event CardMinted(
    address indexed staker,
    uint256 indexed tokenId,
    uint256 amount
);

event CardBurned(
    address indexed staker,
    uint256 indexed tokenId,
    uint256 ethReturned
);

event InterestZappedForNFT(
    uint256 indexed tokenId,
    uint256 interestAmount,
    uint256 lpAmount,
    uint256 treasuryFee
);
```

---

## Distribution Contracts

### Distributor

Pro-rata protocol fee distribution based on PatronPower.

**Template ID:** `keccak256("DISTRIBUTOR")`

**Key Functions:**

#### distribute

Distribute available ETH or ERC20 tokens (permissionless).

```solidity
function distribute(address token) external nonReentrant
```

**Parameters:**
- `token`: Token to distribute (use WETH for ETH)

**Access:** Permissionless

**Algorithm:**
1. Query PatronPower from PatronClaim and VaultClaim
2. Calculate total PatronPower
3. Distribute pro-rata based on power percentages
4. Transfer to claim contracts

**Example:**

```solidity
// Anyone can trigger distribution
IDistributor(distributor).distribute(wethAddress);

// Fees distributed to PatronClaim and VaultClaim
// Users claim individually from their claim contract
```

#### quoteShares

Quote the shares that would be distributed.

```solidity
function quoteShares(address token, uint256 amount)
    external view returns (uint256 patronShare, uint256 vaultShare)
```

**Parameters:**
- `token`: Token to quote
- `amount`: Amount to distribute

**Returns:**
- `patronShare`: Amount to PatronClaim
- `vaultShare`: Amount to VaultClaim

**Events:**

```solidity
event Distribution(
    address indexed token,
    uint256 patronAmount,
    uint256 vaultAmount,
    uint256 totalAmount
);

event TokenDistribution(
    address indexed token,
    uint256 patronAmount,
    uint256 vaultAmount
);
```

---

### EthRewarder

Permissionless donation model for protocol fee distribution.

**Key Functions:**

#### deposit

Deposit ETH to a recipient's balance.

```solidity
function deposit(address recipient, string calldata reason)
    external payable
```

**Parameters:**
- `recipient`: Address to receive ETH
- `reason`: Human-readable reason for deposit

**Access:** Permissionless

#### withdraw

Withdraw ETH balance.

```solidity
function withdraw(address to) external nonReentrant
```

**Parameters:**
- `to`: Address to receive withdrawn ETH

**Access:** Anyone can withdraw their own balance

**Events:**

```solidity
event Deposit(
    address indexed from,
    address indexed to,
    uint256 amount,
    string reason
);

event Withdraw(
    address indexed from,
    address indexed to,
    uint256 amount
);
```

---

## Usage Examples

### Complete Project Deployment

```solidity
// Deploy using OpalsRecipe
OpalsRecipe.ProjectCreationArgs memory args = OpalsRecipe.ProjectCreationArgs({
    owner: msg.sender,
    projectName: "MyProject",
    tokenName: "MyToken",
    tokenSymbol: "MYT",
    tokenInitialSupply: 1e27,
    launcherWethReserve: 0,
    launcherTokenReserve: 1e26,
    launcherTokenPriceInWei: 0,
    launcherTrigger: address(0),
    launcherTarget: 10 ether,
    patronCardImageURI: "ipfs://...",
    patronCardDescriptorURI: "",
    patronCardBaseURI: "ipfs://...",
    vaultCardImageURI: "ipfs://...",
    vaultCardDescriptorURI: "",
    vaultCardBaseURI: "ipfs://..."
});

OpalsRecipe.ProjectCreationResult memory result = recipe.createProject(args);
```

### User Flow: Purchase → Stake → Claim

```solidity
// 1. User purchases NFT
uint256 price = market.getCurrentPrice();
market.collect{value: price}(referrer);

// 2. Market succeeds, liquidity launches
launcher.launch();

// 3. User stakes LP tokens
lpToken.approve(address(vaultClaim), amount);
uint256 tokenId = vaultClaim.stakeLP(amount, 365 days);

// 4. Protocol fees accumulate
distributor.distribute(wethAddress);

// 5. User claims rewards
uint256[] memory tokenIds = new uint256[](1);
tokenIds[0] = tokenId;
vaultClaim.claimTokensForNFTs(tokenIds, wethAddress);
```

### Monitoring Project Health

```solidity
// Check market progress
uint256 sold = market.totalSold();
uint256 maxSupply = market.maxSupply();
bool successful = market.isSuccessful();

// Check liquidity status
bool launched = launcher.isLaunched();
address pair = launcher.pair();

// Check claim statistics
uint256 totalPatronPower = patronClaim.totalPatronPower();
uint256 totalVaultPower = vaultClaim.totalPatronPower();

// Check pending rewards
uint256 claimable = patronClaim.getClaimableAmountForNFT(tokenId, token);
```

---

## Next Steps

- Review [Architecture Overview](./architecture-overview.md) for system design
- Study [Integration Guide](./integration-guide.md) for deployment patterns
- Check [Security](./security.md) for best practices
- Explore test suite in `/test` for more examples

For support, join our [Discord](https://discord.gg/opals) or visit [opals.io](https://opals.io).
