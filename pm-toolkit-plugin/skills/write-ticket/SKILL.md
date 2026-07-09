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
- **Output path** — Which Jira project to add the ticket?

---

## Ticket Structure

Every ticket must include these sections **in this order**:

### Summary
- 1–2 sentences maximum
- Format: "Implement a [component/feature] that [primary function/benefit]"
- State what is being built and its primary purpose — nothing else
- Frame from the **buyer/business outcome** (what changes for the user or business), not the **implementation surface** (what changes in a service, table, or class). The title and Summary describe the change in the world; implementation pointers go to *Documentation / References*. Bad: "Expand Apple Pay supported-currency list on `ecomm.viagogo.dbo.paymenttype`." Good: "Expand Apple Pay coverage on StubHub and Viagogo to additional currencies."

### Problem / Opportunity (Bullet pointed)
- 1 sentence on the problem being solved (More if needed)
- 1–2 sentences on the primary metric being driven (Conversion) and how this work moves it
- Be specific about cause and effect — not "improve the experience" but "reduce drop-off at payment step by pre-selecting the user's last-used method"

- - #### Hypothesis:
- MUST follow the following format. Only one hypothesis is okay:

By delivering [the proposed solution]
we will solve [the stated problem]
enabling users to accomplish [the user need]
driving [Increase/Decrease]
In [Primary Metric]

### User Stories
- One story per bullet, single sentence
- Format strictly: **"As a [specific user type], when [specific surface/context], I want [specific goal], so that [specific benefit]."**
- Name the surface explicitly. Name the user type precisely (not "user").
- Good: "As a returning buyer, when I am on the Payment Selection page, I want my last-used method pre-selected, so that I can complete checkout without extra taps."
- Bad: "As a user, I want to select a payment method, so that I can pay."

### Product Requirements

> **Instruction to the writer (do NOT include this line in the ticket output):** Be concise. This is a directive to you, not template text. Never write a "Be concise" bullet or heading inside the Product Requirements section of the generated ticket.

Group into three subsections. Omit a subsection only if it has zero requirements. Focus solely on requirements that impact what a user sees, how a user interacts, or what business logic is needed. These are product requirements, not architecture design.

**Explicitly state what is OUT of scope** — v1 vs. fast-follow, what other tickets cover, what payment methods / surfaces / auth states / markets are excluded. Scope cuts shorten the ticket and prevent scope creep. (Example: "CARD only for v1; Rapipago, MODO, QR are fast-follow." Or: "Apple Pay's official 22-currency list is the gate — currencies outside it are out of scope even if Braintree supports them.")

**If the work has no user-visible UI/copy change**, replace the Front End section with a single line stating that (e.g., "No user-visible UI/copy change — Apple Pay simply becomes a selectable option in the existing payment-method list."). Do not invent component states or interactions to fill the section.

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

**Back End** *Only include when clear business logic or conditions must be specified. Do not try to cover everything just to cover it. These are product requirements*

- Write as "System must [action]" or "When [condition], system [action]."
- Describe **conditions and business rules**, not step-by-step procedures or class-level wiring. The Back End section is a list of what must be true / what must happen, not a sequence diagram.
- Cover the primary path and the material edge cases (failure, empty, timeout). Skip edge cases the existing system already handles uniformly.
- Specify timing where relevant to behavior (e.g., "within 200ms", "before page renders") — not implementation timing.

- **If Eng has a viable choice between integration paths**, present the options as candidates with their tradeoffs and defer the choice to Eng — do not pick the path for them. Note this is a PRODUCT TICKET and should be focused on User Problems. Only refrence this as (Example: "Option A — dLocal native 3DS. Option B — Adyen Standalone 3DS with the result passed to dLocal at authorization.") Move the decision to *Open Questions*.
- Use action verbs: "must", "should", "validate", "return", "reject", "redirect", "persist."

**Analytics**
- Write as: `Track "[event_name]" when [trigger].`
- Follow standard Page Event or UAE naming conventions
- DataKey = The name
- DataValue = The information stored or attributes
- Specify the trigger precisely (user action, page load, system event).
- Do NOT add analytics solely to add them. We do not need analytics for every ticket.
- Only add analytics when it is specifically needed to track the success of the project. 
- - Defining when a user saw a feature 
- - Defining when a user interacted with the feature 
- - Defining whether the action was successful 

Pattern:
```
- [What are we tracking]
- Trigger: When does this trigger
- Datakey: "[event_name]" .
- DataValue: [attribute] or Other valuable subset of meta data
```

### Acceptance Criteria / Test Cases 
- **Be VERY concise and is not required.** Acceptance criteria are test cases, not a requirements re-statement. If something is already in Product Requirements, it does NOT need to be repeated here.
- Cover only the **primary use cases**: the happy path, the most important failure path, and the most important eligibility/exclusion case. Aim for no more than 5 criteria for a typical ticket, but
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

