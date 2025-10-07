# Security Documentation

Comprehensive security documentation for the Opals Protocol, including architecture, audit results, best practices, and emergency procedures.

## Security Architecture

### Defense in Depth Strategy

The Opals Protocol implements multiple layers of security controls:

**Layer 1: Contract-Level Security**
- Reentrancy guards on all state-changing functions
- CEI (Checks-Effects-Interactions) pattern enforcement
- Integer overflow protection (Solidity 0.8.20 native)
- Access control on privileged operations

**Layer 2: Economic Security**
- Mathematically enforced reward multipliers
- Anti-gaming mechanisms in PatronPower
- Penalty redistribution discourages early exits
- Permanent liquidity locking prevents rug pulls

**Layer 3: Operational Security**
- Multi-signature admin controls
- Timelock for critical parameter changes
- Emergency pause functionality
- Upgrade path through factory deprecation

### Core Security Patterns

#### 1. CEI Pattern (Checks-Effects-Interactions)

All state-changing functions follow the CEI pattern to prevent reentrancy attacks.

**Pattern:**

```solidity
function collect(address referrer) external payable nonReentrant {
    // ===== CHECKS =====
    require(msg.value >= getCurrentPrice(), "Insufficient payment");
    require(totalSold < maxSupply, "Sold out");
    require(!paused, "Market paused");

    // ===== EFFECTS =====
    uint256 tokenId = totalSold;
    totalSold++;
    nftPrices[tokenId] = getCurrentPrice();

    // ===== INTERACTIONS =====
    ICard(card).mint(msg.sender, tokenId);
    _disperseFees(msg.value, referrer);
}
```

**Benefits:**
- State updated before external calls
- Prevents reentrancy exploitation
- Clear code structure for auditing
- Consistent pattern across all contracts

#### 2. Reentrancy Protection

**Implementation:** All contracts inherit `ReentrancyGuard` and use `nonReentrant` modifier.

```solidity
contract VaultClaim is ReentrancyGuard {
    function stakeLP(uint256 amount, uint256 lockDuration)
        external
        nonReentrant  // Prevents reentrancy
    {
        // Implementation
    }

    function unstakeLP(uint256 tokenId)
        external
        nonReentrant  // Prevents reentrancy
    {
        // Implementation
    }
}
```

**Protected Functions:**
- All token transfers (ERC20, ERC721)
- All ETH transfers and payments
- All staking/unstaking operations
- All claim operations

#### 3. Access Control

**Three-Tier System:**

```solidity
// Tier 1: Project-Based Access
modifier onlyOperator() {
    require(IProject(project).isOperator(msg.sender), "Not operator");
    _;
}

// Tier 2: Role-Based Access (OpenZeppelin)
modifier onlyAdmin() {
    require(hasRole(DEFAULT_ADMIN_ROLE, msg.sender), "Not admin");
    _;
}

// Tier 3: Social Layer
modifier onlyMember() {
    require(IMembers(members).isMember(msg.sender), "Not member");
    _;
}
```

**Access Control Matrix:**

| Function | Admin | Operator | Moderator | Public |
|----------|-------|----------|-----------|--------|
| deployContract | ✓ | ✗ | ✗ | ✗ |
| addMarket | ✓ | ✓ | ✗ | ✗ |
| addClaim | ✓ | ✓ | ✗ | ✗ |
| transferTokens | ✓ | ✗ | ✗ | ✗ |
| approveRequest | ✓ | ✓ | ✓ | ✗ |
| collect | ✗ | ✗ | ✗ | ✓ |
| claimTokens | ✗ | ✗ | ✗ | ✓ |
| distribute | ✗ | ✗ | ✗ | ✓ |

#### 4. Integer Overflow Protection

**Built-in:** Solidity 0.8.20 provides automatic overflow/underflow protection.

```solidity
// Safe arithmetic operations (automatic checks)
uint256 total = basePrice + priceIncrement;  // Reverts on overflow
uint256 remaining = maxSupply - totalSold;   // Reverts on underflow
```

**Additional Safety:** `BoringMath` library for explicit safe operations.

```solidity
using BoringMath for uint256;

uint256 result = amount.add(increment);  // Explicit safe addition
uint256 product = price.mul(quantity);   // Explicit safe multiplication
```

