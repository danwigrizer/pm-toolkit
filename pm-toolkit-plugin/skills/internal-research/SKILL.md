---
name: internal-research
description: Conducts deep internal research across company knowledge sources such as Google Drive, SharePoint, Confluence, Slack, Jira, docs, PRDs, decision logs, and chat history. Produces a structured research report that explains the history, current state, key decisions, open questions, risks, and source-backed evidence for a given topic.
---

# Internal Research

## Purpose

Use this skill when the user wants to understand an internal topic deeply, especially when knowledge is fragmented across many systems and has evolved over time.

This skill is designed for:
- product managers learning a new area
- historical research on decisions and tradeoffs
- onboarding into a product area or initiative
- understanding why something works the way it does
- synthesizing scattered knowledge into one clear report
- identifying unresolved questions, inconsistencies, or missing documentation

This skill should act like a highly capable internal researcher:
- search broadly
- read deeply
- compare sources
- identify patterns
- separate fact from assumption
- synthesize a clear, source-backed narrative

## When to use

Use this skill when the user asks things like:
- “Help me understand the history of X”
- “What decisions led to the current approach for Y?”
- “Research this product area for me”
- “Summarize everything we know about Z”
- “What are the main themes, problems, stakeholders, and decisions around this topic?”
- “Create a briefing on this initiative”

Do not use this skill for:
- simple factual lookup from a single source
- lightweight summaries of one document
- purely external or public research
- tasks that do not require synthesis across multiple internal systems

## Research Principles

### Core goals

Your goal is not just to retrieve documents. Your goal is to create understanding.

A high-quality research output should:
1. Explain the topic clearly for someone starting from zero
2. Summarize the historical evolution of the topic
3. Identify major decisions and choices and why they were made and tradeoffs
4. Understand the strategic importance of decisions 
5. Highlight important teams and artifacts
6. Distinguish current reality from outdated information
7. Surface contradictions, risks, and open questions
8. Back every major claim with evidence from internal sources
 

### Key behaviors

You should:
- search across all likely internal sources, not just one
- prefer breadth first, then depth
- search multiple times, refining based on what you learn
- look for both current-state docs and historical discussion
- compare formal documents with informal discussion
- treat recent and authoritative sources as higher-confidence
- note when information is stale, ambiguous, or conflicting
- explicitly separate facts, interpretations, and hypotheses

You should not:
- assume the first few results are sufficient
- present unverified claims as fact
- ignore older sources that explain why decisions were made
- over-weight chat discussions when official docs contradict them
- over-weight polished docs when execution history suggests otherwise
- invent missing context

## Source Strategy

Search broadly across available internal knowledge systems. Examples include:
- Google Drive
- SharePoint
- Confluence
- Slack
- Jira
- PRDs
- RFCs
- strategy docs
- meeting notes
- design docs
- roadmaps
- decision logs
- tickets
- postmortems
- launch docs
- org updates
- dashboards if available

### What each source is best for

#### Formal docs
Best for:
- official definitions
- strategy
- roadmap
- requirements
- architecture
- decision rationale
- launch plans

Examples:
- PRDs
- RFCs
- design docs
- Confluence pages
- Google Docs
- presentations

#### Chat systems
Best for:
- historical discussion
- disagreement
- decision context
- unresolved questions
- stakeholder opinions
- tactical details
- timeline reconstruction

Examples:
- Slack threads
- chat channels
- meeting follow-up threads

#### Issue trackers
Best for:
- implementation history
- prioritization
- ownership
- execution details
- bugs
- scope change
- open work

Examples:
- Jira tickets
- epics
- linked tasks
- milestone issues

#### Supporting artifacts
Best for:
- metrics context
- post-launch learnings
- operational constraints
- dependency mapping

Examples:
- dashboards
- postmortems
- experiment readouts
- review decks

### Source weighting

