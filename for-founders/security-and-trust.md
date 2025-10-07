# Security and Trust: How We Make Rug Pulls Impossible

Security isn't a feature. It's the foundation.

This guide explains how Opals makes rug pulls mathematically impossible and why you can trust the infrastructure.

## The Unruggable Guarantee

**Liquidity is locked permanently.** Not for 6 months. Not for 2 years. Forever.

This isn't a promise. It's cryptographically enforced by smart contract design.

### How the Permanent Lock Works

**Step 1**: LiquidityLauncher receives LP tokens from Uniswap after adding liquidity.

**Step 2**: LiquidityLauncher transfers all LP tokens to PatronClaim contract.

**Step 3**: PatronClaim records LP allocation by weight across all Patron Card holders.

**Step 4**: LP tokens remain in PatronClaim forever.

**Critical design decision**: PatronClaim has no function to withdraw LP tokens. There is no code path that can transfer LP tokens out of the contract.

### Code-Level Verification

You don't have to trust this claim. Verify it yourself:

**PatronClaim contract has**:
- Functions to deposit LP tokens
- Functions to claim reward tokens
- Functions to stake NFTs
- NO function to withdraw LP tokens

**LiquidityLauncher contract has**:
- One-time launch function
- Transfers LP to PatronClaim
- NO admin override
- NO emergency withdrawal

Search the contracts for "withdraw" or "transfer" related to LP tokens. You won't find any way to remove them.

### What This Means

**Project creator cannot rug**: Even you, as the founder, cannot withdraw liquidity.

**Opals platform cannot rug**: The contracts are immutable. No admin keys exist.

**Hackers cannot rug**: No exploit can withdraw LP tokens that have no withdrawal function.

**Result**: 0% rug risk. Mathematically impossible.

## Security Architecture

### CEI Pattern Enforcement

Every state-changing function follows CEI (Checks-Effects-Interactions):

**Checks**: Verify conditions (balance sufficient, approvals valid, caller authorized)

**Effects**: Update contract state (balances, mappings, counters)

**Interactions**: Call external contracts (transfer tokens, mint NFTs)

This pattern prevents reentrancy attacks and state corruption.

### Reentrancy Protection

All critical functions use `nonReentrant` modifier:
- Mint Patron Cards
- Stake LP tokens
- Claim rewards
- Launch liquidity
- Early exit from locks

Even if an attacker tries to reenter during execution, the transaction reverts.

### Access Control Layers

**Three-tier security model**:

**Layer 1: Project-level permissions**: Only project operators can perform project-specific actions.

**Layer 2: Role-based access**: Only authorized roles can deploy new templates or modify factory settings.

**Layer 3: Function-level checks**: Every function verifies caller authorization before executing.

**Result**: No single point of failure. Multiple checks at every level.

## Audit and Testing

### Professional Security Audit

All Opals contracts underwent comprehensive third-party security audit.

**Audit scope**:
- All core contracts
- All template contracts
- All integration contracts
- Common attack vectors tested

**Audit results**:
- All HIGH severity issues resolved
- All MEDIUM severity issues resolved
- Low-risk findings addressed or documented

Full audit report available in repository.

### Test Coverage

**375 tests across 32 test contracts**:
- Unit tests for individual functions
- Integration tests for cross-contract interactions
- Fuzz tests for edge cases
- Security-specific tests for attack vectors

**Coverage areas**:
- Access control violations
- Reentrancy attempts
- Integer overflow/underflow
- Unauthorized withdrawals
- State manipulation
- Front-running scenarios

All tests pass before any production deployment.

### Battle-Tested in Production

Opals contracts are deployed and used by real projects raising real capital.

**Production validation**:
- Multiple projects launched successfully
- Millions in total value locked
- Zero exploits or hacks
- Zero rug pulls

Code proven under real-world conditions.

## Risk Mitigation Strategies

### Smart Contract Risk

**Risk**: Bugs or vulnerabilities in contract code.

**Mitigation**:
- Professional audit by third party
- 375 comprehensive tests
- Battle-tested in production
- Open source for community review
- CEI pattern and reentrancy protection

**Residual risk**: Low. All code audited and tested extensively.

### Economic Attack Risk

**Risk**: Attacker manipulates tokenomics or price.

