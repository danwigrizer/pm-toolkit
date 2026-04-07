---
name: create-flows
description: Create, validate, or convert user flow diagrams in Mermaid flowchart, sequence diagram, state diagram, or bracketed text formats. Output is formatted for direct embedding in PRD section 4b (User Flows).
argument-hint: feature name and flow type (current, future, or comparison)
disable-model-invocation: false
user-invokable: true
---

# Create Flow Diagrams

You are invoking the **flow-mapper** agent to create user flow diagrams.

## Step 1: Determine What's Needed

If `$ARGUMENTS` is vague or missing detail, ask for:
- **Feature name** — what feature or flow are we mapping?
- **Flow type** — which do you need?
  - **Current state**: How the feature works today (use alongside `analyze-current-state`)
  - **Future state**: Proposed behavior from PRD requirements
  - **Comparison**: Current vs. future side-by-side with a delta summary
- **Context or source**:
  - For current state: codebase paths or an existing `analyze-current-state` output
  - For future state: PRD description or requirements
- **Desired format** (optional — flow-mapper will auto-select if not specified):
  - `flowchart` — branching logic and decision trees
  - `sequence` — system interactions and API flows
  - `state` — status workflows and object lifecycle
  - `text` — simple linear paths in bracketed notation

## Step 2: Invoke the flow-mapper Agent

Spawn the **flow-mapper** subagent with the feature context, flow type, and source material.

The flow-mapper will produce:
- **Format selection rationale** — why it chose the format it did
- **Primary flow diagram** — main path with all branches and error paths
- **Edge cases covered** — what edge scenarios are represented
- **PRD placement notes** — which Option (1–4) this maps to in section 4b, ready to paste

For comparison flows, it will produce both current and future diagrams plus a delta summary (what was removed, added, changed, and the impact).

## Step 3: Confirm Output

After the flow-mapper completes:
- Confirm the diagram is valid (no unreachable states, all branches have outcomes)
- Note which PRD section 4b Option label to use when embedding
- Note any edge cases the PM should explicitly handle in D-Sections

## Feature to Map

$ARGUMENTS
