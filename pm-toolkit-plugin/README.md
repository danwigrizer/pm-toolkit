# PM Toolkit Plugin for Claude Code

A comprehensive Product Manager toolkit for Claude Code featuring opinionated, deterministic PRD writing, codebase analysis, flow diagramming, press release proposals, and ticket generation — coordinated by a team of specialized agents.

---

## Features

### 🤖 Specialized Agents

| Agent | Role |
|---|---|
| `prd-writer` | Writes all product sections of PRDs: D-Sections, routing logic, user flows, acceptance criteria |
| `prd-code-explorer` | Analyzes the codebase to extract current user flows, business rules, and routing logic |
| `flow-mapper` | Creates Mermaid flowcharts, sequence diagrams, state diagrams, and bracketed text flows |
| `technical-writer` | Writes technical sections of PRDs: architecture, APIs, data models, performance, security |
| `research-agent` | Provides curated market context, competitor examples, and best practices (max 3 each) |
| `proposal-writer` | Writes future-looking Press Release + FAQ proposals |
| `ticket-writer` | Breaks PRDs into actionable engineering tickets |
| `reviewer-agent` | Reviews all documents for quality and consistency |
| `strategy-writer` | Writes product strategies (NOT roadmaps) using Casey Winters & Reforge frameworks |

### 🛠️ Skills (Slash Commands)

| Skill | Command | Description |
|---|---|---|
| PRD Workflow | `/prd-workflow` | End-to-end PRD pipeline: optional code analysis → flow mapping → full PRD |
| Full PM Cycle | `/pm-full-cycle` | Complete documentation package: research + PRD + proposal + tickets + review |
| Write PRD | `/write-prd` | Write a complete PRD via the prd-writer agent |
| Analyze Current State | `/analyze-current-state` | Analyze how a feature works today via the prd-code-explorer agent |
| Create Flows | `/create-flows` | Create flow diagrams via the flow-mapper agent |
| Write Proposal | `/write-proposal` | Write a Press Release + FAQ proposal |
| Write Ticket | `/write-ticket` | Write a prescriptive engineering ticket |
| Write Strategy | `/write-strategy` | Write a product strategy (not a roadmap) using Casey Winters & Reforge frameworks |

---

## PRD Format

PRDs produced by this toolkit follow an opinionated, immediately executable format.

### Section Structure

1. **Executive Summary** — 2–4 sentence overview
2. **Problem Statement** — current state, friction, measurable impact
3. **Goals & Success Metrics** — primary, secondary, and leading indicators
4. **User Stories & Requirements** — the core of the PRD, broken into:
   - **4a. Desired Future State** — declarative description of "good"
   - **4b. User Flows** — Mermaid flowcharts, sequence diagrams, or bracketed text
   - **4c. Routing & Business Logic** — deterministic `Send to [X] if:` rules
   - **4d. D-Sections** — per-page/component specs (see below)
5. **Solution Overview** — key features and phasing strategy
6. **Timeline & Phasing** — milestones with `[MVP]` / `[Future]` tags
7. **Dependencies & Blockers** — product-level only
8. **Risks & Mitigation** — product risks
9. **Non-Goals** — explicit `[Out of Scope]` items
10. **Success Criteria (Post-Launch)** — launch checklist and evaluation criteria
11. **Key Decision Points** — open questions with Option A / B / Recommendation
12. *Technical sections added separately by `technical-writer`*

### D-Section Format

Each page or component specification includes, in order:

- **Title** — `Page [N]: [Name]` or `Component: [Name]`
- **Purpose** — one sentence starting "Allow users to…"
- **User Actions** — verb-first bullets
- **User Stories** — `As a [specific user type], when [surface], I want [goal], so that [benefit].`
- **Requirements** — grouped into three subsections:
  - *Front End* — per-component with numbered states (default, active, error, disabled), animations, responsive rules, exact constraints
  - *Back End* — `System must…` / `When [condition], system…` with edge cases and timing
  - *Data / Analytics* — `Track "[event]" when [trigger].` with attribute lists
- **Acceptance Criteria** — numbered binary pass/fail conditions starting with "User can…" or "System should…"
- **Logic** — deterministic routing rules
- **D-Section Quality Checklist**

---

## Installation

This toolkit installs as **standalone Claude Code configuration** — copy `agents/` and `skills/` into your Claude config folder. No marketplace or plugin system required. Skills become available immediately as `/write-prd`, `/pm-full-cycle`, etc.

### Option 1: User-Level (Personal Use)

Available across all your projects:

```bash
mkdir -p ~/.claude/agents ~/.claude/skills
cp /path/to/pm-toolkit-plugin/agents/*.md ~/.claude/agents/
cp -r /path/to/pm-toolkit-plugin/skills/* ~/.claude/skills/
```

