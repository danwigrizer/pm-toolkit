# PM Toolkit — Setup Guide

This toolkit works as **standalone Claude Code configuration** — no marketplace or plugin system required. You copy the `agents/` and `skills/` directories into your Claude config folder and skills become available immediately as `/write-prd`, `/pm-full-cycle`, etc.

---

## Prerequisites

- Claude Code installed and authenticated
- Claude Code version 1.0.33 or later (`claude --version` to check)
- Claude Opus 4.6+ (required for agent teams — used by `/pm-full-cycle` and `/prd-workflow`)

---

## Step 1: Enable Agent Teams

Agent teams are experimental and disabled by default. Required for `/pm-full-cycle` and `/prd-workflow`.

```bash
mkdir -p ~/.claude
cat > ~/.claude/settings.json << 'EOF'
{
  "env": {
    "CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"
  }
}
EOF
```

Restart Claude Code after saving.

---

## Step 2: Install

Choose user-level (available in all projects) or project-level (committed to a specific repo).

### Option A: User-Level (Personal Use)

Copies agents and skills into `~/.claude/` so they are available in every project:

```bash
# Create directories if they don't exist
mkdir -p ~/.claude/agents ~/.claude/skills

# Copy agents
cp /path/to/pm-toolkit-plugin/agents/*.md ~/.claude/agents/

# Copy skills
cp -r /path/to/pm-toolkit-plugin/skills/* ~/.claude/skills/
```

Restart Claude Code. Skills will be available in any project.

### Option B: Project-Level (Team Sharing)

Copies into a project's `.claude/` directory so the whole team gets the toolkit when they pull:

```bash
# Navigate to your project root
cd /path/to/your/project

# Create directories
mkdir -p .claude/agents .claude/skills

# Copy agents
cp /path/to/pm-toolkit-plugin/agents/*.md .claude/agents/

# Copy skills
cp -r /path/to/pm-toolkit-plugin/skills/* .claude/skills/

# Commit to version control
git add .claude/agents .claude/skills
git commit -m "Add PM toolkit agents and skills"
git push
```

Team members get the toolkit automatically when they pull.

---

## Step 3: Verify

Start Claude Code and run a quick test:

```
/write-prd Test Feature
```

If Claude responds with PRD sections, the toolkit is working.

Then test agent teams:

```
/pm-full-cycle Test Feature
```

You should see a task list created, agents spawned, and output files generated.

---

## Verification Checklist

- [ ] Agent teams flag is set in `~/.claude/settings.json`
- [ ] Agent files exist in `~/.claude/agents/` or `.claude/agents/`
- [ ] Skill directories exist in `~/.claude/skills/` or `.claude/skills/`
- [ ] `/write-prd` responds (single-agent, no teams required)
- [ ] `/write-ticket` responds
- [ ] `/write-proposal` responds
- [ ] `/analyze-current-state` responds
- [ ] `/create-flows` responds
- [ ] `/prd-workflow` spawns agents (requires agent teams)
- [ ] `/pm-full-cycle` spawns multiple agents (requires agent teams)

---

## What's Installed

### 8 Agents (`agents/`)

| File | Agent | Role |
|---|---|---|
| `prd-writer-agent.md` | `prd-writer` | Writes product PRD sections: D-Sections, routing logic, user flows, acceptance criteria |
| `prd-code-explorer-agent.md` | `prd-code-explorer` | Analyzes codebase to extract current flows, business rules, routing logic |
| `flow-mapper-agent.md` | `flow-mapper` | Creates Mermaid flowcharts, sequence diagrams, state diagrams, bracketed text flows |
| `technical-writer-agent.md` | `technical-writer` | Writes technical PRD sections: architecture, APIs, data models, performance, security |
| `research-agent.md` | `research-agent` | Curated market context and best practices (max 3 each) |
| `proposal-writer-agent.md` | `proposal-writer` | Writes Press Release + FAQ proposals |
| `ticket-writer-agent.md` | `ticket-writer` | Breaks PRDs into actionable engineering tickets |
| `reviewer-agent.md` | `reviewer-agent` | Reviews documents for quality and consistency |

### 7 Skills (`skills/`)

| Command | Skill Directory | Description |
|---|---|---|
| `/prd-workflow` | `prd-workflow/` | PRD pipeline: optional code analysis → flow mapping → full PRD |
| `/pm-full-cycle` | `pm-full-cycle/` | Full package: research + PRD + proposal + tickets + review |
| `/write-prd` | `write-prd/` | Write a complete PRD |
| `/analyze-current-state` | `analyze-current-state/` | Analyze how a feature works today |
| `/create-flows` | `create-flows/` | Generate flow diagrams |
| `/write-proposal` | `write-proposal/` | Write a Press Release + FAQ |
| `/write-ticket` | `write-ticket/` | Write a prescriptive engineering ticket |

