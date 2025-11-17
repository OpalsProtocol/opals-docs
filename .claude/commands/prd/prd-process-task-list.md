---
description: Guidelines for executing tasks from a Product Requirements Document using Beads
---
# PRD Task Execution with Beads

Guidelines for executing tasks from Product Requirements Documents (PRDs) using the Beads issue tracking system for CEO operations, marketing campaigns, and business initiatives.

**IMPORTANT**: We use Beads (bd) for ALL task management. Never create or update markdown task lists.

## Task Execution with Beads

### Finding and Starting Work

```bash
# Find ready tasks (no blockers)
bd ready

# View all tasks for a specific campaign
bd dep tree [campaign-epic-id]

# Start work on a task
bd update [task-id] --status in_progress --assignee me

# Check current work
bd list --status in_progress
```

### Task Implementation Protocol

1. **Find Next Task**: Use `bd ready` to find unblocked work
2. **Claim Task**: Update status to `in_progress`
3. **Execute**: Complete the work as specified
4. **Quality Check**: Verify output meets success criteria
5. **Complete**: Close task with results

### Completion Protocol

**When completing a task:**

1. **Verify Success Criteria Based on Task Type:**

   **Content Tasks:**
   - Content created and reviewed
   - Optimized for platform (Twitter, Medium, etc.)
   - Scheduled or published as planned
   ```bash
   bd close [task-id] --reason "Thread published: 50K impressions in first hour"
   ```

   **Partnership Tasks:**
   - Outreach completed
   - Responses documented
   - Next steps defined
   ```bash
   bd close [task-id] --reason "Reached 20 partners, 5 positive responses, 3 calls scheduled"
   ```

   **Community Tasks:**
   - Event hosted/activity completed
   - Engagement metrics captured
   - Feedback collected
   ```bash
   bd close [task-id] --reason "Twitter Space complete: 150 attendees, 45min, recording saved"
   ```

   **Analytics Tasks:**
   - Data collected and analyzed
   - Reports generated
   - Insights documented
   ```bash
   bd close [task-id] --reason "Week 1 report complete: 250K impressions, 15% engagement rate"
   ```

2. **Handle Incomplete Work:**
   ```bash
   # Create follow-up task for issues
   bd create "ISSUE: Low engagement on thread, needs revision" -t content -p 1
   bd dep add [issue-id] [task-id] --type discovered-from

   # Keep task open if blocked
   bd update [task-id] --status blocked
   ```

3. **Document Outcomes:**
   - Save created content to appropriate folders
   - Update tracking spreadsheets if used
   - Share results with team

## CEO-Specific Task Protocols

### Content Creation Tasks
```bash
# After creating content
# Verify:
# - Hook is compelling (first 3 seconds/words)
# - Aligns with Opals narrative
# - No hype/speculation language
# - Data-backed claims

bd close [task-id] --reason "Fair launch thread created, reviewed, scheduled for 9am PST"
```

### Partnership Development
```bash
# After partner outreach
# Document:
# - Who was contacted
# - Response received (if any)
# - Next steps
# - Value exchange potential

bd close [task-id] --reason "10 DAOs contacted, 3 interested in collaboration, follow-ups scheduled"
```

### Campaign Management
```bash
# After campaign milestone
# Track:
# - Metrics vs goals
# - What worked/didn't
# - Adjustments needed
# - Next phase readiness

bd close [task-id] --reason "Week 1 complete: 80% of target metrics achieved, pivoting messaging for week 2"
```

## Task Discovery and Management

### When You Discover New Work

During execution, you may discover additional tasks:

```bash
# Found during current task
bd create "DISCOVERED: Need infographic to support thread" -p 2
bd dep add [new-id] [current-id] --type discovered-from

# Found market opportunity
bd create "OPPORTUNITY: Trend-jack recent launch failure news" -p 0
bd dep add [new-id] [current-id] --type discovered-from

# Don't switch tasks - finish current work first
bd close [current-id] --reason "Complete, discovered visual content need"
```

### Managing Dependencies

```bash
# Check what's blocking a task
bd show [task-id]

# Add new dependency
bd dep add [dependent] [blocker]  # blocker must complete first

# View dependency tree for campaign
bd dep tree [campaign-epic-id]

# Find circular dependencies
bd dep cycles
```

## Progress Tracking

### Daily Standup View
```bash
# What's ready to work on?
bd ready

# What's in progress?
bd list --status in_progress

# What was completed today?
bd list --status closed --limit 10

# High priority items
bd list --priority 0
```

