---
name: prd
license: MIT
---

# /prd — Product Requirements Document

Co-author, review, or edit PRDs with the rigour of a prolific product leader — grounded in Propsoch's context, Ravi's thinking style, and startup pragmatism.

## Model Routing

**This skill uses Opus for product thinking.**

- **Context gathering** (Linear issues, Drive docs, codebase): Run in current session (Sonnet)
- **PRD drafting / review / critique**: Spawn a Task sub-agent with `model: "opus"`
  - Opus handles: formula decomposition, user journey emotional mapping, edge case identification, technical spec depth, quality scoring
  - For `/prd review`: Opus scores, critiques, and suggests specific rewrites
  - For `/prd new`: Opus drafts the full PRD after Sonnet gathers context

```
Task(
  subagent_type: "general-purpose",
  model: "opus",
  prompt: "You are TARS, acting as a senior product leader reviewing/writing a PRD.
    Context: [Propsoch overview, team structure, codebase architecture, Linear data]
    [For review: paste the PRD content + scoring rubric]
    [For new: paste feature description + gathered context + Ravi's answers]
    Apply the Propsoch PRD Framework. Score honestly. Write specific copy, not placeholders.
    Calibrate feedback to the author's level."
)
```

## Usage
```
/prd new [feature]              # Co-author a new PRD
/prd review [Google Doc ID]     # Review a team member's PRD
/prd edit [Google Doc ID]       # Edit/strengthen an existing PRD
/prd template                   # Show the Propsoch PRD framework
```

---

## The Propsoch PRD Framework

This isn't a template to fill in. It's a thinking cascade — each section forces the next. Skip sections consciously, never accidentally.

### 1. Problem & Objective
- **What problem are we solving?** State it in one line. If you can't, you don't understand it yet.
- **Who has this problem?** Name the personas — both customer-facing (GHB members, leads, visitors) AND internal (CSPs, SMEs, MAs, researchers).
- **Why now?** What changed — volume, complaints, revenue impact, strategic shift?
- **Objective:** One sentence. What does success look like at the highest level?
- **Constraints:** What limits the solution space? (capacity, tech debt, timelines, team bandwidth, regulatory)

### 2. The Formula
Decompose the objective into a mathematical formula or causal chain.
- Example: "Members = Qualified Leads × Conversion Rate"
- Example: "Advisor capacity = Deals per CSP × (Available hours - Follow-up hours)"
- This forces clarity on which lever this feature actually pulls.

### 3. Current State & Root Causes
- **How does this work today?** Describe the current system, workflow, or absence thereof.
- **What's broken and why?** Quantify with real numbers — not "it's slow" but "CSPs spend ~1.5-2.5 hrs/day on follow-ups."
- **Root cause chain:** Keep asking "why?" until you hit the structural reason. "Tasks are missed" → "No system enforces ownership" → "We rely on human memory across WhatsApp, Slack, and calls."

### 4. Business Impact
Before vs After analysis with conservative estimates:
- Time saved (hrs/week or month)
- Revenue at risk or recovered (₹ per deal × deals affected)
- Capacity unlocked (% of advisor bandwidth freed)
- Customer experience impact (CSAT, NPS, drop-off reduction)
- Show your math. Ranges are fine (₹1.5-8L/month) — precision theater is worse than honest estimates.

### 5. Goals & Non-Goals
**Goals** — What this feature MUST achieve. Numbered, specific, measurable.
**Non-Goals** — What this feature explicitly will NOT do. This is just as important — it prevents scope creep and sets expectations.

### 6. User Journeys & Emotional States
For each persona affected:
- Walk through their journey step by step
- At each step: What are they doing? What are they feeling? (Anxious, Overwhelmed, Confused, Hopeful, Frustrated)
- What are their deepest fears at this stage?
- What questions keep them up at night?
- What would make this step feel magical vs mediocre?

This applies to internal personas too. A CSP using a new tool has emotions — confusion, skepticism, relief.

### 7. Solution Design
**Approach:** What are we building? High-level description.
**Tradeoffs considered:** What alternatives were evaluated? Why were they rejected? (Build vs buy, scope A vs scope B, now vs later)

For each feature/component:
- **Logic & State Machine:** Entry conditions, exit conditions, transitions, edge cases. When does X trigger Y? What happens when Z fails?
- **UI Copy & CTAs:** Specify the actual text users will see. Not "a button" — write "Book Site Visit →" with the exact copy, empty states, error messages, confirmations.
- **Conditional Display:** What shows/hides based on state? What changes between segments?
- **Data Requirements:** What data does this need? Where does it come from? What's the schema?

### 8. Technical Specifications
Written for engineers, not PMs:
- API endpoints needed (with request/response shapes)
- Data model changes (new tables, columns, relationships)
- Dependencies on existing systems (CRM, comms, Angelo, payment)
- Performance requirements (latency, throughput)
- Migration or backward compatibility needs

