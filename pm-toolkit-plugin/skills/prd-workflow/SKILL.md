---
name: prd-workflow
description: End-to-end PRD creation workflow. Optionally analyzes current codebase state, maps current and future flows, then writes a complete PRD with embedded diagrams grounded in real behavior. Lighter than pm-full-cycle — focused on PRD only.
argument-hint: feature name or description
disable-model-invocation: false
user-invokable: true
---

# PRD Workflow

You are the team lead for a focused PRD creation pipeline using up to three specialized agents: **prd-code-explorer**, **flow-mapper**, and **prd-writer**.

## Step 1: Gather Information

Ask the user for:
- **Feature name and description** — what are we documenting?
- **Does an existing implementation exist?** — Yes/No. If yes, get codebase paths for current state analysis.
- **Key requirements or changes** — what should be different from today?
- **Output file path** — where to save the final PRD (e.g., `docs/prds/feature-name.md`)

---

## Step 2: Analyze Current State (skip if no existing implementation)

Spawn the **prd-code-explorer** subagent with:
- The feature concept
- Codebase paths provided by the user

Save findings to `research/[feature-name]-current-state.md`.

The explorer's output feeds directly into:
- The PRD's Problem Statement (current friction and limitations)
- Section 4c (current routing rules as the baseline to change)
- Section 4d D-Sections (current behavior per surface)
- Section 11 Key Decision Points (current vs. intended mismatches)

---

## Step 3: Map Current State Flow (skip if no existing implementation)

Spawn the **flow-mapper** subagent with the code explorer findings as source material.

Request: current state flow in the most appropriate format (flow-mapper will auto-select).

This produces the "before" diagram for embedding in section 4b.

---

## Step 4: Map Future State Flow

Spawn the **flow-mapper** subagent with the feature requirements and desired changes as source material.

Request: future state flow showing the proposed behavior.

If both current and future flows exist, also request a **comparison flow** with a delta summary (what's removed, added, changed, and impact).

This produces the "after" diagram (and optional comparison) for embedding in section 4b.

---

## Step 5: Write the PRD

Spawn the **prd-writer** subagent with:
- The full feature description and requirements
- Current state findings from the code explorer (if available)
- The current state flow (if available) — for embedding in section 4b
- The future state flow — for embedding in section 4b
- The comparison flow (if available) — for embedding in section 4b
- The output file path

The prd-writer will produce a complete PRD with all 11 product sections plus technical section placeholders, with the flows embedded in section 4b.

---

## Final Confirmation

Once the prd-writer completes, confirm:
- PRD saved to: `[file path]`
- Flows embedded: current / future / comparison (note which were included)
- Key Decision Points: list any open questions the PM should resolve before handoff
- Technical sections: remind the user that technical-writer should complete those sections

---

## Scope Note

This workflow covers the PRD only. For a full product documentation package (research + PRD + press release + tickets + review), use `/pm-full-cycle` instead.

---

## Feature to Document

$ARGUMENTS
