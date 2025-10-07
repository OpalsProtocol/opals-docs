# Troubleshooting Guide

Common errors and step-by-step solutions. Find your problem, apply the fix, get back to building.

## Transaction Failures

### "INSUFFICIENT_PAYMENT" Error

**What it means**: Your payment is less than the required amount.

**Why it happens**: Price increased between viewing and purchasing. You sent exact amount without buffer.

**How to fix**:
1. Check current price in the market contract
2. Add 5% buffer to handle price increases
3. Approve the higher amount
4. Submit transaction again

**Prevention**: Always add a small buffer when buying NFTs in stepped markets.

### "SOLD_OUT" Error

**What it means**: All NFTs in this batch or market are sold.

**Why it happens**: Someone else bought the last NFT before your transaction confirmed.

**How to fix**:
1. Check if next batch is available (stepped markets)
2. If completely sold out, buy on secondary market
3. Consider joining waitlist for next card set

**Prevention**: Act quickly on popular launches. Use higher gas prices for faster confirmation.

### "INVALID_PRICE" Error

**What it means**: Amount sent doesn't match the exact price required.

**Why it happens**: Sent wrong ETH amount. Batch price changed. Fee calculation incorrect.

**How to fix**:
1. Read current batch price from contract
2. Calculate: Price × Quantity = Total
3. Send exactly that amount
4. Retry transaction

**Example**: Buying 3 NFTs at 0.1 ETH each requires exactly 0.3 ETH.

### "TRANSFER_FAILED" Error

**What it means**: ETH transfer to treasury or liquidity contract failed.

**Why it happens**: Recipient contract cannot receive ETH. Gas limit too low. Reentrancy issue.

**How to fix**:
1. Increase gas limit by 50%
2. Check recipient contract is valid
3. Wait and retry after a few blocks
4. Contact project admin if persists

**When to escalate**: If error persists after 3 attempts with high gas.

### "REFUND_FAILED" Error

**What it means**: Attempting to refund your ETH failed.

**Why it happens**: Your wallet cannot receive ETH. Contract has insufficient balance. Refund period ended.

**How to fix**:
1. Verify your wallet can receive ETH (some multisigs cannot)
2. Check if launch already occurred (refunds disabled after launch)
3. Use a standard wallet address (not contract)
4. Contact support with transaction hash

**Critical**: If you used a smart contract wallet, refunds may not work. Always use EOAs (externally owned accounts).

## NFT Purchase Problems

### Can't See My NFTs After Purchase

**Possible causes**: Wallet not synced. Wrong network. Transaction still pending.

**Solutions**:
1. Check transaction status on block explorer
2. Verify you're on correct network (Base, Optimism, etc.)
3. Refresh wallet NFT section
4. Import NFT contract manually if needed
5. Wait 2-3 minutes for indexing

**Manual import**: Add contract address + your token ID to wallet's NFT section.

### Bought NFTs But No Rewards Available

**Why this happens**: Rewards haven't accumulated yet. Trading volume too low. Claim period not started.

**Check these**:
1. Has liquidity launched yet? (No launch = no trading = no fees)
2. Check trading volume on Uniswap
3. Verify your PatronPower balance
4. Confirm you own the NFT (not transferred)

**Timeline**: Rewards accumulate gradually. Check daily, claim weekly or monthly.

### NFT Shows Zero Value on OpenSea

**Normal situation**: Value comes from utility, not floor price. Rewards > resale.

**If concerned**:
1. Verify rewards are accumulating (check PatronClaim)
2. Calculate lifetime value: Daily fees × 365 × Years
3. Remember: Holding earns, selling stops earnings

**Example**: 0.01 ETH daily rewards = 3.65 ETH yearly. Better than 0.1 ETH sale price.

## Staking Issues

### "INVALID_LOCK_DURATION" Error

**What it means**: Lock duration outside valid range.

**Valid ranges**:
- Minimum: 7 days (604,800 seconds)
- Maximum: 4 years (126,144,000 seconds)
- Permanent: type(uint256).max