### 9. Metrics & Tracking
- **North Star Metric:** One metric that tells you if this worked.
- **Leading indicators:** Metrics that predict success before the NSM moves.
- **Guardrail metrics:** Metrics that should NOT degrade (e.g., conversion rate while adding a new step).
- **Tracking plan:** What events need to be fired in Mixpanel? What dimensions?

### 10. Launch Plan
- **Phasing:** What ships in V1 vs V2 vs Future? Be explicit.
- **Rollout:** Internal dogfood → Bangalore subset → Full rollout? Feature flag?
- **Go/No-Go criteria:** What must be true before launch?
- **Rollback plan:** If it breaks, how do we revert?

### 11. Risks & Open Questions
- **Risks:** What could go wrong? Adoption failure, data quality, performance, edge cases. For each: likelihood, impact, mitigation.
- **Open Questions:** What don't we know yet? Who needs to answer it? By when? These are NOT weaknesses — they're signs of intellectual honesty.

### 12. Appendix
- Wireframes or mockups (link to Figma)
- Research data or customer quotes
- Competitive reference
- Changelog (date + what changed + why)

---

## Quality Scoring Rubric (for /prd review)

Score each dimension 1-10. Present as a table.

| Dimension | What 1 looks like | What 10 looks like |
|-----------|-------------------|---------------------|
| **Problem Clarity** | Vague or absent | One-line problem + quantified pain + clear "why now" |
| **Formula / Decomposition** | No analytical framing | Objective decomposed into measurable formula |
| **Root Cause Depth** | Symptoms listed | 3-level "why" chain with real numbers |
| **Business Case** | No impact estimate | Before/After with revenue math, time savings, capacity |
| **User Empathy** | No personas or journeys | Dual-persona journeys with emotional states tracked |
| **Specification Depth** | Feature names only | State machines, UI copy, conditional logic, edge cases |
| **Technical Clarity** | No technical detail | APIs, data models, dependencies, migration plan |
| **Metrics** | No metrics or vague KPIs | NSM + leading + guardrail + tracking plan |
| **Tradeoffs** | No alternatives discussed | Options evaluated with pros/cons and reasoning |
| **Honest Gaps** | Pretends to have all answers | Open questions listed with owners and deadlines |

**Scoring guide:**
- 1-3: Task list or feature request, not a PRD
- 4-5: Has structure but shallow — no numbers, no logic, no empathy
- 6-7: Solid PRD with gaps — missing technical depth or tradeoffs
- 8-9: Strong PRD — comprehensive, quantified, actionable
- 10: Ravi-level — formula-driven, emotion-aware, copy-specified, state-machined

---

## Execution Instructions

### Mode: `/prd new [feature]`

**Step 1: Gather Context**
- Read relevant knowledge files: `knowledge/context/`, `knowledge/codebase/`, `knowledge/tools/`
- Check Linear for related issues/projects: team `fac85860-3e4c-4038-b0ea-2fd8c2efeca7`
- Check if there's an existing PRD on Google Drive (search for the feature name)
- Pull current metrics from Business Metrics Sheet (`132BnnON8niePEtWCz37RFcMs2l2LlrjHa7hdk9M6BAQ`) if relevant

**Step 2: Ask the Right Questions**
Before writing anything, ask Ravi 5-8 targeted questions that force the thinking:
- What's the formula? What lever does this pull?
- Who are the internal users? What's their current workflow?
- What's the constraint that makes this hard?
- What did you consider and reject?
- What's the smallest version that would prove the hypothesis?

**Step 3: Draft**
Write the PRD following the framework above. Match Ravi's voice:
- Direct, no fluff
- Questions embedded in the document where answers aren't known yet
- Actual UI copy proposed, not placeholders
- Throughput math for capacity-related features
- Emotional states for customer-facing features
- "TO BE PICKED LATER" for sections that need more discovery — don't BS

**Step 4: Review Together**
Present the draft with a self-critique: "Here's what I'm confident about, here's where I need your input, here's what I'd push back on if I were reviewing this."

### Mode: `/prd review [Google Doc ID]`

**Step 1: Fetch the Document**
Use `getGoogleDocContent` with the provided document ID.

**Step 2: Score It**
Apply the Quality Scoring Rubric. Present scores in a table.