### Option 2: Project-Level (Team Sharing)

Commit to your repo so the whole team gets it on `git pull`:

```bash
mkdir -p .claude/agents .claude/skills
cp /path/to/pm-toolkit-plugin/agents/*.md .claude/agents/
cp -r /path/to/pm-toolkit-plugin/skills/* .claude/skills/

git add .claude/agents .claude/skills
git commit -m "Add PM toolkit agents and skills"
```

Restart Claude Code after installing. See [SETUP.md](SETUP.md) for full instructions including agent teams setup.

---

## Usage

### `/prd-workflow` — PRD Only Pipeline

The focused PRD creation workflow. Lighter than `/pm-full-cycle` — produces a complete PRD with optional current state analysis and flow diagrams.

```bash
/prd-workflow Seller Payout Method Setup
```

**What it does:**
1. Asks if an existing implementation exists — if yes, runs `prd-code-explorer` to extract current flows, routing logic, and edge cases
2. Runs `flow-mapper` to produce current state and future state flow diagrams
3. Passes all findings to `prd-writer` to produce a complete grounded PRD
4. Confirms output and highlights Key Decision Points

**Best for:** Feature PRDs where you want the codebase analysis + flow diagrams + full spec in one go, without proposal or tickets.

---

### `/pm-full-cycle` — Complete Documentation Package

Orchestrates up to 8 specialized agents to deliver research, PRD, proposal, and tickets.

```bash
/pm-full-cycle Real-time Collaboration Feature
```

**Phase 0 (optional):** Asks if an existing implementation exists. If yes, spawns `prd-code-explorer` + `flow-mapper` to ground the PRD in real behavior before writing begins.

**Agent execution order:**
1. *(Optional)* `prd-code-explorer` — analyzes current codebase
2. *(Optional)* `flow-mapper` — maps current state flows
3. `research-agent` — curated market context (max 3 examples, 3 best practices)
4. `prd-writer` — product sections informed by research + current state findings
5. `technical-writer` — technical sections (runs after prd-writer)
6. `proposal-writer` — Press Release + FAQ (runs in parallel with technical-writer)
7. `ticket-writer` — implementation tickets (runs after PRD is complete)
8. `reviewer-agent` — validates all outputs

**Output:**
```
research/[feature-name]-current-state.md   # Current codebase analysis (if applicable)
research/[feature-name]-research.md        # Market research and best practices
[feature-name]-PRD.md                      # Full PRD (product + technical + embedded flows)
[feature-name]-Proposal.md                 # Press Release + FAQ (2 pages)
tickets/[feature-name]-*.md               # Implementation tickets
[feature-name]-SUMMARY.md                 # Executive summary
```

---

### `/write-prd` — Write a PRD

Invokes the `prd-writer` agent directly to produce a complete PRD.

```bash
/write-prd Guest Checkout to Account Conversion Flow
```

Gathers context if the feature description is vague, then produces all 11 product sections plus technical section placeholders. Saves to a file path if specified.

---

### `/analyze-current-state` — Analyze Existing Code

Invokes the `prd-code-explorer` agent to extract current behavior from the codebase.

```bash
/analyze-current-state checkout payment step — src/checkout/payment/
```

**Output includes:**
- Current user flows in bracket notation
- Current user-facing states and UX per condition
- Business rules and routing logic in `Send to [X] if:` format
- Edge cases and fallbacks
- Notes mapping findings to PRD sections (Problem Statement, §4c, §4d, §11)

---

### `/create-flows` — Create Flow Diagrams

Invokes the `flow-mapper` agent to produce diagrams for embedding in PRD section 4b.

```bash
/create-flows Seller Payout Setup — future state — flowchart
```

Supports: `flowchart`, `sequence`, `state`, `text`. Auto-selects format if not specified. Can produce current state, future state, or a comparison with delta summary.

---

### `/write-proposal` — Write a Press Release + FAQ

```bash
/write-proposal AI-Powered Product Recommendations
```

Produces a 2-page document (1-page press release + 1-page FAQ) written as if launching 18 months from now. Uses concrete, measurable outcomes. FAQ covers: Why we built it, Why now, How it drives metrics, Risks, Long-term vision, and Who it's NOT for.

---

### `/write-ticket` — Write an Engineering Ticket

```bash
/write-ticket Payment Method Selection — add pre-selection of last-used method
```

Produces a prescriptive ticket matching the PRD's requirements format:

- **Summary** — 1–2 sentences: "Implement a [component] that [benefit]"
- **Problem / Opportunity** — problem + primary metric (Conversion or Retention) + causal link
- **User Stories** — specific surface + user type + goal + benefit
- **Product Requirements** — grouped into Front End / Back End / Analytics with numbered component behaviors, exact constraints, and event tracking patterns
- **Acceptance Criteria** — binary pass/fail conditions
- **Experiments Setup** — eligibility, treatment, success metrics (for A/B tests)