**How to fix**:
1. Convert your desired duration to seconds
2. Ensure it's ≥ 7 days and ≤ 4 years
3. For permanent, use the special constant
4. Resubmit with correct value

**Conversion**: Days × 86,400 = Seconds

### "NOT_TOKEN_OWNER" Error

**What it means**: You don't own the NFT you're trying to stake.

**Why it happens**: Transferred NFT. Wrong wallet connected. Using token ID you don't own.

**How to fix**:
1. Verify you own the token (check on block explorer)
2. Connect correct wallet
3. Double-check token ID
4. If transferred, use new owner's wallet

**Check ownership**: Go to NFT contract, call `ownerOf(tokenId)`.

### "LOCK_NOT_EXPIRED" Error

**What it means**: Trying to unstake before lock period ends.

**Why it happens**: Lock still active. Calculated end time incorrectly. Using wrong timezone.

**How to fix**:
1. Check lock expiration: Current timestamp < End timestamp
2. Calculate: Lock Start + Duration = End
3. Wait until end timestamp passes
4. Or use OVL early exit (if available)

**OVL option**: Exit early with penalty instead of waiting.

### Can't Unstake Even After Lock Expires

**Possible causes**: Wrong function called. Token ID incorrect. Contract paused.

**Solutions**:
1. Call `unstake(tokenId)` not `withdraw()`
2. Verify token ID matches your NFT
3. Check if contract is paused (emergency only)
4. Ensure gas limit is sufficient (200,000+)

**If paused**: Wait for unpause or contact project admin.

## Claim Failures

### "ALREADY_CLAIMED" Error

**What it means**: You already claimed for this NFT.

**Why it happens**: Multiple claim attempts. Claimed in previous transaction. Using wrong token ID.

**How to fix**:
1. Check claim history on block explorer
2. Verify which token IDs are unclaimed
3. Only claim unclaimed tokens
4. Review past transactions for confirmation

**Note**: Each NFT can claim once per distribution period.

### "NO_NFT_HOLDINGS" Error

**What it means**: Your wallet has zero NFTs in this collection.

**Why it happens**: Don't own any Patron Cards. Transferred all NFTs. Wrong wallet connected.

**How to fix**:
1. Verify you own at least one Patron Card
2. Connect wallet that owns NFTs
3. Check if you transferred cards to another address
4. Buy Patron Cards if you don't have any

**Check balance**: Call `balanceOf(yourAddress)` on Card contract.

### "INSUFFICIENT_BALANCE" Error

**What it means**: Claim contract has insufficient tokens to distribute.

**Why it happens**: Distribution not funded yet. Claimed more than available. Calculation error.

**How to fix**:
1. Check contract token balance
2. Verify distribution was deposited
3. Wait for next distribution period
4. Contact project if balance should be higher

**When to worry**: If contract should have balance but shows zero.

### "ZERO_AMOUNT" Error

**What it means**: Your claimable amount is zero.

**Why it happens**: No rewards accumulated. PatronPower too low. Trading volume insufficient.

**How to fix**:
1. Check your PatronPower: Should be > 0
2. Verify trading volume exists
3. Wait for more fees to accumulate
4. Increase your PatronPower (stake more, lock longer)

**Minimum threshold**: Some projects require minimum amount before claiming.

## Configuration Issues

### Wrong Network Connected

**Symptoms**: Contract not found. Transaction fails. Balance shows zero.

**How to identify**:
1. Check wallet shows correct network
2. Verify contract exists on current network
3. Look for "Network Mismatch" warnings

**How to fix**:
1. Open wallet network selector
2. Switch to correct network (Base, Optimism, etc.)
3. Refresh page
4. Reconnect wallet
5. Retry transaction

**Common networks**: Ethereum (1), Base (8453), Optimism (10), Arbitrum (42161)

### Can't Approve Token Spending

**What it means**: ERC20 approval transaction failing.