**Step 3: Critique**
For each dimension scoring below 7:
- State what's missing (specific, not vague)
- Give an example of what good looks like (reference Ravi's PRDs or the framework)
- Suggest specific additions or rewrites

**Step 4: Structural Feedback**
- Is the thinking cascade intact? (Problem → Formula → Root Cause → Solution)
- Are there unsupported assertions? ("This will improve efficiency" — by how much? How do you know?)
- Is the spec buildable? Could an engineer implement from this without 20 clarification questions?
- Are emotions and internal personas considered?

**Step 5: Calibrate to Author**
- For Rahul: Focus on fundamentals — does a PRD even exist? Push for problem statement, user context, and basic specifications. He needs scaffolding.
- For Khushi: Push for depth — tradeoffs, technical specs, wireframes, emotional journey. She has the instinct, needs the framework.
- For Sumit: Expect near-Ravi quality. Push on Propsoch-specific context and formula decomposition.
- For Ravi: Be a sparring partner. Challenge assumptions, find blind spots, push on risks and non-goals.

**Step 6: Deliver**
Structure as:
1. Overall assessment (2-3 sentences)
2. Score table
3. Top 3 critical gaps (with specific fix suggestions)
4. Section-by-section feedback (only where needed)
5. What's good (acknowledge strengths — especially for team members building the muscle)

### Mode: `/prd edit [Google Doc ID]`

**Step 1: Fetch and Score**
Same as review Steps 1-2.

**Step 2: Propose Edits**
For each gap, write the actual content that should be added — not just "add a business case" but the actual Before/After table with numbers, the actual formula, the actual UI copy.

**Step 3: Present as Diff**
Show what exists vs what should exist. Let Ravi approve before any Google Doc updates.

**Step 4: Update**
If approved, use `updateGoogleDoc` to apply changes. Preserve the author's voice — strengthen, don't overwrite.

### Mode: `/prd template`

Output the Propsoch PRD Framework (Section above) as clean markdown that can be copied into a Google Doc. Add section-specific prompting questions as comments to guide the author.

---

## Propsoch-Specific Context

Always consider when writing or reviewing Propsoch PRDs:

**Product verticals:**
- Service (GHB journey, advisory, site visits, reports)
- Demand (website, SEO, conversion, lead gen)
- Comms (WhatsApp, email, notifications, nudges)
- Internal Tools (Angelo, CRM, dashboards, trackers)

**Key systems:**
- Angelo (internal ops tool — React/Next.js)
- GHB Journey (customer-facing — propsoch.com)
- Comms engine (WhatsApp + email automation)
- Backend (Node.js + Python, PostgreSQL, AWS)

**Operational reality:**
- 33-person team, not 300. Features must be simple enough for non-tech ops team.
- CSPs/SMEs/MAs are the primary internal users — they're busy, not technical, and already overwhelmed.
- Bangalore is mature (16-28 homes/month), Mumbai is new (4-5 months old). Features may need city-specific rollout.
- 90/10 service/product mix targeting 30/70 by EOY 2026. Every PRD should ask: "Does this move us toward product-led?"

**Quality bar reality:**
- "In real time at a startup, it may not always be feasible to be as detailed in the PRD."
- "All PRDs are work in progress and will always stay that way."
- "But we need to push for rigour."
- Push for rigour, but don't let perfect be the enemy of shipped.

---

## Reference Documents (Ravi's)

For calibration on voice, depth, and style:
- GHB Journey PRD: `166SND_WStU0QT7Jctx7Ga0Lichp0m--6CkLaK6q8aR0`
- Angelo PRD: `1R5GCYWWSqbc0cPfZFshAOt4XExgGhHtFdYGKknb324w`
- PRD Template (Upraised): `12tjxRIQUB_tFjsrCKJtlCxQPdkHPWg1LoDm0a5sSKD0`
- Product Strategy Ops: `1UBCgfrepj4xcZM8wbNLIUbTkajKigedX2HLvHjFwUuk`
- Product Strategy Growth: `1rb_ENAavPorxLok1_zv3cMeimmJuMxYu373pk2NlH7Y`

**Team PRDs (for calibration on current level):**
- Rahul — Fair Price Calculator: `1kMrHRp2W_fZvvPjv2WOBDtMxynwPXVFKJkFR1LjMr10` (Score: ~1/10)
- Khushi — Task Management System: `1Y2x-nW1R6RDvXJ5cFfB0P58ih816fUeJ97evMmsEr2Q` (Score: ~6/10)

---

## Interactive Questioning Rules (Borrowed from gstack)

- **One issue = one AskUserQuestion.** Never batch.
- **Lead with recommendation.** "Do B. Here's why:" — opinionated, not a menu.
- **Present 2-3 lettered options** for every decision. Label as NUMBER + LETTER (e.g., "3A").
- **Escape hatch:** Obvious fixes don't need questions — state what you'll do and move on.

## Completion Summary

At the end of every /prd run, display:

```
+====================================================================+
|            /prd — COMPLETION SUMMARY                               |
+====================================================================+
| Mode               | new / review / edit                           |
| Author             | [name]                                        |
| Score              | [X/10] across 10 dimensions                   |
+--------------------------------------------------------------------+
| Problem & Objective| [clear / vague / missing]                     |
| Formula            | [present / missing]                           |
| User Journey       | [mapped / partial / missing]                  |
| Edge Cases         | [N identified]                                |
| Success Metrics    | [defined / partial / missing]                 |
| Technical Spec     | [sufficient / needs depth]                    |
| Copy               | [specified / placeholder]                     |
| State Machine      | [diagrammed / missing]                        |
+--------------------------------------------------------------------+
| Critical Gaps      | [list]                                        |
| Author Coaching    | [1-2 specific growth areas]                   |
| Unresolved         | [list any open decisions]                     |
+====================================================================+
```