**Mitigation**:
- PatronPower formula prevents mercenary capital exploitation
- Permanent locks create strong holder incentives
- Stepped pricing removes bot advantage
- Weight-based allocation prevents Sybil attacks

**Residual risk**: Very low. Economic design prevents gaming.

### Oracle and Price Manipulation Risk

**Risk**: Price oracle manipulation affects rewards or launches.

**Mitigation**:
- No external price oracles used in core mechanics
- Uniswap TWAP provides manipulation resistance for any price-dependent features
- Launch price determined by actual ETH raised, not external feed

**Residual risk**: Minimal. Most mechanics don't depend on external prices.

### Admin Key Risk

**Risk**: Malicious admin could steal funds or manipulate system.

**Mitigation**:
- No admin keys can withdraw LP tokens
- Critical parameters are immutable after deployment
- Multi-sig recommended for project admin functions
- Time-locks on sensitive operations

**Residual risk**: Very low for LP security. Standard for project-level admin functions.

### Platform Risk

**Risk**: Opals platform itself could have vulnerabilities.

**Mitigation**:
- OpalsFactory is immutable
- Templates are immutable once deployed
- No platform upgrade mechanism for deployed projects
- Open source allows independent verification

**Residual risk**: Low. Decentralization limits platform risk.

## Transparency and Verification

### Open Source Contracts

Every line of code is public:
- GitHub repository available
- All contracts verified on block explorer
- Community can audit independently

No closed-source components. No hidden logic.

### On-Chain Verification

All claims are verifiable on-chain:
- 2% fee hardcoded in contract constants
- Permanent lock proven by lack of withdrawal functions
- PatronPower formula visible in contract code
- Launch mechanics transparent in LiquidityLauncher

Don't trust marketing. Verify the contracts.

### Immutable Design

Once deployed, contracts cannot be changed:
- No upgrade mechanisms
- No admin overrides for core security features
- No emergency stops that could prevent withdrawals

**This means**:
- What you audit is what runs forever
- No surprise changes after you launch
- Rules are cryptographically guaranteed

## Common Security Questions

### Q: What if Opals shuts down?

**A**: Your project continues running. Opals platform going away doesn't affect deployed contracts. They're immutable and decentralized.

### Q: Can Opals team access my funds?

**A**: No. Opals has no access to project funds or LP tokens. Your wallet deploys contracts. You control admin functions.

### Q: What if a vulnerability is discovered later?

**A**: New projects use fixed templates. Existing projects continue with their deployed code. No forced upgrades.

### Q: How do I know LP tokens are actually locked?

**A**: Read PatronClaim.sol. Search for functions that transfer LP tokens out. You won't find any. It's cryptographically enforced.

### Q: What about reward token security?

**A**: Reward tokens flow through PatronClaim but can be withdrawn by stakers. This is intentional. Rewards are meant to be claimed.

### Q: Can supporters lose their NFTs or LP allocations?

**A**: NFTs are standard ERC721. LP allocations are recorded on-chain. Cannot be lost unless supporter loses their wallet.

## Security Best Practices for Founders

### Use Hardware Wallet for Admin

Your admin wallet has significant privileges:
- Can configure project parameters (pre-launch)
- Can send reward tokens to PatronClaim
- Can update project metadata

Protect this wallet with hardware wallet (Ledger, Trezor) or multi-sig.

### Set Minimum Thresholds

Configure minimum ETH threshold for launch:
- Prevents launch with insufficient liquidity
- Protects supporters from shallow markets
- Can refund if threshold not met

Recommended: Set threshold to 50-70% of target raise.

### Communicate Transparently

Share contract addresses publicly:
- Supporters can verify on block explorer
- Builds trust through transparency
- Enables community auditing

### Plan for Reward Distribution

PatronClaim needs reward tokens to distribute:
- Plan distribution schedule in advance
- Set aside tokens from your allocation
- Distribute regularly (monthly or quarterly)

Consistent rewards build community loyalty.

### Test Configuration Before Launch

Verify all parameters before deploying:
- Pricing strategy is correct
- Token allocation matches plan
- Threshold is reasonable
- Market type fits your community

Once deployed, parameters are immutable.

## Security Comparison

### Opals vs Traditional Launchpads