### Campaign Progress
```bash
# View campaign hierarchy with status
bd dep tree [campaign-epic-id]

# Check completion percentage
bd show [campaign-epic-id]  # Shows child task completion

# Overall statistics
bd stats
```

## Strategic Execution Best Practices

### Content Production Tasks
- Always create multiple versions for A/B testing
- Include metrics predictions in task notes
- Save all versions for future reference
- Track actual vs predicted performance

### Partnership Tasks
- Document all communications
- Create follow-up tasks immediately
- Track relationship temperature (cold/warm/hot)
- Note value exchange clearly

### Community Engagement Tasks
- Capture quantitative metrics (attendance, engagement)
- Document qualitative feedback
- Create follow-up tasks for raised issues
- Build recurring engagement cadence

### Analytics Tasks
- Automate data collection where possible
- Create templates for consistent reporting
- Track trends not just snapshots
- Generate actionable insights not just data

## Opals-Specific Considerations

### Fair Launch Narrative Tasks
- Every piece reinforces fair launch philosophy
- Avoid VC-friendly language
- Emphasize community alignment
- Use data to support claims

### Founder Education Tasks
- Focus on pain points and solutions
- Use real examples (anonymized if needed)
- Create actionable takeaways
- Build trust through transparency

### Patron NFT Campaign Tasks
- Explain value clearly (not speculation)
- Show community benefits
- Create FOMO through exclusivity not price
- Document holder stories

## AI Instructions for Task Execution

When executing strategic tasks with Beads:

1. **Always use Beads commands** - Never edit markdown task lists
2. **Check ready work first** - Use `bd ready` before starting
3. **Update status immediately** - Mark in_progress when starting
4. **Track metrics** - Document quantitative results in close reason
5. **Document discoveries** - File new issues for found opportunities
6. **Complete atomically** - Close task only when fully done
7. **Maintain dependencies** - Update deps when relationships change
8. **Think strategically** - Every task serves the larger campaign

## Example Task Execution Flow

```bash
# Find next task
bd ready
# Shows: opals-campaign-105 - Write thread on why 99% of launches fail

# Start work
bd update opals-campaign-105 --status in_progress

# Execute the task...
# - Research data on launch failures
# - Write compelling hook
# - Create 7-10 tweet thread
# - Review and optimize
# - Schedule in Typefully

# Task complete - close with results
bd close opals-campaign-105 --reason "Thread written and scheduled, hook: 'Nobody talks about this, but 99% of token launches are designed to fail. Here's the pattern I've seen 100+ times:'"

# Check for next task
bd ready
# Shows: opals-campaign-106 - Create supporting infographic

# Continue...
```

## Common Commands Reference

```bash
# Essential workflow
bd ready                       # Find unblocked work
bd update ID --status STATUS   # Update task status
bd close ID --reason "..."     # Complete task with results
bd create "..." -p 0 -t type   # Create high-priority task

# Discovery
bd create "..." --discovered-from ID     # Track found work
bd dep add NEW OLD --type discovered-from

# Progress tracking
bd stats                       # Overall statistics
bd dep tree ID                 # View campaign hierarchy
bd list --status in_progress   # Current work
bd list --status closed --limit 20  # Recent completions

# Investigation
bd show ID                     # Detailed task view
bd blocked                     # Show blocked tasks
bd dep cycles                  # Find circular dependencies
```

## Task Types for CEO Operations

### Content Types
- `content` - Threads, articles, videos, graphics
- `partnership` - Outreach, negotiations, collaborations
- `community` - Events, engagement, discussions
- `analytics` - Metrics, reports, insights
- `strategy` - Planning, research, positioning
- `epic` - Campaigns, initiatives, programs

### Priority Levels
- **P0**: Campaign critical, launch blockers
- **P1**: Important for success, should complete
- **P2**: Nice to have, bonus value

## Success Patterns

### High-Performing Task Execution
- Complete 3-5 tasks daily
- Close tasks with specific metrics/outcomes
- Discover 1-2 new opportunities per day
- Maintain clean dependency tree
- No tasks blocked unnecessarily

### Campaign Success Indicators
- 80%+ of planned tasks completed on time
- Metrics tracked for every task
- Clear progression through campaign phases
- Continuous discovery of improvements
- Team aligned through Beads visibility

## Remember

**Beads is our single source of truth for campaign execution.** All task creation, updates, and completion must go through Beads commands. This ensures proper dependency tracking, progress visibility, and strategic alignment.

Every task closed should include measurable outcomes that demonstrate progress toward campaign goals.