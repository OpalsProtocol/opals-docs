# Architecture: LP Allocation and Fee Distribution

Technical overview of Opals protocol architecture, component interactions, and capital flows.

## System Components

**Core Contracts:**
- **Market** - Presale contract for Patron Card sales
- **Token** - ERC20 with fixed supply (1e27)
- **Project** - Central coordination hub
- **LiquidityLauncher** - Automated LP creation on threshold
- **PatronClaim** - Permanent LP allocation for presale participants
- **VaultClaim** - Flexible LP staking post-launch
- **WorkLock** - USDC deposits with Aave yield integration
- **Distributor** - Fee collection and distribution engine
- **OpalSwap** - Uniswap V2 fork with 1% trading fees

## Capital Flow Architecture

### Presale Phase

**Market Contract:**
- Receives ETH from Patron Card purchases
- Executes 80/20 split:
  - 80% → Project Treasury (operational runway)
  - 20% → LiquidityLauncher (liquidity creation)

**Token Allocation:**
- Total supply: 1e27 tokens (1 billion with 18 decimals)
- Split at deployment:
  - 80% (8e26) → Project Treasury
  - 20% (2e26) → LiquidityLauncher

### Liquidity Creation

**LiquidityLauncher Execution:**
1. Triggers when ETH threshold reached
2. Pairs 2e26 tokens with accumulated ETH
3. Creates LP position on OpalSwap
4. Sends LP tokens → PatronClaim contract
5. PatronClaim has no withdrawal function (permanent lock)

**LP Allocation:**
- LP tokens allocated to Patron Cards (not burned)
- Card-level accounting: Card #N owns X LP tokens
- NFT transferability: Selling card transfers LP rights
- Secondary market pricing based on LP allocation

### WorkLock Mechanism

**USDC Deposit Flow:**
1. User deposits USDC into WorkLock
2. WorkLock stakes USDC in Aave (receives aUSDC)
3. Principal remains liquid (withdrawable anytime)
4. Interest accumulates over time

**Interest Distribution:**
- Split: 70% LP creation / 30% Project Treasury
- 70% portion processing:
  - 50% swapped for project tokens (buy pressure)
  - Remaining 50% paired with tokens
  - Creates LP position on OpalSwap
  - LP locked in VaultClaim contract

### Post-Launch Staking

**VaultClaim Mechanics:**
- Users provide liquidity on OpalSwap
- Stake LP tokens with chosen duration
- Duration options: 7 days → permanent
- PatronPower multipliers:
  - 7 days: 1.024x
  - 1 year: 1.25x
  - 4 years: 5x
  - Permanent: 10x

**Early Exit:**
- Open Vested Liquidity (OVL) allows exit with penalty
- Penalty formula: `(Remaining Time / Total Duration) × 50%`
- Penalties redistribute to remaining stakers (PatronPower weighted)

## Fee Distribution System

### Distributor Architecture

**Fee Collection:**
- OpalSwap charges 1% on all swaps
- Fees accumulate in Distributor contract
- Distributor tracks total LP across all claim contracts

**Distribution Calculation:**
```
User Share = (User LP Amount / Total System LP) × Accumulated Fees
```

**Key Properties:**
- Distribution weighted by LP amount (NOT token holdings)
- No governance control over distribution
- No admin override capability
- Mathematical precision (18 decimals)

**Claiming:**
- Users claim from respective contracts:
  - PatronClaim: Presale participants
  - VaultClaim: Post-launch stakers
- Permissionless claiming (anytime)
- Gas-efficient accumulator pattern

## Component Connections

**Presale Flow:**
```
User → Market → [80% Treasury / 20% Launcher]
              → Launcher → OpalSwap → LP → PatronClaim
```

**WorkLock Flow:**
```
User → WorkLock → Aave → Interest → [70% LP / 30% Treasury]
                                   → LP → VaultClaim
```

**Fee Flow:**
```
OpalSwap (1% fees) → Distributor → [PatronClaim / VaultClaim]
                                 → Users claim pro-rata
```

**Staking Flow:**
```
User → OpalSwap (add liquidity) → LP tokens
    → VaultClaim (stake) → PatronPower multiplier
```

## Security Model

**Immutability:**
- All contracts deployed without upgrade functions
- No admin keys after deployment
- No governance override mechanisms
- Code guarantees permanent

**Rug Prevention:**
- LP tokens allocated to claim contracts
- Claim contracts lack withdrawal functions
- Missing functionality = mathematical impossibility
- Not time-locked (function doesn't exist in bytecode)

**Economic Alignment:**
- Fee distribution rewards LP ownership
- Zero token inflation (fixed supply)
- Sustainable yield from trading volume
- Honest economics (low volume = low yield)

## LP Accumulation Paths

**Path 1: Presale (PatronClaim)**
- Buy Patron Cards with ETH
- Automatic permanent LP allocation
- 10x PatronPower multiplier
- Tradeable on secondary markets

**Path 2: Post-Launch (VaultClaim)**
- Provide liquidity on OpalSwap
- Stake LP with chosen duration
- 1.024x-10x multiplier (duration-based)
- Exit with penalty or wait for expiration

**Path 3: WorkLock (VaultClaim)**
- Deposit USDC (principal liquid)
- Interest converts to LP automatically
- LP locked in VaultClaim
- Risk-free participation

---

**All paths converge:** Locked LP ownership → Distributor fee sharing → Sustainable yield without inflation.