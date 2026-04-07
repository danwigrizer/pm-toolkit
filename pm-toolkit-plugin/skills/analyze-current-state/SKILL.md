---
name: analyze-current-state
description: Analyze how a feature currently works by exploring the codebase. Extracts current user flows, business rules, routing logic, and edge cases. Produces a structured summary formatted for direct use in PRD authoring.
argument-hint: feature or flow to analyze
disable-model-invocation: false
user-invokable: true
---

# Analyze Current State

You are invoking the **prd-code-explorer** agent to analyze how a feature works today.

## Step 1: Gather Information

If `$ARGUMENTS` is vague or missing detail, ask for:
- **Feature or flow to analyze** — what area of the product? (e.g., "payout method setup", "checkout payment step")
- **Codebase paths** — relevant directories or service names (e.g., `src/payments/`, `payout-service`). If unknown, the explorer will infer from naming conventions.
- **Specific questions** — any focused questions to answer (e.g., "What happens if the user has no saved methods?")
- **Output path** — where to save the analysis (e.g., `research/payout-current-state.md`). If not specified, output to conversation.

## Step 2: Invoke the prd-code-explorer Agent

Spawn the **prd-code-explorer** subagent with the feature concept, codebase paths, and any specific questions.

The explorer will produce a structured summary covering:
- **Scope Analyzed** — paths and files examined, coverage notes
- **Current User Flows** — bracket notation end-to-end flows
- **Current User-Facing States & UX** — what users see in each condition
- **Current Business Rules & Routing Logic** — deterministic `Send to [X] if:` rules
- **Current Edge Cases & Fallbacks** — behavior when things go wrong
- **Current vs. Intended Behavior** — mismatches to address in the PRD (if applicable)
- **Notes for PRD Authoring** — mapped to specific PRD sections (Problem Statement, §4c Routing Logic, §4d D-Sections, §11 Key Decision Points)

## Step 3: Confirm Output

After the explorer completes:
- Confirm the file was saved (if a path was provided)
- Summarize key findings — especially any Current vs. Intended mismatches the PM should know about
- Note which PRD sections this analysis informs

## Feature to Analyze

$ARGUMENTS