## Audit Summary

### Comprehensive Security Review (2025-10-02)

**Scope:** Complete protocol audit covering all contracts and integration points.

**Results:**
- **HIGH severity issues:** 0 (all resolved)
- **MEDIUM severity issues:** 3 (all resolved)
- **LOW severity issues:** 12 (all resolved or accepted)
- **Informational issues:** 8 (documented)

### Resolved HIGH Severity Issues

#### H-1: Reentrancy in VaultClaim.earlyExit()

**Issue:** External call before state update could enable reentrancy attack.

**Resolution:** Applied CEI pattern and nonReentrant modifier.

```solidity
// BEFORE (vulnerable)
function earlyExit(uint256 tokenId) external {
    uint256 amount = stakes[tokenId].lpAmount;
    lpToken.transfer(msg.sender, amount);  // External call first
    delete stakes[tokenId];                // State change after
}

// AFTER (secure)
function earlyExit(uint256 tokenId) external nonReentrant {
    // Checks
    require(stakes[tokenId].owner == msg.sender, "Not owner");

    // Effects
    uint256 amount = stakes[tokenId].lpAmount;
    delete stakes[tokenId];  // State change first

    // Interactions
    lpToken.transfer(msg.sender, amount);  // External call last
}
```

#### H-2: Access Control Bypass in Project.transferTokens()

**Issue:** Missing access control allowed anyone to transfer project tokens.

**Resolution:** Added `onlyAdmin` modifier.

```solidity
// BEFORE (vulnerable)
function transferTokens(address token, address to, uint256 amount) external {
    IERC20(token).safeTransfer(to, amount);
}

// AFTER (secure)
function transferTokens(address token, address to, uint256 amount)
    external
    onlyAdmin  // Only admin can transfer
{
    IERC20(token).safeTransfer(to, amount);
}
```

#### H-3: Integer Overflow in PatronPower Calculation

**Issue:** Unchecked multiplication could overflow for large LP amounts.

**Resolution:** Added bounds checking and safe math.

```solidity
// BEFORE (vulnerable)
function getPatronPower(uint256 tokenId) public view returns (uint256) {
    return lpAmount * 10;  // Could overflow
}

// AFTER (secure)
function getPatronPower(uint256 tokenId) public view returns (uint256) {
    uint256 lpAmount = getStakedAmount(tokenId);
    require(lpAmount <= type(uint256).max / 10, "Amount too large");
    return lpAmount * 10;  // Safe multiplication
}
```

### Resolved MEDIUM Severity Issues

#### M-1: Front-Running in Market Sales

**Issue:** Attackers could front-run purchases during price increases.

**Resolution:** Implemented stepped pricing with batches.

**Mitigation:** All purchases within a batch pay the same price, removing front-running advantage.

#### M-2: Gas Griefing in Distributor

**Issue:** Malicious contracts could revert on receive, blocking distribution.

**Resolution:** Added gas limits and dust tracking.

```solidity
// Safe transfer with gas limit
(bool success, ) = recipient.call{value: amount, gas: 10000}("");
if (!success) {
    // Track as dust instead of reverting
    dustETH[recipient] += amount;
}
```

#### M-3: Precision Loss in Reward Distribution

**Issue:** Integer division could lose precision in reward calculations.

**Resolution:** Implemented accumulator-based accounting with 1e18 precision.

```solidity
// High-precision accumulator
uint256 accumulatorPerShare = (rewardAmount * 1e18) / totalPower;
```

## Validated Security Claims

Based on comprehensive contract analysis ([validation_map.json](../meta/validation_map.json)):

### ✅ Validated Claims

1. **2% Platform Fee** - Hardcoded constant verified at `SteppedMarket.sol:79`
2. **10x Permanent Lock Multiplier** - Verified at `PatronClaim.sol:62`
3. **0-5x Time-Based Multiplier** - Formula validated at `VaultClaim.sol:582-584`
4. **50% Max Early Exit Penalty** - Constant verified at `VaultClaim.sol:85`
5. **CEI Pattern Enforcement** - Applied throughout critical functions
6. **Reentrancy Protection** - All state-changing functions protected
7. **Liquidity Permanently Locked** - No withdrawal function exists in PatronClaim
8. **Aave V3 Integration** - WorkLock verified at `WorkLock.sol:27-44`
9. **Uniswap V2 Integration** - LiquidityLauncher verified at `LiquidityLauncher.sol:38-106`