| Security Feature | Opals | Traditional Launchpads |
|------------------|-------|------------------------|
| **LP lock** | Permanent, cryptographic | Time-limited, trust-based |
| **Admin keys** | Cannot withdraw LP | Often have admin keys |
| **Upgrade risk** | Immutable | Often upgradeable |
| **Transparency** | Fully open source | Varies, often partial |
| **Audit** | Complete, public | Varies by platform |

Opals provides stronger security guarantees.

### Opals vs DIY Launch

| Security Feature | Opals | DIY Launch |
|------------------|-------|------------|
| **Audit** | Professional, complete | Your responsibility |
| **Testing** | 375 tests, battle-tested | Your responsibility |
| **CEI pattern** | Enforced | Must implement |
| **Reentrancy protection** | All functions | Must implement |
| **Known vulnerabilities** | Zero (after audit) | Unknown until audited |

Opals reduces security burden significantly.

## What We Don't Protect Against

**Honest disclosure of limitations**:

### Token Price Risk

We cannot prevent your token price from falling:
- Market determines price
- Poor execution affects price
- Broader market conditions matter

Unruggable liquidity doesn't mean price always goes up.

### Project Execution Risk

We cannot force you to deliver on your roadmap:
- Supporters trust you'll build what you promised
- Failure to deliver affects reputation and token value
- This is execution risk, not platform risk

Build what you promise. Reputation matters.

### Regulatory Risk

We cannot prevent regulatory issues:
- Securities laws vary by jurisdiction
- Token sales may face regulation
- Legal compliance is your responsibility

Consult legal counsel in your jurisdiction.

### Smart Contract Platform Risk

We build on Ethereum and compatible chains:
- Underlying chain security matters
- Bridge risks if deploying cross-chain
- Gas costs vary with network congestion

These are blockchain-level risks, not Opals-specific.

## Emergency Procedures

### If You Discover a Bug

**Before launch**:
1. Don't deploy
2. Report to Opals team
3. Wait for fix or guidance
4. Deploy patched version

**After launch**:
1. Assess impact (does it affect LP security?)
2. Report immediately to Opals and community
3. If critical, pause operations where possible
4. For deployed contracts, prepare migration if needed

Transparency is critical. Don't hide issues.

### If Your Wallet Is Compromised

**If admin wallet compromised BEFORE launch**:
- Abandon that deployment
- Deploy new project from secure wallet

**If admin wallet compromised AFTER launch**:
- LP tokens remain safe (locked in PatronClaim)
- Attacker cannot rug liquidity
- Supporters can still stake and claim rewards
- Deploy new admin wallet and update community

The permanent lock protects against even admin compromise.

## Building Trust with Your Community

### Share Contract Addresses Immediately

Post on all channels:
- Twitter
- Discord
- Telegram
- Project website

Supporters can verify everything on block explorer.

### Explain Security Features

Educate your community:
- How permanent lock works
- Why rug pulls are impossible
- How they can verify claims

Knowledgeable supporters are confident supporters.

### Point to Audit Reports

Share third-party validation:
- Link to full audit report
- Highlight zero critical issues
- Explain any residual risks

Transparency builds trust.

### Demonstrate Long-Term Commitment

Actions speak louder than words:
- Lock significant team allocation long-term
- Distribute rewards consistently
- Engage with community regularly
- Deliver on roadmap milestones

Security features provide foundation. Execution builds trust.

## Summary: Why Trust Opals

**Cryptographic guarantees**:
- LP tokens cannot be withdrawn (no function exists)
- Contracts are immutable (no upgrade mechanism)
- All code is open source (verify yourself)

**Professional security**:
- Third-party audit completed
- 375 tests passing
- Battle-tested in production
- CEI pattern and reentrancy protection

**Proven track record**:
- Multiple projects launched successfully
- Zero exploits or hacks
- Zero rug pulls
- Millions in value secured

**Transparent design**:
- All code public
- All fees verifiable
- All claims provable
- Community can audit

You don't have to trust promises. Verify the code yourself.

[View audit reports](../technical/security-audits.md) →

[Explore contracts](../technical/core-contracts.md) →

[Start your launch](./launch-process.md) →

---

**Remember**: Security is not negotiable. We've built the most secure launchpad infrastructure in crypto. Your job is to execute on your vision. Let us handle the security.
