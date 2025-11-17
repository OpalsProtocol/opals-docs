---
description: Create a Product Requirements Document (PRD)
---
# Rule: Generating a Product Requirements Document (PRD)

## Goal

To create a detailed Product Requirements Document in Markdown format for marketing campaigns, go-to-market initiatives, partnership programs, community strategies, or any business initiative. The document should be clear, actionable, and suitable for anyone on the team to understand and execute.

## Process

1. **Receive Initial Request:** The user provides a brief description of an initiative, campaign, or project.
2. **Ask Clarifying Questions:** Before writing the PRD, *must* ask clarifying questions to gather sufficient detail. The goal is to understand the "what" and "why" of the initiative. Provide options in letter/number lists for easy responses.
3. **Generate PRD:** Based on the initial request and answers, generate a PRD using the structure below.
4. **Save PRD:** Save the document as `[n]-prd-[initiative-name].md` inside the `/tasks` directory. (Where `n` is a zero-padded 4-digit sequence starting from 0001, e.g., `0001-prd-founder-education.md`, `0002-prd-patron-nft-campaign.md`, etc.)

## Clarifying Questions (Examples)

Adapt questions based on the initiative type:

* **Problem/Goal:** "What problem does this initiative solve for Opals?" or "What is the main goal we want to achieve?"
* **Target Audience:** "Who is the primary audience for this initiative? (Founders, investors, community members?)"
* **Core Activities:** "What are the key activities or deliverables?"
* **User Stories:** "Can you describe some user journeys? (e.g., As a founder, I want to understand fair launches so that I can make better decisions)"
* **Success Criteria:** "How will we know when this initiative is successful? What are the key metrics?"
* **Scope/Boundaries:** "Are there specific things this initiative *should not* include?"
* **Content Requirements:** "What content needs to be created (threads, articles, videos)?"
* **Timeline:** "What is the target timeline? Any key dates or milestones?"
* **Resources:** "What resources are available (team members, budget, tools)?"
* **Risks:** "What are potential risks or challenges?"

## PRD Structure

The generated PRD should include:

### 1. Executive Summary
Brief overview of the initiative and why it matters for Opals

### 2. Strategic Objectives
- Primary goal (specific, measurable)
- Secondary goals
- Alignment with Opals mission

### 3. Target Audience
- Primary persona (detailed description)
- Secondary personas
- Pain points and motivations
- Where they spend time (channels)

### 4. Requirements

#### Content Requirements
- List specific content pieces needed
- Format and length for each
- Key messages to communicate
- Distribution channels

#### Partnership Requirements
- Target partners and why
- Value exchange
- Collaboration model

#### Community Requirements
- Engagement tactics
- Events or activities
- Ambassador/advocate programs

#### Resource Requirements
- Team members needed
- Tools or platforms required
- Budget considerations

### 5. User/Audience Journey
- Discovery: How they find us
- Engagement: How they interact
- Conversion: Desired actions
- Retention: Ongoing relationship

### 6. Success Metrics
- Quantitative KPIs (impressions, engagement, conversions)
- Qualitative indicators (sentiment, feedback quality)
- Measurement methods
- Reporting cadence

### 7. Timeline & Milestones
- Phase 1: [Activities and deadline]
- Phase 2: [Activities and deadline]
- Phase 3: [Activities and deadline]
- Key milestones and checkpoints

### 8. Task Breakdown (For Beads)
20-50 specific tasks with:
- Clear descriptions
- Dependencies noted
- Priority levels (P0, P1, P2)
- Time estimates
- Success criteria

### 9. Risks & Mitigation
- Identified risks
- Mitigation strategies
- Contingency plans

### 10. Open Questions
- Remaining questions needing clarification
- Decisions to be made
- Dependencies on external factors

## Target Audience

The primary reader is anyone on the Opals team who needs to understand and execute the initiative. Requirements should be explicit, unambiguous, and avoid unnecessary jargon.

## Output Example

```markdown
# Founder Education Program - Product Requirements Document

## Executive Summary
Create a comprehensive education program to help Web3 founders understand fair launch principles and how Opals enables sustainable token launches...

## Strategic Objectives
- Primary: Educate 100 founders on fair launch mechanics by Q2
- Secondary: Generate 50 qualified leads for Opals platform
- Alignment: Supports mission of making fair launches the standard

## Target Audience
### Primary Persona: Early-Stage Web3 Founder
- Building first protocol/dApp
- Concerned about sustainable funding
- Skeptical of VC-dominated launchpads
- Active on Twitter, Discord, and GitHub

[Continue with full structure...]
```

## Integration with Beads

After creating the PRD, generate Beads commands:

```bash
# Create epic for the initiative
bd create "[Initiative Name]" -t epic -p 0

# Create tasks from the breakdown
bd create "Research founder pain points" -p 0 -t research
bd create "Create education curriculum" -p 0 -t content
bd create "Write Module 1: Fair Launch Basics" -p 1 -t content

# Add dependencies
bd dep add write-module-1 create-curriculum
```

## Usage

When user says:
- "Create a PRD for [initiative]"
- "Help me plan [campaign]"
- "Design a strategy for [goal]"

You should:
1. Ask clarifying questions
2. Generate comprehensive PRD
3. Break into Beads tasks
4. Save to `/tasks` directory