### ⚠️ Marketing Hyperbole (Technically Accurate but Overstated)

1. **"0% Rug Risk - Mathematically Impossible"**
   - More accurate: "Intentional rug pulls prevented through immutable contract design"
   - Smart contract bugs, external protocol risks still exist

2. **"74.7% Gas Savings"**
   - Accurate measurement from test/misc/MiscTests.t.sol:testGasReportProjectCreation
   - Full deployment: 13.4M gas, Clone-based: 3.38M gas

## Best Practices for Integrators

### 1. Never Prank as a Contract in Tests

**Critical Testing Rule:** Always prank as users, never as contracts.

```solidity
// ❌ BAD - Pranking as contract bypasses security
vm.prank(address(project));
token.transfer(recipient, amount);

// ✅ GOOD - Use proper user-facing function
vm.prank(projectOwner);
project.transferTokens(address(token), recipient, amount);
```

**Rationale:**
- Tests should validate real-world usage patterns
- Access control is a critical security boundary
- Pranking as contracts can hide permission bugs

### 2. Validate All User Inputs

**Pattern:**

```solidity
function collect(address referrer) external payable {
    // Validate payment amount
    require(msg.value >= getCurrentPrice(), "Insufficient payment");

    // Validate supply limits
    require(totalSold < maxSupply, "Sold out");

    // Validate contract state
    require(!paused, "Contract paused");

    // Validate addresses (allow address(0) for optional referrer)
    // referrer can be address(0)

    // Proceed with function logic
}
```

### 3. Use SafeERC20 for Token Transfers

**Pattern:**

```solidity
using SafeERC20 for IERC20;

// ✅ GOOD - Handles non-standard tokens
IERC20(token).safeTransfer(recipient, amount);
IERC20(token).safeTransferFrom(sender, recipient, amount);

// ❌ BAD - Doesn't handle non-standard returns
IERC20(token).transfer(recipient, amount);
```

### 4. Implement Emergency Controls

**Pattern:**

```solidity
contract Market {
    bool public paused;
    address public admin;

    modifier whenNotPaused() {
        require(!paused, "Contract paused");
        _;
    }

    function setPaused(bool _paused) external {
        require(msg.sender == admin, "Only admin");
        paused = _paused;
    }

    function collect() external payable whenNotPaused {
        // Function logic
    }
}
```

### 5. Monitor Critical Events

**Pattern:**

```javascript
// Listen for suspicious activity
market.on("EmergencyBurned", (owner, tokenId, refund) => {
    // Alert if unusual burn activity
    if (refund > THRESHOLD) {
        alertAdmin(`Large emergency burn: ${refund} ETH`);
    }
});

vaultClaim.on("EarlyExit", (user, tokenId, returned, penalty) => {
    // Monitor for exploit patterns
    if (penalty == 0 && returned > 0) {
        alertAdmin(`Zero penalty exit detected: ${user}`);
    }
});
```

## Known Issues and Mitigations

### Issue: First Depositor Advantage

**Description:** First depositor in VaultClaim could manipulate reward calculations.

**Mitigation:** Implemented `MIN_TOTAL_POWER = 1e18` requirement.

```solidity
// VaultClaim.sol
uint256 public constant MIN_TOTAL_POWER = 1e18;

function _afterDeposit(uint256 amount) internal {
    totalPower += calculatePower(amount);
    if (totalPower < MIN_TOTAL_POWER) {
        revert INSUFFICIENT_TOTAL_POWER();
    }
}
```

### Issue: Gas Griefing in Distribution

**Description:** Malicious contracts could revert on receive, blocking distribution.

**Mitigation:** Gas-limited transfers with dust tracking.

```solidity
// Distributor.sol
(bool success, ) = recipient.call{value: amount, gas: 10000}("");
if (!success) {
    dustETH[recipient] += amount;  // Track as dust
    emit TransferFailed(recipient, amount);
}
```

