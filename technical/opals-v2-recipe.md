# OpalsRecipe: Project Creation Contract

`OpalsRecipe` is a factory wrapper that deploys and wires nine interconnected contracts atomically. The `createProject` function handles deployment, initialization, and cross-contract wiring in a single transaction.

## Contract Deployments

The recipe clones these templates from `OpalsFactory`:

1. **Project** - Coordination hub with bidirectional mappings
2. **Token** - ERC20 with fixed supply (1e27)
3. **Operator** - Role-based access control
4. **LiquidityLauncher** - OpalSwap liquidity deployment
5. **PresaleCard** - ERC721 for ownership
6. **VaultCard** - ERC721 for LP staking
7. **PatronClaim** - Permanent LP allocation (10x PatronPower)
8. **VaultClaim** - Flexible LP staking (1.024x-10x multipliers)
9. **Distributor** - Fee distribution to claims

## ProjectCreationArgs

```solidity
struct ProjectCreationArgs {
    address owner;                    // Project owner address
    string projectName;               // Project display name
    string tokenName;                 // ERC20 token name
    string tokenSymbol;               // ERC20 token symbol
    string projectImageURI;           // Project metadata URI
    string projectDescriptorURI;      // Project descriptor URI
    uint256 tokenInitialSupply;       // Total token supply (1e27 default)
    uint256 launcherWethReserve;      // Initial WETH for LP
    uint256 launcherTokenReserve;     // Initial tokens for LP
    uint256 launcherTokenPriceInWei;  // Token price in wei
    address launcherTrigger;          // Address authorized to trigger launch
    uint256 launcherTarget;           // ETH threshold for auto-launch
    string patronCardImageURI;        // Patron card metadata
    string patronCardDescriptorURI;   // Patron card descriptor
    string patronCardBaseURI;         // Patron card base URI
    string vaultCardImageURI;         // Vault card metadata
    string vaultCardDescriptorURI;    // Vault card descriptor
    string vaultCardBaseURI;          // Vault card base URI
}
```

## Deployment Flow

### Phase 1: Deploy Core Components

```solidity
_deployCoreComponents(args)
```

Clones and partially initializes:
- **Project** (deployed but initialized later)
- **Token** (initialized with 1e27 supply minted to recipe)
- **LiquidityLauncher** (deployed but initialized later)
- **Operator** (initialized with project and owner)

### Phase 2: Deploy Cards and Claims

```solidity
_deployAndInitCardsAndClaims(args, result)
```

1. Clone PatronCard, VaultCard, PatronClaim, VaultClaim templates
2. Initialize cards with naming convention: `{tokenName} Patron Card` / `{tokenSymbol}_PC`
3. Initialize PatronClaim with initial card set (patronCard address)
4. **Now** initialize Launcher with PatronClaim as `lpRecipient`
5. Initialize VaultClaim with VaultCard as minter
6. Clone and initialize Distributor with claim addresses
7. **Now** initialize Project with Distributor address
8. Grant operator permissions to claims
9. Add patronCard to PatronClaim with weight-based allocation (100 weight/card, 1000 max)

### Phase 3: Wire Components

```solidity
IProject(result.project).batchWireProject(
    result.patronClaim,
    result.vaultClaim,
    result.patronCard,
    result.vaultCard
)
```

Establishes bidirectional mappings in Project hub:
- Claim ↔ Card relationships
- Component registry

### Phase 4: Transfer Tokens

```solidity
IERC20(result.token).safeTransfer(result.launcher, LIQUIDITY_SUPPLY);  // 1e26
IERC20(result.token).safeTransfer(result.project, TOKEN_SUPPLY - LIQUIDITY_SUPPLY);  // 9e26
```

- Launcher receives 20% (1e26 tokens) for liquidity
- Project receives 80% (9e26 tokens) for distribution

## Initialization Dependencies

Order matters due to circular dependencies:

1. Token and Operator initialize first (no dependencies)
2. PatronClaim needs to exist before Launcher initializes
3. Distributor needs PatronClaim and VaultClaim addresses
4. Project needs Distributor address for initialization

## Constants

```solidity
uint256 TOKEN_SUPPLY = 1e27;        // 1 billion with 18 decimals
uint256 LIQUIDITY_SUPPLY = 1e26;    // 100 million (10% of supply)
uint256 MAX_TOKEN_SUPPLY = 1e30;    // Maximum to prevent overflow
```

## Return Value

```solidity
struct ProjectCreationResult {
    address project;       // Project coordination hub
    address token;         // ERC20 token
    address launcher;      // Liquidity launcher
    address distributor;   // Fee distributor
    address operator;      // Access control
    address patronClaim;   // Permanent claim
    address vaultClaim;    // Flexible claim
    address patronCard;    // Patron NFT
    address vaultCard;     // Vault NFT
}
```

## Security Properties

- **Atomic Deployment**: All contracts deploy or none deploy
- **No Partial State**: Transaction reverts on any failure
- **Immutable Masters**: Clones reference audited templates
- **Validation**: Input parameters validated before deployment

## Usage Example

```solidity
ProjectCreationArgs memory args = ProjectCreationArgs({
    owner: msg.sender,
    projectName: "Example Project",
    tokenName: "Example Token",
    tokenSymbol: "TKN",
    projectImageURI: "ipfs://...",
    projectDescriptorURI: "ipfs://...",
    tokenInitialSupply: 1e27,
    launcherWethReserve: 0,
    launcherTokenReserve: 0,
    launcherTokenPriceInWei: 0,
    launcherTrigger: address(this),
    launcherTarget: 100 ether,
    patronCardImageURI: "ipfs://...",
    patronCardDescriptorURI: "ipfs://...",
    patronCardBaseURI: "ipfs://...",
    vaultCardImageURI: "ipfs://...",
    vaultCardDescriptorURI: "ipfs://...",
    vaultCardBaseURI: "ipfs://..."
});

ProjectCreationResult memory result = recipe.createProject(args);
```

All nine contracts deployed, initialized, and wired in one transaction. For automatically uploading images to IPFS, please use the create project wizard at https://opals.io/