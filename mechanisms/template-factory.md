# Template Factory: Deploy for $15 Instead of $1,000

The Template Factory deploys complete project ecosystems in 5 minutes for $15.

## Why The Template Factory Exists

Traditional smart contract deployment is absurdly expensive.

Every project writes similar contracts. Token contract. NFT contract. Staking contract. Liquidity launcher. Each gets deployed separately, paying full gas costs each time.

A typical deployment costs 3-5 million gas. At 50 gwei and $2,000 ETH, that's $300-$500 per contract. Deploy 10 contracts for your project? $3,000-$5,000 in gas alone.

The Template Factory eliminates this waste through pre-deployed templates and lightweight clones.

## The Core Innovation

The Template Factory uses pre-deployed master contracts.

One master Token contract gets deployed once. Every project creates a lightweight clone pointing to that master. The clone contains only project-specific data. All logic lives in the master.

This pattern reduces deployment gas from 3 million to 150 thousand per contract. That's 74.7% savings. Your $300 deployment becomes $76.

The technical term is EIP-1167 minimal proxy pattern. The business term is "photocopying instead of writing by hand."

## How Template Deployment Works

Deployment happens in three steps.

First, recipes call the factory with template specifications. The recipe says "I need a Token contract with these parameters" and passes initialization data.

Second, the factory creates a minimal proxy clone. This tiny contract contains jump instructions to the master template. Deploying these jump instructions costs ~150k gas instead of 3M gas.

Third, the factory initializes the clone with project-specific data. Name, symbol, initial supply, access controls. The clone now behaves exactly like a full contract but costs 95% less.

## Why This Saves Money

Gas costs scale with contract size.

A full ERC20 token contract contains thousands of lines of logic. Deploying all that code costs millions of gas. You're paying to write the same logic to the blockchain repeatedly.

The minimal proxy pattern deploys ~300 bytes of jump logic. Those 300 bytes point to the master template. The EVM executes the master's logic in the context of your clone's storage.

Result: your clone behaves identically to a full deployment but costs 74.7% less because you're not redeploying the logic.

## Why This Is Safer Than Custom Contracts

The Template Factory improves security through battle-tested reuse.

Custom contracts introduce custom bugs. Even audited code can have vulnerabilities. Every unique deployment is a new attack surface.

Template Factory contracts get audited once. Every clone inherits that audit. One security review covers thousands of deployments. Bugs get fixed in the master, protecting all clones.

This creates network effects around security. More deployments mean more testing. More testing means more bug discoveries. More bug discoveries mean better masters. Better masters mean safer new deployments.

## The Photocopy Analogy

Think of the Template Factory as a copy machine for smart contracts.

Writing a document by hand is slow and expensive. You might make mistakes. Each copy requires full rewriting effort.

Photocopying is fast and cheap. One master document. Unlimited perfect copies. Each copy looks identical to the original but costs pennies instead of dollars.

The Template Factory does this for smart contracts. One master. Unlimited clones. Each clone behaves identically but costs $15 instead of $300.

## Gas Savings Calculation

The savings come from comparing full deployment vs. clone deployment.

Full ERC20 deployment: ~2,500,000 gas. Full ERC721 deployment: ~3,000,000 gas. Full staking contract: ~3,500,000 gas. Total for basic project: ~9,000,000 gas.

At 50 gwei and $2,000 ETH: 9M gas × 50 gwei × $2,000 / 1e18 = $900 total.

Clone deployments: ~150,000 gas each. Three clones: 450,000 gas total.

At same gas price: 450k gas × 50 gwei × $2,000 / 1e18 = $45 total.

Savings: $855, or 74.7%.

## The Seven Core Templates

Opals provides seven essential templates covering all project needs.

### Token Template

Standard ERC20 with role-based minting. Fixed supply of 1e27 tokens. Minter role for controlled distribution. Transfer functions without fees built-in.

Every project needs a token. This template provides the minimum viable implementation. No complexity. No weird edge cases. Just a token that works.

### Card Template

Standard ERC721 for membership and patron cards. Batch minting support. Metadata storage. Owner enumeration.

Projects issue cards representing commitment levels. Patron cards for permanent supporters. Vault cards for flexible stakers. This template handles both.