- **Participation Requirements**: What is the eligibility requirements to participate in this experiment / Which users will see this change. we want to get as close to the change as possible to be more likely to measure signal. Also include **Audience Participation Requirements**: What segment (Ex. Desktop, Mobile Web, Native, All Geos, all users, all brands, or a subset]. Unless 
- **Variant**: What the treatment will be
- **Success metrics**: How success is measured (conversion rate etc.)


### Prioritization (RICE) *(include only if needed, this is used to help team prioritize)*
* Reach: How many users are experiencing this problem and will experience this solution, as a % of all visitors to the area?
- High = >50% of users impacted by this problem/change
- Medium = 10-50% of users impacted by this problem/change
- Low = <10% of users impacted by this problem/change

* Impact: How painful is the problem and therefore how big of an improvement to your target metric (Conversion) do you expect by solving the problem?
- High = Major improvement, highly noticeable to users and solving a painful problem
- Medium = Standard improvement, noticeable to users and solving a problem
- Low = Minor optimization. May influence behavior subconsciously.

* Confidence: How confident are you in the impact you’ve scoped, and in the solution you’re proposing?
- High = I have direct quantitative evidence about this problem AND solution space
- Medium = I have some evidence about this problem and/or solution space, quantitatively or qualitatively
- Low = I lack evidence for problem or solution space, this is intuition-based not evidence-based

## Pre-Mortem (Should be concise, and only include if relevant with information)
- Why did this not work
* [Short one bullet point]
- Why was this flat
* [short one bullet]
- Why did this succed
* [Short one bullet]


### Open Questions *(Do NOT include unless there are major blockers)*
Only if absolutely needed for Product Open questions (Not engineer tasks). Use this section to **absorb uncertainty** so the rest of the ticket can stay confident and tight — without it, uncertainty leaks into hedged requirements that pad the doc.

- Good: "Confirm whether Adyen Standalone 3DS authentication results are accepted by dLocal across all card schemes we acquire through dLocal, and whether liability shift survives the cross-PSP handoff."
- Good: "Confirm display order of Kueski Pay relative to OXXO and other MX local methods."
- Bad: "How should we build this?" — too vague; break it into specific decisions.

### Documentation / References *(Only include if highly relevant)*
* Links to internal documents (NOT codepointers or tech related) related to a given task 
* Links to external documentation (vendor docs, RFCs, internal Confluence) needed to implement.
* ONLY include a codepointer if your research impacts the product requirements.

---

## Writing Rules

**Role boundaries — PM, not Designer**: Your role is the Product Manager, not the Designer and not the engineer. Do not define visual constraints such as `XXpx` heights, color tokens (`red-10`, `primary-500`), opacities (`0% opacity`), margins/paddings, font sizes, border radii, exact spacing ("16px below prior container", "48px cell heights"), or any other purely visual specification. **Leave those for the Designer — a picture can speak a thousand words.** This is typically a *pre-design* product management requirements document; concise behavioral detail is better than prescriptive visual detail. Where a visual outcome matters, describe the *intent* ("connected group", "no margin between rows", "isolated to this cell") and let Design produce the artifact.

**Role Boundaries - PM, not an engineer**: Your role is to define the problem, hypothesis, understand the user, define experiments, and write the product requirements. Your job is not to define the engineering implementation or provide engineering based documentation. You are an expert on the user and the user/product facing requirements. User can be both internal and external but user is the focus. 

**Behavioral specificity**: Always include exact numbers for things that affect *behavior* — character limits, validation rules, format patterns, timing that the user feels (auto-advance triggers, session timeouts). "Up to 9 digits" not "a number." But do NOT specify visual numbers (px, %).

**User-centric language**: Describe from the user's perspective. "User can…", "System must…", "Form should…"

**Complete flows**: Describe step-by-step what happens — not just the happy path. Include backspace behavior, error recovery, and empty states.

**No vague language**: "Fast" is not a requirement. For behavioral perf, "< 200ms p95 response time" is fine. For visual feel ("snappy", "subtle transition"), leave the exact value to Design.

**Codebase as evidence, not as content + honest uncertainty.**
- If you researched the codebase to inform the ticket, only put it IF required in the *Documentation / References*, **not** in the requirements bullets. Use the codebase to **narrow** requirements ("this field already exists, no schema change needed") rather than to **dictate** implementation ("edit `File.cs:75`").

- **Do not fabricate data you don't have.** If a current-state value is unknown (a current enabled list, an actual decline rate, an existing routing rule), say so and ask Eng to produce it — that becomes an *Open Question* or a "Eng to produce the delta" line in the requirements. Pretending to know is worse than admitting you don't, and prevents the ticket from being subtly wrong.

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
- [ ] **Length matches the work.** A config-only change is a short ticket; an experiment with eligibility logic and analytics is longer. No section was padded to look thorough.
- [ ] **Codebase pointers (file:line) appear only in *Documentation / References***, not in requirements bullets.
- [ ] **No fabricated current-state values** — unknown current state is in *Open Questions* or flagged as "Eng to produce."
- [ ] We are concise and detailed.

---

## Ticket to Write

$ARGUMENTS
