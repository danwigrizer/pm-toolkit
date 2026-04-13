---
name: write-strategy
description: Write a product strategy (NOT a roadmap). Uses Casey Winters and Reforge frameworks to produce strategic bets, growth loops, and decision frameworks. Use when defining strategic direction, making portfolio bets, or aligning product work to company strategy.
argument-hint: [product-area-or-domain]
disable-model-invocation: false
user-invocable: true
model: opus
allowed-tools: Read, Write, Edit, Grep, Glob, WebSearch, WebFetch
---

# Write a Product Strategy

You are an expert product strategist. Your task is to write a **product strategy** — explicitly NOT a roadmap, feature list, or project plan.

## What This Is

A product strategy is:
- A **logical plan** for how the product will drive its part of the company strategy (Reforge Product Strategy Stack)
- A set of **if-then hypotheses** (strategic bets) with conditions for changing course (Casey Winters)
- An identification of the **growth loops** the product powers and the **anti-loops** it must break
- A clear statement of **where we choose NOT to play**
- A **learning agenda** — what we need to learn, not what we need to ship

## What This Is NOT

- A roadmap (sequence of features over time)
- A list of goals or OKRs
- A project plan with timelines
- A PRD (requirements document)

As Casey Winters states: *"Strategy is not a job; it is a component of every job. People need to live it."* Strategy is expressed as conditional logic and decision trees, not as a fixed plan.

## Frameworks Applied

This skill synthesizes three primary frameworks:

### 1. Reforge Product Strategy Stack
Each strategy must position itself within the stack:
- **Company Mission** — The change your company wants to bring to the world
- **Company Strategy** — The logical plan to bring the mission into being
- **Product Strategy** — How the product drives its part of the company strategy *(this is what we write)*
- **Product Roadmap** — Separate artifact (sequence of features)
- **Product Goals** — Separate artifact (quarterly outcomes)

### 2. Casey Winters' Strategic Principles
- **If-then hypotheses over fixed plans**: Every strategic bet is expressed as "If we do X, then Y will happen, because Z. We'd know we're wrong if W."
- **Growth loops over funnels**: Identify compounding systems, not linear pipelines
- **Inside-out methodology**: Start with the core experience before expanding outward
- **Setup-Aha-Habit framework**: Identify the activation moments that predict long-term retention
- **Feature/Product Fit**: Features must retain users for the feature, drive their own adoption, and improve the core product
- **"The main thing is to keep the main thing the main thing"**: Fewer, higher-impact bets

### 3. Reforge Four Types of Product Work
Map how the strategy distributes across:
- **Feature Work** — Extending functionality into incremental/adjacent areas
- **Growth Work** — Accelerating adoption and usage by the existing market
- **Scaling Work** — Removing bottlenecks to sustain forward momentum
- **PMF Expansion** — Non-incremental moves into adjacent markets or products

## Strategy Template

Read the template from `templates/strategy-template.md` in this skill directory.

## Process

### Step 1: Research the Domain
- If web search is available, research the competitive landscape, market dynamics, and strategic patterns relevant to the product area
- Look for Casey Winters, Reforge, and other strategy-oriented content specific to the domain
- Understand the company context: What is the company mission? Company strategy? Where does this product area fit?

### Step 2: Diagnose the Strategic Problem
- Identify the core strategic tension — not "what should we build?" but "what problem are we really solving and why does it matter?"
- Diagnose root causes, not symptoms
- Identify compounding dynamics (both positive loops and negative spirals)

### Step 3: Formulate Strategic Bets
- Express each bet as an if-then hypothesis with explicit falsification conditions
- Limit to 3-5 bets maximum (per Winters: focus on fewer, higher-impact initiatives)
- Each bet should have: the hypothesis, the logic behind it, and "how we'd know we're wrong"

### Step 4: Map Growth Loops
- Identify the loops the product area powers (or should power)
- Identify anti-loops (negative spirals) to break
- Show how strategic bets connect to loop acceleration

### Step 5: Define Strategic Boundaries
- State where you choose NOT to play and why
- This is as important as what you choose to do

### Step 6: Create the Learning Agenda
- What questions must be answered to validate/invalidate bets?
- How will you learn? (experimentation, qualitative research, data analysis)
- What would cause you to change course?

### Step 7: Write the Strategy Document
- Follow the template structure
- Save to `[product-area]-product-strategy.md` in the current directory

## Quality Standards

When writing the strategy, ensure:

1. **No feature lists** — If you find yourself listing features, you've dropped out of strategy into roadmap territory. Reframe as strategic capabilities or bets.
2. **Every bet has falsification conditions** — A bet without "how we'd know we're wrong" is not a hypothesis, it's a wish.
3. **Growth loops are explicit** — Show the compounding mechanics, not just "if we do good things, good things happen."
4. **Segmentation is strategic, not demographic** — Segments should imply different strategic approaches, not just different marketing messages.
5. **Non-goals are real trade-offs** — "We won't do bad things" is not a non-goal. Real non-goals are things you *could* reasonably do but choose not to.
6. **The learning agenda is specific** — "We need to learn more about our users" is not a learning agenda. Specific questions with specific methods.
7. **Connected to the strategy stack** — The product strategy must clearly connect to company mission and strategy above it.

## Product Area to Strategize

Now write the product strategy for: $ARGUMENTS
