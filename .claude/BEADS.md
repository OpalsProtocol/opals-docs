# Beads Task Management for Opals CEO Campaigns

## Overview

Opals CEO operations use **Beads** (bd) as the task management system for executing campaigns, content calendars, and strategic initiatives. Beads tracks campaign tasks with dependencies, making it easy to see what's ready to work on and manage complex, multi-week initiatives.

**CRITICAL**: We use Beads instead of markdown for ALL task tracking. Never create TODO.md or TASKS.md files.

## Why Beads Over Markdown?

### Problems with Markdown Task Lists
- ❌ High cognitive load from parsing text files
- ❌ Not queryable - can't find "what's next?" easily
- ❌ No proper dependency tracking
- ❌ Plans bit-rot quickly as they're rarely updated
- ❌ Creates a swamp of half-finished task files

### Beads Advantages
- ✅ Structured SQLite database with fast queries
- ✅ Four dependency types (blocks, related, parent-child, discovered-from)
- ✅ Automatic ready work detection
- ✅ Git-backed JSONL for version control
- ✅ Self-healing from corruption via git history
- ✅ Hierarchical epics with unlimited nesting
- ✅ Full audit trail for forensics

## Quick Reference

### Essential Commands

```bash
# Create campaign tasks
bd create "Write 3-part thread on fair launches" -p 0 -t content
bd create "Reach out to 20 founder influencers" -p 1 -t partnership
bd create "Compile weekly engagement metrics" -p 2 -t analysis

# View tasks
bd list                    # All open tasks
bd list --status closed    # Completed tasks
bd ready                   # Unblocked tasks ready to work on
bd show campaign-1         # View specific task details

# Update task progress
bd update campaign-1 --status in_progress
bd update campaign-1 --assignee me
bd close campaign-1 --reason "Twitter thread published successfully"

# Manage dependencies
bd dep add campaign-2 campaign-1  # Task 2 blocked by task 1
bd dep tree campaign-epic         # View full campaign hierarchy
bd blocked  # Show all blocked issues
```

## Dependency Types

### 1. Blocks
Task B must complete before Task A can start
```bash
bd dep add opals-app-frontend-2 opals-app-frontend-1
# Issue 1 must be completed before issue 2 can proceed
```

### 2. Parent-Child (Epics)
Hierarchical organization of work
```bash
# Create epic
bd create "Implement Token Staking System" -t epic -p 0
# Returns: opals-app-frontend-10

# Create child tasks
bd create "Design staking contract" --parent opals-app-frontend-10
bd create "Implement staking logic" --parent opals-app-frontend-10
bd create "Add staking UI" --parent opals-app-frontend-10
```

### 3. Related
Soft connection between issues
```bash
bd dep add opals-app-frontend-5 opals-app-frontend-6 --type related
# Issues are connected but don't block each other
```

### 4. Discovered-From
Track provenance when finding new work
```bash
# While working on issue 5, discovered need for refactoring
bd create "Refactor presale contract for clarity" --discovered-from opals-app-frontend-5
```

## Workflow Patterns

### Pattern 1: Feature Development

```bash
# 1. Create feature epic
bd create "Implement LP Staking Rewards" -t epic -p 0
# Returns: opals-app-frontend-20

# 2. Break down into tasks
bd create "Design reward calculation formula" --parent opals-app-frontend-20
bd create "Implement Farm contract changes" --parent opals-app-frontend-20
bd create "Add frontend staking interface" --parent opals-app-frontend-20
bd create "Write integration tests" --parent opals-app-frontend-20

# 3. Add dependencies (design must complete before implementation)
bd dep add opals-app-frontend-22 opals-app-frontend-21

# 4. Start work on ready tasks
bd ready  # Shows opals-app-frontend-21 is ready
bd update opals-app-frontend-21 --status in_progress
```

### Pattern 2: Security Audit

```bash
# 1. Create audit epic
bd create "Security Audit: Presale Contract" -t epic -p 0
# Returns: opals-app-frontend-30

# 2. Create audit phases as children
bd create "Phase 1: Reentrancy Analysis" --parent opals-app-frontend-30
bd create "Phase 2: Access Control Review" --parent opals-app-frontend-30
bd create "Phase 3: Mathematical Verification" --parent opals-app-frontend-30
bd create "Phase 4: Integration Security" --parent opals-app-frontend-30

# 3. Create specific checks under each phase
bd create "Check presale() for reentrancy" --parent opals-app-frontend-31
bd create "Check refund() for reentrancy" --parent opals-app-frontend-31
bd create "Check claim() for reentrancy" --parent opals-app-frontend-31

# 4. Track findings as related issues
bd create "FINDING: Reentrancy in refund()" -p 0 -t bug
bd dep add opals-app-frontend-38 opals-app-frontend-35 --type related
```

### Pattern 3: Test-Driven Development

```bash
# 1. Create test suite epic
bd create "TDD: Vesting Mechanism" -t epic
# Returns: opals-app-frontend-40

# 2. Create test cases
bd create "Test: Linear vesting over 7 days" --parent opals-app-frontend-40
bd create "Test: Early claim penalty calculation" --parent opals-app-frontend-40
bd create "Test: Full claim after vesting period" --parent opals-app-frontend-40

# 3. Work through TDD cycle
bd update opals-app-frontend-41 --status in_progress
# Write failing test
# Implement code to pass
bd close opals-app-frontend-41 --reason "Test passing"
```

### Pattern 4: Bug Discovery During Development