**Common causes**: Insufficient gas. Already approved. Token contract paused.

**Solutions**:
1. Check current allowance: May already be approved
2. Revoke old approval first: Set to 0, then new amount
3. Use unlimited approval: type(uint256).max
4. Increase gas limit to 100,000
5. Check token is not paused

**Security tip**: Only approve amounts you plan to use immediately.

### Transaction Pending Forever

**What it means**: Transaction stuck in mempool.

**Why it happens**: Gas price too low. Nonce conflict. Network congestion.

**How to fix**:
1. Check gas price vs. network average
2. Speed up: Resubmit with same nonce, higher gas
3. Cancel: Send 0 ETH to yourself with same nonce
4. Wait: Sometimes takes 30+ minutes during congestion

**Prevention**: Use recommended gas prices. Add 10% buffer during congestion.

## Gas Estimation Problems

### "Out of Gas" Error

**What it means**: Transaction ran out of gas during execution.

**Why it happens**: Underestimated complexity. Loops over large arrays. Reentrancy.

**How to fix**:
1. Increase gas limit by 50%
2. Break operation into smaller batches
3. Remove unlimited approvals and redo
4. Check contract for gas estimates

**Typical limits**:
- Deploy: 5,000,000
- Buy NFT: 300,000
- Claim: 200,000
- Stake: 250,000

### Gas Price Too High

**Not an error**: Just expensive network conditions.

**How to reduce costs**:
1. Use L2s: Base, Optimism, Arbitrum (100x cheaper)
2. Wait for low congestion (nights, weekends)
3. Batch operations: Claim multiple at once
4. Set lower gas price, wait longer

**Cost comparison**:
- Ethereum: $50-200 per transaction
- Base: $0.50-2
- Optimism: $0.30-1.50
- Arbitrum: $0.20-1

### Transaction Underpriced

**What it means**: Gas price below network minimum.

**Why it happens**: Used old gas price. Network congestion increased. EIP-1559 base fee rose.

**How to fix**:
1. Get current base fee from block explorer
2. Use wallet's recommended gas
3. Increase max fee to 2x base fee
4. Retry transaction

**EIP-1559 networks**: Set both maxFeePerGas and maxPriorityFeePerGas.

## Slippage and Price Issues

### "SLIPPAGE_TOO_HIGH" Error

**What it means**: Price moved too much between transaction submission and execution.

**Why it happens**: High volatility. Large trade size. Low liquidity. Front-running.

**How to fix**:
1. Increase slippage tolerance to 3-5%
2. Split large trades into smaller ones
3. Wait for lower volatility
4. Use limit orders if available

**Warning**: High slippage = worse price. Only increase if necessary.

### Price Changed During Purchase

**Normal behavior**: Stepped markets increase price each batch.

**What to expect**:
1. Batch 1-100: 0.1 ETH
2. Batch 101-200: 0.15 ETH
3. Price jumps when batch fills

**How to handle**:
1. Check current batch and price
2. Send enough ETH for next price tier
3. Excess ETH refunded automatically
4. Monitor batch fill levels

**Strategy**: Buy early in batch for best price.

## Smart Contract Specific Errors

### "INVALID_ADDRESS" Error

**What it means**: Provided address is zero address or invalid.

**Common in**: Initialization. Token transfers. Delegation.

**How to fix**:
1. Verify address is not 0x0000...0000
2. Check address is checksummed correctly
3. Ensure address is for correct network
4. Copy-paste to avoid typos

**Validation**: Use Etherscan to verify address exists.

### "ONLY_OPERATOR" Error

**What it means**: Function requires operator role. You don't have it.

**Why it happens**: Trying to call admin functions. Not added as operator. Wrong wallet.

**How to fix**:
1. Verify you have operator role
2. Ask project admin to grant role
3. Use wallet with operator permissions
4. Check if function is public (may not need role)

**Check role**: Call `isOperator(yourAddress)` on Project contract.

### "ONLY_ADMIN" Error

**What it means**: Function requires admin role. Even operators can't call it.