When sources disagree, weigh them roughly in this order:
1. Recent official docs owned by responsible teams
2. Explicit decision records and approved plans
3. Recent implementation artifacts and issue history
4. Recent cross-functional discussion from relevant stakeholders
5. Older planning docs
6. Informal discussion without confirmation

Older sources are still valuable for history, but should not be mistaken for current truth.

## Research Workflow

Copy this checklist and track progress:

```text
Research Progress:
- [ ] Step 1: Synthesize the request
- [ ] Step 2: Map likely knowledge repositories
- [ ] Step 3: Run first-pass broad search
- [ ] Step 4: Open and review highest-signal sources
- [ ] Step 5: Synthesize key information, themes, and timeline
- [ ] Step 6: Run second-pass targeted search
- [ ] Step 7: Resolve contradictions and validate claims
- [ ] Step 8: Create structured summary
- [ ] Step 9: Verify citations and confidence
```

### Step 1: Synthesize the request

Clarify the research objective internally before searching.

Determine:
- the exact topic
- the likely scope
- what the user probably wants to understand
- likely related terminology, aliases, project names, team names, and adjacent concepts
- whether the user likely needs history, current state, decision rationale, execution status, or all of these

Write a short internal framing:
- Research topic
- Likely subtopics
- Likely source types
- Likely stakeholders or teams
- Key questions to answer

Example questions:
- What is this area?
- Why was it created?
- How has it changed over time?
- What major decisions shaped it?
- What problems is it trying to solve?
- What is the current state?
- What remains unresolved?

### Step 2: Map likely knowledge repositories

Before reading deeply, identify where the highest-signal information is likely to live.

Create a repository plan:
- official docs and specs
- historical discussions
- tickets and execution history
- decision artifacts
- launch or review materials
- supporting discussions and postmortems

Do not rely on one repository alone.

### Step 3: Run first-pass broad search

Search widely using:
- exact topic name
- alternate names
- abbreviations
- related systems
- team names
- stakeholder names
- adjacent features
- known terminology discovered from the request

Goal of first pass:
- build coverage
- identify major clusters of information
- find canonical docs
- find the earliest and latest references
- identify repeated names, concepts, and decisions

At this stage, prioritize recall over precision.

### Step 4: Open and review highest-signal sources

Review the most relevant documents and discussions in detail.

For each source, capture:
- what it is
- when it was created or discussed
- who authored or influenced it
- what claims it makes
- what decisions it records
- what assumptions it reveals
- whether it appears current or outdated
- how it relates to other sources

Look for:
- repeated themes
- inflection points
- decision moments
- organizational ownership
- conflicts across sources
- language indicating uncertainty or debate

### Step 5: Synthesize key information, themes, and timeline

Once you have reviewed enough sources, synthesize:

#### Core understanding
What is the topic, in simple terms?

#### Timeline
How did this area evolve over time?

#### Major decisions
What were the important decisions, and why were they made?

#### Themes
What patterns appear repeatedly?

#### Current state
What seems true now?

#### Open questions
What still appears unresolved, uncertain, or under-documented?

This step should produce a coherent mental model, not just notes.

### Step 6: Run second-pass targeted search

Use what you learned to search again with better precision.

Search for:
- newly discovered project names
- acronyms
- key people
- specific decisions
- ticket IDs
- launch names
- architecture terms
- competing proposals
- follow-up work
- postmortems
- status updates

This pass should fill gaps and test your emerging understanding.

### Step 7: Resolve contradictions and validate claims

For every important claim:
- verify that a source supports it
- Open GitHub and validate any code claims to see if the claims have code examples that are supported.
- check whether a newer source updates or reverses it
- identify whether the claim is factual, interpretive, or speculative
- note disagreements across sources

When contradictions exist:
- do not hide them
- explain them
- identify which source appears more authoritative and why
- include uncertainty where necessary

### Step 8: Create structured summary

Produce a research report that teaches the user the topic from zero.

Your report should prioritize clarity, structure, and synthesis over exhaustiveness.

### Step 9: Verify citations and confidence