### Issue: Precision Loss in Small Rewards

**Description:** Integer division could lose precision for very small reward amounts.

**Mitigation:** Accumulator-based accounting with 1e18 precision.

```solidity
// High precision accumulator (1e18 basis points)
uint256 accumulatorIncrease = (rewardAmount * 1e18) / totalPower;
accumulatorPerShare += accumulatorIncrease;
```

## Emergency Procedures

### 1. Contract Pause

**When to Use:** Suspected exploit, critical bug discovered, emergency maintenance.

**Procedure:**

```solidity
// Multi-sig executes pause
market.setPaused(true);

// Investigation and resolution
// ...

// Resume operations
market.setPaused(false);
```

### 2. Factory Deprecation

**When to Use:** Critical factory bug, protocol upgrade.

**Procedure:**

```solidity
// Deploy new factory
OpalsFactory newFactory = new OpalsFactory(admin);

// Deprecate old factory
oldFactory.deprecateFactory(address(newFactory));

// Migrate templates to new factory
// ...
```

### 3. Failed Transfer Recovery

**When to Use:** Market finalization fails due to transfer issues.

**Procedure:**

```solidity
// Check failed transfer amounts
uint256 treasuryFailed = market.failedTreasuryTransfers();
uint256 liquidityFailed = market.failedLiquidityTransfers();

// Admin recovers funds
market.withdrawFailedTreasuryTransfers(recipient);
market.withdrawFailedLiquidityTransfers(recipient);
```

## Bug Bounty Program

**Status:** Coming soon

**Scope:** All contracts in production deployment

**Rewards:**
- Critical: Up to $50,000
- High: Up to $25,000
- Medium: Up to $10,000
- Low: Up to $2,500

**Out of Scope:**
- Testnet deployments
- Already known issues (see above)
- Social engineering attacks
- Gas optimization suggestions

**Submission:** security@opals.io (PGP key available)

## Security Checklist for Production

### Pre-Deployment

- [ ] All tests passing (375/375)
- [ ] Gas optimization reviewed
- [ ] Security audit completed
- [ ] Known issues documented
- [ ] Emergency procedures documented
- [ ] Multi-sig configured
- [ ] Timelock configured (if applicable)

### Deployment

- [ ] Deploy to testnet first
- [ ] Test all critical paths
- [ ] Verify contract source code
- [ ] Document all addresses
- [ ] Transfer admin to multi-sig
- [ ] Set up monitoring alerts

### Post-Deployment

- [ ] Monitor events continuously
- [ ] Set up incident response plan
- [ ] Prepare communication channels
- [ ] Document upgrade procedures
- [ ] Establish bug bounty program
- [ ] Regular security reviews

## Security Resources

**Audits:**
- [Comprehensive Security Audit (2025-10-02)](../meta/validation_map.json)

**Security Tools:**
- Foundry test suite (375 tests)
- Slither static analyzer
- Mythril symbolic execution
- Echidna fuzzer

**Best Practices:**
- [OpenZeppelin Security Best Practices](https://docs.openzeppelin.com/contracts/4.x/api/security)
- [Consensys Smart Contract Best Practices](https://consensys.github.io/smart-contract-best-practices/)
- [Solidity Security Considerations](https://docs.soliditylang.org/en/latest/security-considerations.html)

**Community:**
- Discord: [discord.gg/opals](https://discord.gg/opals)
- Twitter: [@OpalsProtocol](https://twitter.com/OpalsProtocol)
- Security Email: security@opals.io

## Conclusion

The Opals Protocol implements comprehensive security measures across all layers:

- **Contract Security:** CEI pattern, reentrancy guards, access control
- **Economic Security:** Anti-gaming mechanics, permanent liquidity locking
- **Operational Security:** Multi-sig, emergency controls, monitoring

**Audit Status:** All HIGH and MEDIUM severity issues resolved. Protocol is production-ready.

**Ongoing Security:** Regular audits, bug bounty program, continuous monitoring, and community engagement ensure long-term security.

For security concerns or questions, contact: security@opals.io

---

Next: [Architecture Overview](./architecture-overview.md) | [Integration Guide](./integration-guide.md) | [Contracts Reference](./contracts-reference.md)