### Project Template

Central coordination hub connecting all project components. Bidirectional mappings between contracts. Operator access control. Component registry.

This acts as the source of truth. Want to know this project's token? Check the Project contract. Want to know this token's project? Check the Project contract. All relationships map through here.

### Operator Template

Role-based access control for project management. Admin role for critical operations. Operator role for daily management. Minter role for token creation.

Not every team member needs full admin access. Operators can manage markets without touching treasury. Minters can distribute tokens without changing parameters. Separation of duties through clear roles.

### Market Templates

Three market types for NFT sales. SteppedMarket for batch-based pricing that increases per batch. FixedMarket for single-price sales. MembersMarket for gated access.

Different projects need different sale mechanics. Launch a huge collection? Use SteppedMarket for bot resistance. Small exclusive drop? Use FixedMarket. Premium tier for existing holders? Use MembersMarket.

### Claim Templates

Three claim types for token distribution. PatronClaim for permanent LP allocation with 10x rewards. VaultClaim for flexible staking with time-weighted rewards. DiamondClaim for vesting with penalty redistribution.

Token distribution is complex. These templates handle all common patterns. Weight-based allocation. Time-locked vesting. Pro-rata distribution. All built-in.

### Launcher Template

Automated liquidity deployment to Uniswap. Accumulates tokens and ETH. Creates LP pair. Adds liquidity. Transfers LP tokens to PatronClaim. All atomic.

Manual liquidity launches fail constantly. Wrong ratios. Slippage issues. Lost funds. The Launcher template makes it foolproof. Set parameters, call launch, done.

## How Templates Enable 5-Minute Launches

Speed comes from pre-configuration and recipes.

Recipes are orchestration contracts that deploy and wire multiple templates atomically. One recipe call deploys your entire project: token, cards, markets, claims, launchers. Everything connected correctly.

Without templates, you deploy each contract manually. Then connect them. Then test. Then fix issues. This takes days or weeks.

With templates and recipes, everything happens in one transaction. Either the entire project deploys successfully or nothing happens. No partial deployments. No manual wiring errors.

Five minutes includes: choosing parameters, calling the recipe, waiting for confirmation. That's it.

## Template Upgrades and Evolution

Templates are immutable after deployment. This is a feature, not a bug.

Immutability ensures deployed projects never change unexpectedly. Your clone points to a specific master address. That master's logic is frozen. No rug risk through malicious upgrades.

New features require new templates. Deploy an improved Token template as TokenV2. Existing projects on TokenV1 continue working. New projects choose between V1 and V2.

This creates version optionality. Projects can migrate to newer templates voluntarily. Or stay on old versions if they prefer stability. No forced upgrades.

## Template Composition

The real power comes from composing multiple templates.

One template is useful. Seven connected templates create complete ecosystems. Token mints to PatronClaim. PatronClaim distributes to card holders. Cards sold through SteppedMarket. Market funds LiquidityLauncher. Launcher creates Uniswap pair.

Each template handles one concern. Token handles ERC20 logic. Market handles sales. Launcher handles liquidity. Clean separation enables reliable composition.

Projects can also add custom contracts alongside templates. Need unique governance logic? Deploy it separately and connect via the Project hub. Templates handle standard parts. Custom code handles unique parts.

## Why This Pattern Enables Sovereignty

Template Factory deployments are fully owned by project creators.

The factory has no admin keys over your deployed contracts. No pause functions. No upgrade controls. Once deployed, your project is yours.

Compare this to hosted platforms. They control the contracts. They can pause your project. They can change parameters. They can take their platform offline.

Template Factory gives you the contracts. You control them through the Operator system. The factory only provides deployment infrastructure. After deployment, it's irrelevant.

This sovereignty is critical for serious projects. You're not renting infrastructure. You're deploying infrastructure you own.

## Template Factory vs. Custom Development

Custom development gives you perfect fit. Template Factory gives you speed and security.

Custom contracts can implement any logic you imagine. Perfect optimization. Exact feature set. No compromises.

But custom contracts take months to build and audit. You need senior developers. You risk bugs. You pay $50,000+ for audits.