```bash
# While working on issue 50
bd update opals-app-frontend-50 --status in_progress

# Discover a bug
bd create "BUG: Integer overflow in reward calculation" -p 0 -t bug --discovered-from opals-app-frontend-50

# Discover needed refactoring
bd create "Refactor: Extract vesting logic to library" -p 2 --discovered-from opals-app-frontend-50

# Continue with original task after filing issues
bd close opals-app-frontend-50
```

## Agent-Specific Instructions

### For Product Manager Agent

When creating PRDs and task breakdowns:
```bash
# Create PRD epic
bd create "PRD: [Feature Name]" -t epic -p 0

# Create main implementation phases as children
bd create "Backend Implementation" --parent [epic-id]
bd create "Frontend Implementation" --parent [epic-id]
bd create "Testing & QA" --parent [epic-id]
bd create "Documentation" --parent [epic-id]

# Add blocking dependencies
bd dep add [frontend-id] [backend-id]  # Backend blocks frontend
bd dep add [testing-id] [frontend-id]  # Frontend blocks testing
```

### For Contract Auditor Agent

When performing audits:
```bash
# Create audit campaign
bd create "Audit: [Contract/System Name]" -t epic -p 0

# Create findings as separate issues
bd create "CRITICAL: [Finding Title]" -p 0 -t bug
bd create "HIGH: [Finding Title]" -p 1 -t bug
bd create "MEDIUM: [Finding Title]" -p 2 -t bug

# Link findings to audit
bd dep add [finding-id] [audit-id] --type related
```

### For Test Automator Agent

When implementing TDD:
```bash
# Create test suite
bd create "Test Suite: [Feature]" -t epic

# Create individual test cases
bd create "Test: [Specific Behavior]" --parent [suite-id] -t test

# Track test status
bd update [test-id] --status in_progress  # Writing test
bd update [test-id] --label "red"         # Test failing
bd update [test-id] --label "green"       # Test passing
bd close [test-id] --reason "Implemented and passing"
```

## Best Practices

### 1. Issue Creation
- Use descriptive titles that explain WHAT needs to be done
- Set appropriate priority (0=highest, 4=lowest)
- Use types: epic, feature, bug, test, task, refactor
- Add labels for categorization

### 2. Dependency Management
- Use "blocks" for hard dependencies (must complete first)
- Use "related" for soft connections (relevant but not blocking)
- Use "parent-child" for hierarchical organization
- Use "discovered-from" to track work provenance

### 3. Status Management
- `open` - Not started
- `in_progress` - Currently working
- `blocked` - Waiting on dependency
- `review` - In review/testing
- `closed` - Completed

### 4. Ready Work Queue
- Always check `bd ready` before starting new work
- This shows unblocked issues ready to tackle
- Prioritize based on priority field

### 5. Discovery During Work
- File new issues immediately when discovered
- Use `--discovered-from` to maintain provenance
- Don't let discovered work interrupt current task
- Finish current task, then reassess priorities

## Git Integration

Beads automatically syncs with git:
- Issues stored in `.beads/opals-app-frontend.jsonl`
- Auto-exports to JSONL after changes (5s debounce)
- Auto-imports from JSONL when newer than DB
- Recoverable from corruption via git history

### Recovery from Corruption

If the database gets corrupted:
```bash
# Remove corrupted database
rm .beads/*.db

# Reimport from JSONL
bd import .beads/opals-app-frontend.jsonl

# Or restore from git history
git checkout HEAD~1 .beads/opals-app-frontend.jsonl
bd import .beads/opals-app-frontend.jsonl
```

## Migration from Markdown Tasks

For any existing markdown task lists:

1. **Archive Old Files**: Move to `/docs/archive/markdown-tasks/`
2. **Convert to Beads**: Create equivalent issues in Beads
3. **Maintain Context**: Use descriptions to capture important context
4. **Link Related Work**: Use dependencies to maintain relationships

Example conversion:
```bash
# Old markdown task:
# - [ ] Implement presale refund mechanism
#   - [ ] Add refund function to contract
#   - [ ] Calculate 20% penalty
#   - [ ] Update frontend UI

# Converted to Beads:
bd create "Implement presale refund mechanism" -t feature -p 1
bd create "Add refund function to contract" --parent opals-app-frontend-1
bd create "Calculate 20% penalty" --parent opals-app-frontend-1
bd create "Update frontend UI" --parent opals-app-frontend-1
bd dep add opals-app-frontend-4 opals-app-frontend-2  # Contract blocks UI
```

## Common Queries

```bash
# What should I work on next?
bd ready

# What's blocking the most work?
bd blocked

# Show my in-progress tasks
bd list --status in_progress

# Show high-priority bugs
bd list --type bug --priority 0

# Show all work for a specific epic
bd dep tree [epic-id]

# Show recently closed issues
bd list --status closed --limit 10

# Get JSON for programmatic use
bd ready --json
```

## Tips for AI Agents

1. **Always use bd commands** - Never create markdown task files
2. **File issues immediately** - When you discover new work, create an issue
3. **Check ready work** - Use `bd ready` to find unblocked tasks
4. **Update status** - Mark issues as in_progress when starting
5. **Close with reason** - Provide context when closing issues
6. **Use dependencies** - Properly link related work
7. **Maintain provenance** - Use discovered-from for found work

## Issue Naming Convention

Issues are automatically named: `opals-app-frontend-[number]`

This prefix is based on the directory name and ensures unique issue IDs across the project.

## Remember

**Beads is THE way we track work in this project. No markdown task lists, no TODO files, just Beads.**

When in doubt, run `bd quickstart` for a refresher on basic commands.