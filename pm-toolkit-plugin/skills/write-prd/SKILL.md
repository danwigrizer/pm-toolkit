---
name: write-prd
description: Write a complete Product Requirements Document (PRD) by invoking the prd-writer agent. Produces immediately executable, deterministic output with D-Sections, routing logic, user flows, and acceptance criteria. Use when defining product features or requirements.
argument-hint: feature name or description
disable-model-invocation: false
user-invokable: true
---

# Write a Product Requirements Document (PRD)

You are the PM team lead invoking the **prd-writer** agent to produce a complete, handoff-ready PRD.

## Step 1: Gather Information

If `$ARGUMENTS` is vague or missing detail, ask for:
- **Feature name** — what are we building?
- **Problem** — what user or business problem does it solve?
- **Target users** — who is affected and how?
- **Key requirements** — any known constraints or must-haves?
- **Current state** — does this replace or extend an existing flow?
- **Output path** — where to save the PRD (e.g., `docs/prds/feature-name.md`). If not specified, output to conversation.

Do not proceed with a vague feature description — the prd-writer needs enough context to produce deterministic requirements.

## Step 2: Invoke the prd-writer Agent

Once you have sufficient information, spawn the **prd-writer** subagent with a prompt that includes:
- The full feature description
- Any context gathered in Step 1
- The output file path (if provided)

The prd-writer will produce a complete PRD with all required sections:
1. Executive Summary
2. Problem Statement
3. Goals & Success Metrics
4. User Stories & Requirements (Desired Future State → User Flows → Routing Logic → D-Sections with Front End / Back End / Data/Analytics requirements and Acceptance Criteria)
5. Solution Overview
6. Timeline & Phasing
7. Dependencies & Blockers
8. Risks & Mitigation
9. Non-Goals
10. Success Criteria (Post-Launch)
11. Key Decision Points
+ Placeholder headers for Technical sections (technical-writer completes these separately)

## Step 3: Confirm Output

After the prd-writer completes:
- Confirm the file was saved (if a path was provided)
- Summarize what sections were written
- Note any Key Decision Points the PM should resolve before handoff

## Feature to Document

$ARGUMENTS