**Critical functions**: Adding operators. Changing core settings. Emergency pause.

**How to fix**:
1. Must be project admin (usually founder)
2. No way to grant admin without existing admin
3. If lost admin access, contract may be locked
4. Use multisig for admin role (recommended)

**Prevention**: Set admin to multisig. Never use hot wallet.

### "CONTRACT_PAUSED" Error

**What it means**: Contract is emergency paused.

**Why it happens**: Security incident. Upgrade in progress. Admin action.

**How to fix**:
1. Wait for unpause announcement
2. Check project Discord/Twitter for updates
3. Don't panic: Funds are safe
4. Contact admin if pause seems wrong

**Timeline**: Usually unpaused within hours. Days maximum for serious issues.

## Common User Mistakes

### Approving Wrong Token

**Problem**: Approved USDC but need to approve WETH.

**How to fix**:
1. Identify required token from error
2. Approve correct token
3. Check transaction requirements before signing

### Using Wrong Wallet

**Problem**: Connected different wallet than one holding NFTs.

**How to fix**:
1. Disconnect current wallet
2. Connect wallet with NFTs/tokens
3. Verify balance before transactions

### Insufficient ETH for Gas

**Problem**: Have tokens but no ETH for gas.

**How to fix**:
1. Send ETH to wallet (0.01-0.1 ETH sufficient)
2. Keep gas reserves on all networks
3. Use faucets for testnets

### Sent to Wrong Address

**Critical**: Cannot reverse blockchain transactions.

**If tokens sent wrong**:
1. Contact recipient if known
2. No protocol-level recovery possible
3. Check if recipient is contract (may have recovery)

**Prevention**: Always verify address. Use address book. Test with small amount first.

## Getting Help

### Before Asking for Support

Collect this information:
1. Transaction hash
2. Wallet address
3. Error message (exact text)
4. Network being used
5. Steps to reproduce

### Where to Get Help

**Community Discord**: Real-time help from community members

**GitHub Issues**: Bug reports and technical problems

**Documentation**: Most questions answered in docs

**Twitter**: Announcements and quick updates

### When to Contact Admin

Contact for:
- Contract paused unexpectedly
- Funds stuck in contract
- Suspected security issue
- Operator access needed

Don't contact for:
- How-to questions (use docs)
- Price questions (check market)
- General support (use Discord)

## Emergency Procedures

### Suspected Security Issue

**Immediate actions**:
1. Stop all transactions
2. Document the issue
3. Contact admin privately (DM, not public)
4. Don't share exploit publicly
5. Wait for response

**Don't**: Post exploit publicly. Continue transacting. Panic sell.

### Lost Access to Wallet

**NFT holdings**:
1. Check seed phrase backups
2. Try hardware wallet recovery
3. Contact wallet provider support

**Admin role**:
1. If multisig: Use other signers
2. If single wallet: May be unrecoverable
3. Prevention: Always use multisig for admin

### Contract Acting Weird

**Investigation steps**:
1. Check recent transactions
2. Review contract events
3. Compare to expected behavior
4. Ask in Discord

**If confirmed bug**:
1. Document clearly
2. Report to admin
3. Await emergency response

## Prevention Best Practices

### Before Every Transaction

1. Verify correct network
2. Check you have gas ETH
3. Review transaction details
4. Start with small test amount
5. Confirm addresses are correct

### Security Checklist

1. Never share private keys
2. Use hardware wallet for large amounts
3. Verify contract addresses
4. Check transaction before signing
5. Keep backups of seed phrases

### Gas Management

1. Keep ETH for gas on all networks
2. Check gas prices before transacting
3. Use L2s for frequent operations
4. Batch claims to save gas

### Smart Defaults

1. Use recommended gas prices
2. Add 5% slippage buffer
3. Verify before every signature
4. Keep emergency contact list
5. Know project admin contacts

---

**Still stuck?** Join the Discord and ask with your transaction hash, wallet address, and error message. The community is here to help.