---

## Quickstart

### Single-agent skills (no agent teams required)

```
/write-prd Guest Checkout to Account Conversion Flow
```

```
/write-ticket Payment Method Selection — add pre-selection of last-used method
```

```
/write-proposal AI-Powered Product Recommendations
```

```
/analyze-current-state checkout payment step — src/checkout/payment/
```

```
/create-flows Seller Payout Setup — future state — flowchart
```

### Multi-agent pipelines (requires agent teams)

```
/prd-workflow Seller Payout Method Setup
```

```
/pm-full-cycle Real-time Collaboration Feature
```

---

## Troubleshooting

### Skills not recognized

**Check that skill directories were copied correctly:**

```bash
# User-level
ls ~/.claude/skills/
# Should see: analyze-current-state  create-flows  pm-full-cycle  prd-workflow  write-prd  write-proposal  write-ticket

# Project-level
ls .claude/skills/
```

Each skill directory must contain a `SKILL.md` file:

```bash
ls ~/.claude/skills/write-prd/
# Should see: SKILL.md  templates/
```

Restart Claude Code after copying files.

### Agents not found by skills

Check that agent `.md` files are in the right directory:

```bash
# User-level
ls ~/.claude/agents/
# Should see 8 .md files

# Project-level
ls .claude/agents/
```

If you installed at project-level and agents are at user-level (or vice versa), skills may not find them. Install both agents and skills at the same scope.

### Agent teams not spawning

```bash
cat ~/.claude/settings.json
# Should contain: {"env": {"CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"}}
```

If missing:
```bash
echo '{"env": {"CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"}}' > ~/.claude/settings.json
```

Restart Claude Code.

### Skill frontmatter errors

If you've customized a `SKILL.md` file, skill frontmatter only supports these fields:

```
name, description, argument-hint, disable-model-invocation, user-invokable
```

Do NOT add `allowed-tools` or `model` to skill frontmatter — those fields are only valid in agent files.

---

## Customization

### Modify an agent

Open the agent file and edit the system prompt or `allowed-tools`:

```bash
# User-level
nano ~/.claude/agents/prd-writer-agent.md

# Project-level
nano .claude/agents/prd-writer-agent.md
```

Key frontmatter fields in agent files:
- `model: opus` or `model: sonnet` — controls which model the agent uses
- `allowed-tools` — restricts which tools the agent can call

### Add examples

Add example PRDs, tickets, or proposals to guide output style:

```bash
mkdir -p ~/.claude/skills/write-prd/examples/
cp your-example-prd.md ~/.claude/skills/write-prd/examples/
```

---

## Team Onboarding Script

Save as `setup-pm-toolkit.sh` in your repo and share with your team:

```bash
#!/bin/bash
# setup-pm-toolkit.sh — Install PM Toolkit agents and skills

set -e

SCRIPT_DIR="$(cd "$(dirname "$0")" && pwd)"
TOOLKIT_DIR="${SCRIPT_DIR}/.claude"

echo "Setting up PM Toolkit..."

# Enable agent teams
mkdir -p ~/.claude
if [ -f ~/.claude/settings.json ]; then
    echo "settings.json already exists — manually ensure CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS=1 is set"
else
    echo '{"env": {"CLAUDE_CODE_EXPERIMENTAL_AGENT_TEAMS": "1"}}' > ~/.claude/settings.json
    echo "Agent teams enabled"
fi

# Verify toolkit files are present (project-level)
if [ -d ".claude/agents" ] && [ -d ".claude/skills" ]; then
    echo "PM Toolkit installed at .claude/agents and .claude/skills"
    echo ""
    echo "Restart Claude Code, then try:"
    echo "  /write-prd Test Feature"
    echo "  /pm-full-cycle Test Feature"
else
    echo "ERROR: .claude/agents or .claude/skills not found."
    echo "Ensure you have pulled the latest from the repo."
    exit 1
fi
```

---

## Notes on the Plugin Format

This toolkit includes a `.claude-plugin/plugin.json` file. This is for future **marketplace distribution** — it is not used by the standalone config install described above and can be ignored for local use.

If you later want to publish this to a Claude Code marketplace, the plugin format is already prepared.

---

## Support

- Toolkit README: `pm-toolkit-plugin/README.md`
- Claude Code Plugins docs: https://code.claude.com/docs/en/plugins
- Issues: https://github.com/anthropics/claude-code/issues
