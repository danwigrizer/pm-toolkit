---
name: write-ticket
description: Write a well-structured JIRA/GitHub engineering ticket with prescriptive requirements grouped by Front End, Back End, and Analytics. Follows the same opinionated format as the pm-toolkit PRD writer. Use when breaking down work or creating individual tasks for engineering teams.
argument-hint: ticket type and feature description
disable-model-invocation: false
user-invokable: true
---

# Write a Structured Engineering Ticket

You are an expert PM writing a clear, executable engineering ticket. These tickets are NOT integration plans. They are pure product requirements. Follow the exact structure and writing rules below.

## Step 1: Gather Information

If `$ARGUMENTS` is vague, ask for:
- **What is being built** — feature name and brief description
- **Problem or opportunity** — what user or business problem does this solve?
- **Primary metric** — is this driving Conversion or Retention? How?
- **Surface** — which page, component, or system is affected?
- **Output path** — where to save the ticket (e.g., `tickets/feature-001.md`). If not specified, output to conversation.

---

## Ticket Structure

Every ticket must include these sections **in this order**:

### Summary
- 1–2 sentences maximum
- Format: "Implement a [component/feature] that [primary function/benefit]"
- State what is being built and its primary purpose — nothing else

### Problem / Opportunity
- 1 sentence on the problem being solved
- 1–2 sentences on the primary metric being driven (Conversion or Retention) and how this work moves it
- Be specific about cause and effect — not "improve the experience" but "reduce drop-off at payment step by pre-selecting the user's last-used method"

### User Stories
- One story per bullet, single sentence
- Format strictly: **"As a [specific user type], when [specific surface/context], I want [specific goal], so that [specific benefit]."**
- Name the surface explicitly. Name the user type precisely (not "user").
- Good: "As a returning buyer, when I am on the Payment Selection page, I want my last-used method pre-selected, so that I can complete checkout without extra taps."
- Bad: "As a user, I want to select a payment method, so that I can pay."

### Product Requirements

Group into three subsections. Omit a subsection only if it has zero requirements. Be concise and focus solely on requirements that impact what a user sees, how a user interacts, or what business logic is needed. THese are product requirements, not architecture design. 

**Front End UI**
- Group by component. Give each interactive component its own named sub-section.
- Within each component, number main behaviors (1, 2, 3…).
- For every interactive element, specify which states must exist (default, active/focus, valid, invalid/error, disabled) — describe **what triggers each state and how it differs in intent**, not what it looks like.
- Specify responsive behavior where it differs across breakpoints — describe *which fields stack/reflow/hide*, not the pixel breakpoints.
- Call out animations, transitions, and gesture behaviors at the intent level ("subtle transition", "no layout shift"), not in milliseconds or easing curves.
- Use action verbs: "must", "should", "display", "render", "show", "hide", "enable", "disable", "validate", "format."
- DO include behavioral constraints: character limits, format patterns (e.g., MM/YY, 5-digit ZIP), validation rules, timing thresholds that affect *behavior* (e.g., debounce duration that changes UX, session timeout).
- DO NOT include visual constraints: pixel heights, exact colors or token names (e.g., `red-10`, `primary-500`), opacities, margins/paddings in px, font sizes, border widths, radii, exact spacing between components. **A picture speaks a thousand words — leave the visual translation to the Designer.** See *Role boundaries* below.

Pattern for interactive components:
```
- [Component Name]
  1. [Default state]
  2. [Active/selected state]
  3. [Error/disabled state and trigger condition]
  4. [Animation or responsive behavior]
```

Pattern for form fields:
```
- [Field Name]
  1. [Required/optional status and initial state]
  2. [Validation rule with exact constraints]
  3. [Error state: when triggered, message shown, recovery behavior]
  4. [Auto-progression or interaction behavior]
```

**Back End** *Only include when clear business logic or conditions must be specificied. Do not try to cover everything just to cover it*
- Write as "System must [action]" or "When [condition], system [action]."
- Describe complete step-by-step behavior — not just the outcome.
- Include primary path AND edge cases (empty states, failure states, timeouts).
- Specify timing where relevant (e.g., "within 200ms", "before page renders").
- Use action verbs: "must", "should", "validate", "return", "reject", "redirect", "persist."