Before finishing:
- ensure every major claim is source-backed
- ensure citations map cleanly to the correct claims
- remove unsupported statements
- note confidence level where evidence is weak or conflicting

## Output Format

Use this structure unless the user asks for a different format.

### Internal Research Report: [Topic]

#### 1. Executive Summary
A concise explanation of the topic, why it matters, and the most important findings.

#### 2. What This Is
Explain the area in plain language for someone unfamiliar with it.

#### 3. Why It Exists
Summarize the original problem, business need, or organizational context.

#### 4. Historical Evolution
Provide a timeline of key moments, including:
- origin
- major decisions
- launches or pivots
- ownership changes
- important incidents or lessons

#### 5. Key Decisions and Tradeoffs
For each major decision, summarize:
- what was decided
- why
- alternatives considered if known
- tradeoffs or consequences

#### 6. Current State
Describe:
- how the area works today
- who owns it
- current goals or constraints
- what seems stable versus in flux

#### 7. Key Themes and Insights
Summarize repeated patterns, such as:
- recurring problems
- strategic tensions
- operational pain points
- alignment or misalignment across teams
- known dependencies

#### 8. Open Questions and Risks
List unresolved issues, missing clarity, or risky assumptions.

#### 9. Important Sources
List the most important documents, threads, tickets, or artifacts reviewed.

#### 10. Confidence and Gaps
State:
- what is well supported
- where evidence is mixed
- what remains unclear due to missing or conflicting sources

## Citation Rules

Every major claim should be grounded in source material.

### Citation expectations
- Cite concrete source artifacts, not vague repository names
- Prefer citing the most authoritative source available
- If a claim is supported by multiple sources, use the strongest one or cite multiple if useful
- When citing a timeline or decision, prefer the source closest to the event plus any later confirming source
- If citing Slack or chat, explain whether it reflects a decision, a proposal, or discussion only

### Evidence labels

When useful, label information as:
- **Fact**: directly supported by source material
- **Inference**: reasonable conclusion drawn from multiple sources
- **Unverified**: mentioned but not sufficiently confirmed
- **Conflicting**: sources disagree

Do not present inference as fact.

## Quality Bar

A strong report should:
- teach the user the topic from zero
- capture both history and current state
- explain why major decisions happened
- identify key players and artifacts
- connect scattered knowledge into one coherent narrative
- be specific, not generic
- be well-cited
- be honest about uncertainty

A weak report:
- is just a list of documents
- summarizes sources one by one without synthesis
- ignores historical context
- ignores contradictions
- lacks citations
- overstates confidence

## Heuristics for Better Research

### Look for canonical artifacts
When available, identify:
- main PRD or spec
- decision doc or RFC
- implementation ticket or epic
- launch document
- postmortem or review
- active owner or team

### Reconstruct history
Good internal research often requires stitching together:
- earliest proposal
- review or debate
- implementation work
- launch or rollout
- follow-up issues
- current-state maintenance or redesign

### Watch for stale information
A polished doc may be outdated. A Slack thread may be newer but less authoritative.
Always ask:
- Is this still true?
- Was this proposal ever implemented?
- Did a later source supersede this?

### Look for language that matters
Pay attention to phrases like:
- “we decided”
- “proposal”
- “deprecated”
- “current approach”
- “for launch”
- “temporary workaround”
- “next phase”
- “blocked on”
- “follow-up”
- “not aligned”
- “revisit later”

These often signal decision points or unresolved issues.

## Example User Requests

- Research the history and current state of our recommendations system
- Help me understand everything important about account linking
- Create an internal briefing on our seller onboarding flow
- Summarize the history of the payments platform and major architectural decisions
- What should a new PM know about experimentation infrastructure?

## Final Instructions

When using this skill:
1. Search broadly first
2. Read deeply second
3. Synthesize across sources
4. Search again based on what you learned
5. Validate every major claim
6. Produce a report that is clear, historical, practical, and evidence-backed

The goal is not to collect documents. The goal is to create understanding.
