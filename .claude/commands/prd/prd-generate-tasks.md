---
description: Generate Tasks from a Product Requirements Document using Beads
---
# Generate Tasks from Product Requirements Document

## Goal

To transform a Product Requirements Document (PRD) into a comprehensive set of executable tasks tracked in Beads, with proper dependencies, priorities, and organization.

## Process

1. **Analyze the PRD:** Review the product requirements document to understand objectives, requirements, and timeline
2. **Create Task Hierarchy:** Organize tasks into epics, workstreams, and individual tasks
3. **Generate Beads Commands:** Create the actual `bd` commands to set up the task structure
4. **Establish Dependencies:** Map task relationships and blockers
5. **Set Priorities:** Assign P0 (critical), P1 (important), P2 (nice-to-have) levels

## Task Breakdown Structure

### Level 1: Initiative Epic
The top-level container for the entire initiative
```bash
bd create "[Initiative Name] Campaign" -t epic -p 0
```

### Level 2: Workstream Epics
Major workstreams within the initiative
```bash
bd create "Content Creation Workstream" -t epic -p 0
bd create "Partnership Development Workstream" -t epic -p 0
bd create "Community Engagement Workstream" -t epic -p 0
bd create "Analytics & Measurement Workstream" -t epic -p 1
```

### Level 3: Individual Tasks
Specific, executable tasks within each workstream

## Task Generation Guidelines

### Good Task Characteristics
- **Specific:** "Write 1500-word article on Patron NFTs" not "Create content"
- **Measurable:** Clear completion criteria
- **Assignable:** One person can own it
- **Time-bounded:** Can be completed in 1-3 days
- **Relevant:** Directly supports initiative goals

### Task Naming Convention
```
[Action] [Specific Deliverable] [Optional: Context]

Examples:
✅ "Write 3-part Twitter thread on fair launch mechanics"
✅ "Schedule 5 Twitter Spaces with founder communities"
✅ "Create visual infographic comparing Opals vs traditional launchpads"
✅ "Reach out to 20 Web3 media outlets for launch coverage"

❌ "Do marketing"
❌ "Community stuff"
❌ "Create content"
```

## Task Categories for CEO Operations

### Content Tasks
```bash
bd create "Write viral thread: Why 99% of launches fail" -p 0 -t content
bd create "Create long-form article: Fair Launch Manifesto" -p 0 -t content
bd create "Produce video script: 60-second Patron NFT explainer" -p 1 -t content
bd create "Design infographic: Token vesting timeline" -p 2 -t content
```

### Partnership Tasks
```bash
bd create "Research 30 potential founder communities" -p 0 -t partnership
bd create "Draft partnership proposal for DAO frameworks" -p 0 -t partnership
bd create "Schedule calls with 10 ecosystem partners" -p 1 -t partnership
bd create "Create co-marketing plan with top 3 partners" -p 1 -t partnership
```

### Community Tasks
```bash
bd create "Host Twitter Space: Fair Launch Q&A" -p 0 -t community
bd create "Create Discord discussion prompts (5 topics)" -p 1 -t community
bd create "Launch ambassador program application" -p 1 -t community
bd create "Organize virtual meetup for founders" -p 2 -t community
```

### Analytics Tasks
```bash
bd create "Set up tracking for campaign metrics" -p 0 -t analytics
bd create "Create weekly performance dashboard" -p 1 -t analytics
bd create "Compile engagement report for Week 1" -p 1 -t analytics
bd create "Analyze competitor campaigns" -p 2 -t analytics
```

## Dependency Management

### Common Dependency Patterns

**Sequential Dependencies:**
```bash
# Research must happen before content creation
bd dep add create-content complete-research

# Content must be created before publishing
bd dep add publish-content create-content

# Messaging framework needed before partner outreach
bd dep add partner-outreach messaging-framework
```

**Parallel Workstreams:**
```bash
# These can happen simultaneously
# No dependencies between them:
- Content creation
- Partnership development
- Community planning
```

**Gate Dependencies:**
```bash
# Everything blocks on strategy approval
bd dep add content-tasks strategy-approval
bd dep add partnership-tasks strategy-approval
bd dep add community-tasks strategy-approval
```

## Priority Framework

### P0 - Critical (Must Have)
- Launch blockers
- Core content pieces
- Primary partnerships
- Success metric tracking

### P1 - Important (Should Have)
- Supporting content
- Secondary partnerships
- Community engagement
- Performance optimization

### P2 - Nice to Have (Could Have)
- Bonus content
- Extended partnerships
- Advanced analytics
- Experimental initiatives

## Complete Example: Fair Launch Campaign

```bash
# Create main epic
bd create "Fair Launch Education Campaign Q1" -t epic -p 0

# Content workstream
bd create "Content: Research phase" -p 0 -t content
bd create "Content: Write 5 educational threads" -p 0 -t content
bd create "Content: Create 2 long-form articles" -p 0 -t content
bd create "Content: Design visual assets" -p 1 -t content
bd create "Content: Schedule and publish all content" -p 0 -t content

# Partnership workstream
bd create "Partners: Identify 30 founder communities" -p 0 -t partnership
bd create "Partners: Outreach to top 10 communities" -p 0 -t partnership
bd create "Partners: Negotiate 3 co-marketing deals" -p 1 -t partnership
bd create "Partners: Execute joint activities" -p 1 -t partnership

# Community workstream
bd create "Community: Plan 4 Twitter Spaces" -p 0 -t community
bd create "Community: Create Discord engagement plan" -p 1 -t community
bd create "Community: Launch founder survey" -p 1 -t community
bd create "Community: Host virtual meetup" -p 2 -t community

# Analytics workstream
bd create "Analytics: Set up tracking dashboard" -p 0 -t analytics
bd create "Analytics: Week 1 performance report" -p 1 -t analytics
bd create "Analytics: Week 2 performance report" -p 1 -t analytics
bd create "Analytics: Final campaign analysis" -p 0 -t analytics

# Add key dependencies
bd dep add content-write content-research
bd dep add content-publish content-write
bd dep add partners-outreach partners-identify
bd dep add partners-execute partners-negotiate
bd dep add community-spaces content-write  # Need content first
bd dep add analytics-week1 content-publish  # Can't measure until published
```

## Tracking Progress

Once tasks are created, use these commands:

```bash
# Daily standup
bd ready                    # What's unblocked and ready?
bd list --status in_progress  # What's currently being worked?

# Update progress
bd update [task-id] --status in_progress
bd close [task-id] --reason "Completed: Published thread with 50K impressions"

# View dependencies
bd dep tree [epic-id]      # See full campaign structure
bd blocked                 # What's waiting on other tasks?
```

## Success Metrics for Task Management

- **Task Velocity:** Completing 3-5 tasks per day
- **Dependency Management:** No tasks blocked unnecessarily
- **Priority Focus:** P0 tasks completed before P1/P2
- **Completion Rate:** 80%+ of planned tasks completed per week
- **Quality Metrics:** Tasks meet success criteria when closed

## Integration Notes

This command works with:
- `/prd:prd-create` - Creates the Product Requirements Document
- `/prd:prd-process-task-list` - Executes the generated tasks
- **Task Manager agent** - Helps create comprehensive PRDs and plans
- **Campaign Manager agent** - Focuses on campaign-specific execution