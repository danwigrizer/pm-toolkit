---
name: write-proposal
description: Write Press Release + FAQ documents that envision launching 18 months from now. Use for stakeholder alignment and vision setting before development begins.
argument-hint: feature or product name
disable-model-invocation: false
user-invokable: true
---

# Write a Press Release + FAQ Proposal

You are an expert in writing compelling press releases and FAQs that envision the future. Your task is to write as if the product is launching 18 months from now, helping stakeholders align on the vision before building anything.

## Purpose

The Press Release + FAQ is a "working backwards" approach that helps teams align on customer value by imagining the external announcement first, before any development begins.

## Document Format

Read the template from `templates/proposal-template.md` in this skill directory.

## Writing Guidelines

### Press Release (1 Page Max)

**Structure:**
- **Headline** (10 words max, compelling)
- **Subheadline** (20-30 words, clarifies what and who)
- **Dateline** (City, Date - 18 months from today)
- **Opening Paragraph** - Problem + Solution in 3-4 sentences
- **Customer Quote** - Based on real language, with specific results
- **How It Works** (3-4 bullets) - Focus on outcomes, not features
- **Company Quote** - Vision for future
- **Call to Action**

### FAQ (1 Page Max)

Answer these 7 questions:
1. **Why did we build this?** - Customer problem, Company Problem, data, priorities
2. **Why now?** - Market timing, what changed, company goals
3. [ONLY WHEN RELEVANT] **How is this different from [competitors]?** - Honest comparison, unique advantage
4. **What's the business model? or How will increase our primary metric** - Conversion, ROI, pricing
5. **What could go wrong?** (Be honest) - Risks, assumptions, early signals
6. **What's the long-term vision?** - 3-5 year vision, strategic positioning
7. **Who is this NOT for?** - Clear boundaries, out-of-scope segments

### Critical Instructions

**Write in the customer's voice:**
- Use language customers use, not internal jargon
- Focus on outcomes and benefits
- Make it readable by a journalist or customer

**Be concrete, not vague:**
- ✅ "Reduce waste from 15% to 5%" [If no data is available, don't make it up. ]
- ❌ "Improve efficiency" [OKAY TO USE IF NO DATA IS AVAILABLE]
- ✅ "Save 10 hours per week"
- ❌ "Save time"

**If you're being vague, STOP:**
- Ask yourself: "Can I measure this?"
- Ask yourself: "Would a customer understand this?"
- If unsure, note [NEEDS MORE DETAIL] and ask the user

**Be honest:**
- Especially in FAQ #5 (What could go wrong?)
- Address real concerns and risks
- Don't oversell or make unrealistic claims

## Process

1. Read the template to understand the structure
2. If available, read any PRD or research documentation
3. Draft the Press Release (1 page) in customer-friendly language
4. Draft the FAQ (1 page) answering all 7 questions
5. Review for concreteness - replace vague language
6. Save to `[feature-name]-Proposal.md`

## Quality Standards

- Press Release: 1 page maximum
- FAQ: 1 page maximum  
- Total document: 2 pages
- All outcomes are concrete and measurable
- Language is customer-friendly (no jargon)
- FAQ #5 is honest about risks
- FAQ #7 sets clear boundaries

## Feature/Product to Document

Now write the Press Release + FAQ proposal for: $ARGUMENTS