---

## Plugin Structure

```
pm-toolkit-plugin/
├── .claude-plugin/
│   └── plugin.json
├── agents/
│   ├── prd-writer-agent.md          # Opinionated PRD writer with D-Sections
│   ├── prd-code-explorer-agent.md   # Codebase analyzer for current behavior
│   ├── flow-mapper-agent.md         # Flow diagram creator and validator
│   ├── technical-writer-agent.md    # Technical sections specialist
│   ├── research-agent.md            # Market research specialist
│   ├── proposal-writer-agent.md     # Press Release + FAQ specialist
│   ├── ticket-writer-agent.md       # Engineering ticket specialist
│   └── reviewer-agent.md            # Quality reviewer
├── skills/
│   ├── prd-workflow/
│   │   └── SKILL.md                 # PRD-only pipeline (3 agents)
│   ├── pm-full-cycle/
│   │   └── SKILL.md                 # Full cycle orchestrator (up to 8 agents)
│   ├── write-prd/
│   │   ├── SKILL.md
│   │   └── templates/prd-template.md
│   ├── analyze-current-state/
│   │   └── SKILL.md
│   ├── create-flows/
│   │   └── SKILL.md
│   ├── write-proposal/
│   │   ├── SKILL.md
│   │   └── templates/proposal-template.md
│   └── write-ticket/
│       ├── SKILL.md
│       └── templates/ticket-template.md
└── README.md
```

---

## When to Use What

| Situation | Recommended Skill |
|---|---|
| Existing feature being redesigned — want code analysis + flows + full PRD | `/prd-workflow` |
| Net new feature — just need the PRD | `/write-prd` |
| Need full package: research + PRD + proposal + tickets | `/pm-full-cycle` |
| Just want to understand how something works today | `/analyze-current-state` |
| Need a flow diagram for an existing PRD | `/create-flows` |
| Stakeholder alignment before development | `/write-proposal` |
| Breaking down a PRD into tickets | `/write-ticket` |

---

## Best Practices

### PRD Writing
- **Use `/prd-workflow` when refactoring or changing an existing feature** — the code explorer grounds the Problem Statement and D-Sections in what actually exists, not assumptions
- **D-Sections are the heart of the PRD** — every interactive surface needs a D-Section with Front End states, Back End logic, and Analytics events specified
- **Routing logic must be deterministic** — every routing rule uses `Send to [X] if:` with mutually exclusive conditions
- **Scope tag everything** — `[MVP]`, `[Future]`, and `[Out of Scope]` must be applied consistently across all three requirement subsections

### Ticket Writing
- **Tickets should match PRD D-Sections** — one ticket per D-Section component is a reasonable starting point
- **Never use vague constraints** — "up to 9 digits", "< 200ms p95", "16-character max" not "a number", "fast", "reasonable length"
- **Every interactive element needs all states** — default, active, error, and disabled

### Agent Teams
- **Cost**: Each agent has its own context window — agent team runs use more tokens
- **Quality**: Multiple agents provide better coverage and peer review than a single pass
- **Best for**: Complex, multi-document projects or when you need both product and technical sections

### Research Agent
- Max 3 market examples per research request
- Max 3 best practices per research request
- Every example must connect directly to the current PRD goal ("So What?" rule)
- Does not write requirements — context only

---

## Troubleshooting

### Agent Teams Not Working

```bash
# Verify agent teams are enabled
cat ~/.claude/settings.json
# Should show: {"env": {"CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"}}
```

Restart Claude Code after enabling. Requires Claude Code with agent teams support.

### Skills Not Found

```bash
# Verify plugin installation
ls ~/.claude/plugins/pm-toolkit/skills/
# or for project-level
ls .claude/plugins/pm-toolkit/skills/
```

Check that `plugin.json` is valid JSON. Restart Claude Code.

### Agents Not Being Invoked Correctly

Agent files use `allowed-tools` and `model` in frontmatter — these are agent-specific fields.
Skill files do **not** support `allowed-tools` or `model` — skills use only: `name`, `description`, `argument-hint`, `disable-model-invocation`, `user-invokable`, `compatibility`, `license`, `metadata`.

---

## Customization

### Modify Agent Behavior

Edit agent files in `agents/` to adjust:
- Allowed tools (`allowed-tools`)
- Model selection (`model: opus` or `model: sonnet`)
- Section ownership or writing rules

### Add Examples

Place example PRDs, tickets, or proposals in each skill's `examples/` directory to guide Claude's output style.

---

Built for Product Managers using Claude Code.