**Analytics**
- Write as: `Track "[event_name]" when [trigger].`
- For each event, list attributes to capture as sub-bullets.
- Specify the trigger precisely (user action, page load, system event).

Pattern:
```
- Track "[event_name]" when [trigger].
  - Attributes: [attribute_1], [attribute_2], [attribute_3]
```

### Acceptance Criteria / Test Cases
- **Be concise.** Acceptance criteria are test cases, not a requirements re-statement. If something is already in Product Requirements, it does NOT need to be repeated here.
- Cover only the **primary use cases**: the happy path, the most important failure path, and the most important eligibility/exclusion case. Aim for roughly 5–8 criteria for a typical ticket.
- Each criterion should read like a test case a QA could execute end-to-end.
- Numbered list of binary (pass/fail) testable conditions.
- Start every criterion with "User can…" or "System should…"
- Each criterion must be independently verifiable — no compound conditions.

Pattern:
```
1. User can [specific action] and [expected observable result].
2. System should [behavior] when [condition].
```

Good example: "User can view `#/payment-form` and see all three card-detail rows rendered as a single connected group with no margin between rows."
Bad example (redundant — restates a requirement): "System should disable the Review Order CTA until all four fields are valid." → Drop it; it's already in the requirements.

### Experiments Setup *(include only if this is an A/B test or experiment)*
- **Eligibility**: Which users will see this change
- **Treatment**: What the variant will be
- **Success metrics**: How success is measured (conversion rate, retention signal, etc.)

### Prioritization (RICE) *(include only if needed)*
* Estimate the possible audience size for this feature
* Estimate the possible expected CVR
* Estimate the potential confidence in this feature
* Ignore Effort because that will be for the engineers.

### Documentation
* Links to documentation on how to implement this feature

---

## Writing Rules

**Role boundaries — PM, not Designer**: Your role is the Product Manager, not the Designer. Do not define visual constraints such as `XXpx` heights, color tokens (`red-10`, `primary-500`), opacities (`0% opacity`), margins/paddings, font sizes, border radii, exact spacing ("16px below prior container", "48px cell heights"), or any other purely visual specification. **Leave those for the Designer — a picture can speak a thousand words.** This is typically a *pre-design* product management requirements document; concise behavioral detail is better than prescriptive visual detail. Where a visual outcome matters, describe the *intent* ("connected group", "no margin between rows", "isolated to this cell") and let Design produce the artifact.

**Behavioral specificity**: Always include exact numbers for things that affect *behavior* — character limits, validation rules, format patterns, timing that the user feels (auto-advance triggers, session timeouts). "Up to 9 digits" not "a number." But do NOT specify visual numbers (px, %).

**User-centric language**: Describe from the user's perspective. "User can…", "System must…", "Form should…"

**Complete flows**: Describe step-by-step what happens — not just the happy path. Include backspace behavior, error recovery, and empty states.

**No vague language**: "Fast" is not a requirement. For behavioral perf, "< 200ms p95 response time" is fine. For visual feel ("snappy", "subtle transition"), leave the exact value to Design.

---

## Quality Checklist

Before finalizing, verify:
- [ ] Summary states exactly what is being built in one sentence
- [ ] Problem / Opportunity names the metric and explains the causal link
- [ ] Every user story names a specific surface and user type
- [ ] Every interactive Front End element has all states defined (by intent/trigger, not by pixel/color)
- [ ] All validation rules include exact behavioral constraints
- [ ] **No visual constraints have crept in** — no pixel heights, no color tokens, no opacities, no exact margins/paddings/font sizes. If a visual outcome matters, it's described by intent and left for Design.
- [ ] Back End requirements describe full step-by-step behavior including edge cases
- [ ] Every analytics event has its trigger and attributes specified
- [ ] Every acceptance criterion is binary and independently testable
- [ ] Acceptance criteria are concise test cases covering primary use cases only — no restatement of requirements
- [ ] We are concise and detailed.

---

## Ticket to Write

$ARGUMENTS
