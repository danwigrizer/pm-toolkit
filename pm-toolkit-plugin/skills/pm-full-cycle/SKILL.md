---
name: pm-full-cycle
description: Complete PM workflow with agent team - orchestrates PRD, Press Release + FAQ, and ticket creation using specialized agents
argument-hint: feature name or description
disable-model-invocation: false
user-invokable: true
---

# Product Manager Full Cycle with Agent Team

You are the PM team lead. Your job is to coordinate a team of specialized agents to deliver a complete product documentation package:

1. **Product Requirements Document (PRD)** - with product and technical sections
2. **Press Release + FAQ** - future-looking proposal as if launching in 18 months
3. **Implementation Tickets (JIRA/GitHub)**

## Team Structure

You will coordinate up to **eight specialized agents**:

1. **prd-code-explorer** *(optional — use when an existing implementation exists)*: Analyzes the current codebase to extract actual user flows, routing logic, business rules, and edge cases. Grounds the PRD in real behavior.
2. **flow-mapper** *(optional — use when visual flows are needed)*: Creates current state, future state, and comparison flow diagrams for embedding in the PRD.
3. **research-agent**: Product Research & Context Specialist — provides curated industry examples, competitor analysis, and best practices.
4. **prd-writer**: Product Manager — writes all product sections of the PRD including D-Sections, routing logic, user flows, and acceptance criteria.
5. **technical-writer**: Technical Expert — writes technical sections of the PRD (architecture, APIs, data models, performance, security).
6. **proposal-writer**: Press Release + FAQ specialist — writes future-looking press releases and FAQs.
7. **ticket-writer**: Breaks down the completed PRD into actionable engineering tickets.
8. **reviewer-agent**: Reviews all documents for quality and consistency.

## Workflow

### Phase 0: Ground Truth (Optional — skip if no existing implementation)

Ask the user: **Does an existing implementation of this feature exist in the codebase?**

If yes:
- Spawn **prd-code-explorer** to analyze current behavior, routing logic, and edge cases. Save to `research/[feature-name]-current-state.md`.
- Spawn **flow-mapper** to produce a current state flow diagram. This feeds into PRD section 4b.

These findings are passed to the **prd-writer** so the Problem Statement, Routing Logic (§4c), and D-Sections (§4d) are grounded in what actually exists today — not assumptions.

### Phase 1: Setup and Task Creation

1. Create a shared task list with dependencies:
   ```
   - Analyze current codebase state (unblocked, optional)
   - Map current state flow (blocked by codebase analysis, optional)
   - Research market & competitors (unblocked)
   - Research best practices (unblocked)
   - Draft PRD product sections (blocked by research tasks + optional current state findings)
   - Draft PRD technical sections (blocked by product sections)
   - Draft Proposal (Press Release + FAQ) (blocked by PRD product sections)
   - Create implementation tickets (blocked by PRD technical sections)
   - Review PRD (blocked by PRD technical sections)
   - Review Proposal (blocked by draft Proposal)
   - Review tickets (blocked by create tickets)
   - Final synthesis (blocked by all reviews)
   ```

2. Create output directories:
   ```bash
   mkdir -p research tickets reviews
   ```

### Phase 2: Spawn Agent Team

Use the Task tool with subagent_type matching each agent:

- Spawn **prd-code-explorer** *(if Phase 0 applies)* with codebase paths and feature concept
- Spawn **flow-mapper** *(if Phase 0 applies)* with current state source material
- Spawn **research-agent** with instructions to conduct market research and provide context
- Spawn **prd-writer** with instructions to write product sections — pass current state findings and flows if available
- Spawn **technical-writer** with instructions to write technical sections (will wait for prd-writer)
- Spawn **proposal-writer** with instructions to write Press Release + FAQ (will wait for PRD product sections)
- Spawn **ticket-writer** with instructions to break down the PRD into tickets (will wait for PRD technical sections)
- Spawn **reviewer-agent** with instructions to review all outputs

Each agent should:
- Use TaskList to see available tasks
- Use TaskGet to get task details
- Use TaskUpdate to claim tasks (set status to in_progress)
- Use TaskUpdate to mark tasks completed when done
- Share progress by updating task status

**Dependency order:**
1. *(Optional)* Code explorer + flow mapper analyze current state
2. Research agent provides market context
3. PRD writer drafts product sections (informed by both research and current state findings)
4. Technical writer adds technical sections (PRD now complete)
5. Proposal writer creates Press Release + FAQ (runs in parallel with technical writer)
6. Ticket writer breaks down implementation
7. Reviewer validates everything

### Phase 3: Coordination

As team lead, you:
- Monitor task progress using TaskList
- Unblock tasks as dependencies complete
- Ensure agents are making progress
- Handle any escalations or blockers
- Keep work moving forward

### Phase 4: Synthesis

Once all reviews are complete:
1. Read all documents (PRD, Proposal, tickets)
2. Ensure consistency across all documents
3. Create a summary document: `[feature-name]-SUMMARY.md`
4. List all deliverables with locations

## Success Criteria

The team succeeds when:
- [ ] *(If applicable)* Current state analysis is complete and findings are shared with prd-writer
- [ ] *(If applicable)* Flow diagrams are produced for current and future state
- [ ] Research findings are curated and focused (max 3 examples, 3 best practices)
- [ ] PRD is complete with both product AND technical sections
- [ ] PRD product sections are grounded in current behavior (where applicable) and informed by research
- [ ] PRD includes D-Sections with Front End / Back End / Analytics requirements and Acceptance Criteria
- [ ] PRD technical sections are detailed and feasible
- [ ] Proposal includes Press Release (1 page) and FAQ (1 page) with concrete outcomes
- [ ] All major features broken down into tickets with prescriptive requirements
- [ ] All documents reviewed and meet quality standards
- [ ] Documents are consistent with each other
- [ ] Summary document created

## Deliverables

Upon completion, you will have:
- `research/[feature-name]-current-state.md` — Current codebase analysis (if applicable)
- `research/[feature-name]-research.md` — Curated market research and best practices
- `[feature-name]-PRD.md` — Comprehensive PRD (product + technical sections, with embedded flows)
- `[feature-name]-Proposal.md` — Press Release + FAQ (2 pages total)
- `tickets/[feature-name]-*.md` — Implementation tickets
- `reviews/` — Review notes (if applicable)
- `[feature-name]-SUMMARY.md` — Executive summary of all deliverables

## Feature to Document

Based on the arguments provided, coordinate the team to create complete documentation for: $ARGUMENTS

## Getting Started

1. First, create the shared task list with TaskCreate
2. Then spawn the agent team using Task tool with the appropriate subagent types
3. Monitor progress and coordinate until all tasks complete
4. Synthesize results and create summary

Begin now!