Template Factory contracts are ready now. Audited once. Proven through thousands of deployments. You trade perfect customization for immediate availability.

For most projects, this trade makes sense. Standard token logic works fine. Standard NFT logic works fine. Save the custom development budget for your actual unique value proposition.

## Template Verification and Trust

Every template is open source and verifiable.

The master contracts live at known addresses. Anyone can read their code. Anyone can verify their behavior. Anyone can audit them independently.

When you deploy a clone, anyone can verify it points to the correct master. No hidden logic. No obfuscated code. Pure transparency.

This builds trust without requiring trust. Don't trust the Opals team? Verify the templates yourself. Hire your own auditors. Read the source code. The security comes from math, not promises.

## Gas Optimization Details

The 95% savings come from avoiding constructor execution and code storage.

Full contract deployment: compile the contract, execute the constructor, store all bytecode on-chain. Every operation costs gas. Large contracts cost millions.

Minimal proxy deployment: deploy 300 bytes of jump logic, call initialization function. No constructor execution. No code storage. Just storage writes for your specific data.

The proxy bytecode is tiny: load the master address, delegate the call, return the result. That's ~50 opcodes. Deploying 50 opcodes costs ~150k gas.

Initialization writes your project-specific data to storage. Token name, symbol, owner. These are storage writes you'd pay anyway. The savings come purely from not redeploying logic.

## Template Factory Security Model

Security relies on template immutability and clone isolation.

Each template is audited before registration. The audit covers all possible initialization states. Once registered, the template cannot change.

Clones are isolated. One project's clone cannot affect another's. They share logic but have separate storage. This prevents cross-project exploits.

The factory itself is non-upgradable. No admin can change template addresses. No one can inject malicious templates. Registration is one-way and permanent.

This creates a trust-minimized deployment system. Verify the master once, trust the clones forever.

## Common Template Factory Questions

### Can templates be upgraded?

No. Masters are immutable. Deploy new versions as separate templates. Projects choose which version to use.

### What if a template has a bug?

New projects use the fixed version. Old projects can migrate by deploying new clones and transferring state. The bug doesn't auto-propagate.

### Do all projects share the same code?

They share logic but not storage. Each clone has independent state. One project's tokens don't affect another's.

### Can I add custom logic?

Yes, through composition. Deploy templates for standard parts. Deploy custom contracts for unique parts. Connect them via the Project hub.

### Is this pattern tested in production?

Yes. EIP-1167 minimal proxies are used by major protocols including Uniswap V2 and Compound. Billions in TVL rely on this pattern.

## Template Factory Enables Decentralization

The Template Factory pattern aligns with crypto's decentralization ethos.

Hosted platforms are centralized. One company controls everything. They can censor projects. They can change terms. They are single points of failure.

Template Factory is infrastructure, not platform. Deploy your contracts. Control them yourself. No ongoing platform dependency.

If Opals disappears tomorrow, your deployed projects continue working. The contracts live on Ethereum. You hold the admin keys. Pure ownership.

This decentralization is why serious projects choose the Template Factory over hosted solutions.

## MISO Navigation: Understanding Template Factory

**Ingredient**: Pre-audited contract templates deployed via EIP-1167 cloning (74.7% gas savings)

**Recipe**: OpalsRecipe combines multiple templates into one project. Deploy token, market, claims, launcher simultaneously.

**Navigation**:
- Want to deploy your project? → [For-Founders Quick Start](../for-founders/quick-start.md)
- Want cost details? → [For-Founders Pricing](../for-founders/pricing-and-economics.md)
- Want technical details? → [Technical Architecture](../technical/architecture-overview.md)
- Want anti-gaming? → [Anti-Gaming Mechanisms](./anti-gaming-mechanisms.md)
- Want to understand each contract? → [Components](../components/)

## Next Steps

Ready to deploy for $15?

**For Founders**: Use OpalsRecipe. Deploy token, market, claims, launcher in one transaction. Five minutes. Your project lives.

**For Developers**: Integrate Template Factory clones into your tooling. Reduce deployment costs 74.7%. Speed up iteration.

**For Auditors**: Review once. Protect thousands. One master template = infinite secure deployments.

Template Factory is live. Contracts are audited. Start deploying.
