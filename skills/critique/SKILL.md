---
name: critique
license: MIT
---

# /critique — Product Spec Critique & Pre-Mortem

Stress-test product specs, PRDs, and design decisions before committing engineering resources. Uses structured frameworks to surface risks, blind spots, and untested assumptions.

This is the tool you use AFTER `/design` or `/prd` produces a spec — and BEFORE engineering starts building.

## Model Routing

**This skill runs interactively in the main session.**

- If on Opus: Run directly (preferred for deep reasoning)
- If on Sonnet: Run directly for lightweight critiques, spawn Opus sub-agent for full pre-mortems

## Usage
```
/critique [spec or doc path]           # Full critique (all frameworks)
/critique premortem [spec]             # Pre-mortem only (Tigers, Paper Tigers, Elephants)
/critique risks [spec]                 # Four-risk analysis (Value, Usability, Viability, Feasibility)
/critique assumptions [spec]           # Surface and test untested assumptions
/critique killcriteria [spec]          # Define kill criteria and pre-commitments
```

---

## The Critique Operating System

### Philosophy

The most expensive bugs are not in code — they're in thinking. A spec that's wrong but well-engineered costs more than a spec that's right but poorly formatted. The job of `/critique` is to find the thinking bugs before they become engineering bugs.

### The Rule

**Be honest, not kind.** A critique that says "looks good!" is useless. A critique that says "this will fail because X, and here's the evidence" is invaluable. The person receiving the critique would rather hear hard truths now than discover them after 3 months of engineering.

---

## Framework 1: Pre-Mortem (Shreyas Doshi)

### When to Use
Before committing to build anything in the spec. Especially important for:
- Large initiatives (>2 weeks of engineering)
- New product surfaces (not iterations on existing)
- Anything involving new data pipelines or integrations
- Anything affecting the core conversion funnel

### The Taxonomy

**Tigers** — Real threats that could kill the project or make it fail.
These are the risks that, if they materialize, mean the project doesn't achieve its goals. Not "it could be better" — "it could fail."

Questions to surface Tigers:
- "If this project fails in 6 months, what's the most likely reason?"
- "What are we assuming about user behavior that hasn't been validated?"
- "What dependency could block this that we're not tracking?"
- "What's the hardest part of this to build, and what happens if it doesn't work?"
- "Is there a market/competitive change that could make this irrelevant?"

**Paper Tigers** — Things that seem threatening but aren't real risks.
These waste team energy. Naming them frees the team to focus on actual Tigers.

Questions to surface Paper Tigers:
- "What risks are people worried about that probably won't materialize?"
- "What objection keeps coming up that we have evidence against?"
- "What sounds scary but has precedent showing it works?"

**Elephants** — Big unspoken risks nobody is talking about.
These are the most dangerous. They're often obvious in hindsight but invisible in the moment because they're uncomfortable to raise.

Questions to surface Elephants:
- "What would a new hire, seeing this spec for the first time, immediately question?"
- "What would a competitor say is the weakness of this approach?"
- "What are we not saying because it's awkward or political?"
- "If the CEO read this spec, what would they challenge first?"
- "What user behavior are we hoping for but have no evidence of?"

### Process (Shreyas's Modified Script — 1 Hour)

**When running with a team:**
1. **Context setting (5 min):** Introduce the concept. Ask everyone to come up with 2+ Tigers, plus any Paper Tigers and Elephants.
2. **Quiet Time #1 (10 min):** Everyone writes independently. NO talking. Silence is productive.
3. **Quiet Time #2 (10 min):** Read everyone else's items. Give up to 5 "+1" votes. Be selective.
4. **Discussion (20 min):** Go around the room. What Tiger resonated most? What was surprising?
5. **Wrap-up (5 min):** Facilitator summarizes top themes.
6. **Action Plan (post-meeting):** The most important part. See below.

**When running as a solo exercise (product leader + AI):**
1. **Read the spec.** Absorb fully before critiquing.
2. **Silent brainstorm.** List all Tigers, Paper Tigers, and Elephants.
3. **Present findings.** For each item:
   - Name it clearly (1 sentence, use the team's actual language when possible)
   - Explain why it's a risk (evidence or reasoning)
   - Classify: Tiger / Paper Tiger / Elephant
   - Suggest mitigation (for Tigers) or de-escalation (for Paper Tigers)
4. **Prioritize.** Rank Tigers by: likelihood × impact. Top 3 get action plans.
5. **Define kill criteria.** For the top 3 Tigers, what signal tells us this risk is materializing?

### The Pre-Mortem Action Plan

This is the output that matters. Not the meeting — the plan.

| Priority | Verbatim Tiger/Elephant | DRI | Mitigating Actions (priority order) |
|----------|------------------------|-----|-------------------------------------|
| 1 | [Exact language from the brainstorm] | [Single person] | 1. [Reduce chances] 2. [Limit impact if it occurs] |

**Rules:**
- List verbatim language (reassures the team their input was used)
- Single DRI per item (can delegate, but one person owns it)
- Don't list every possible problem — focus on the deadliest Tigers
- Accept living with some problems (solving one often creates another — be explicit about which problems you'll tolerate)
- Merge the action plan into the project plan — not a one-off document
- Track progress against the action plan throughout the project lifecycle

---

## Framework 2: Four-Risk Analysis (SVPG)

### When to Use
For any feature or product surface. Quick assessment that covers all bases.

### The Four Risks

**Value Risk** — Will users actually want this?
- Is there evidence of demand (user research, behavioral data, competitor validation)?
- Are we solving a real problem or an assumed one?
- Would users choose this over their current alternative (including doing nothing)?
- What's the "so what?" test — if we built this perfectly, would it matter?

**Usability Risk** — Can users actually use this?
- Is the interaction model familiar (Jacob's Law) or novel?
- How many steps to get value? (Every step is a drop-off point)
- What's the cognitive load? Can a distracted person on their phone at 10pm use this?
- What happens when things go wrong? (Error states, edge cases, recovery)

**Viability Risk** — Does this work for the business?
- Does this move a metric that matters? Which one?
- Does this create operational load? (Content production, support queries, advisor training)
- Does this scale? (What works for 100 users may break at 1000)
- Does this align with the 90/10 → 30/70 service-to-product transition?

**Feasibility Risk** — Can we actually build this?
- Do we have the data? (Check against existing data models)
- Do we have the skills? (Frontend, backend, AI/ML, content)
- What's the hardest technical component? What's the risk of it not working?
- Are there third-party dependencies? (Google Maps API, AI models, WhatsApp API)
- What's the smallest buildable version that tests the hypothesis?

### Output
Rate each risk: Low / Medium / High. For any "High," define:
- What specifically makes it high
- What would de-risk it (research, prototype, experiment)
- Whether it should block the build or can be addressed in parallel

---

## Framework 3: Assumption Surfacing (Teresa Torres + Annie Duke)

### When to Use
When the spec feels "obvious" or "clearly right." That's when assumptions are most dangerous — they're invisible because everyone agrees.

### Process

1. **List every assumption.** Go through the spec section by section. For each design decision, ask: "What are we assuming is true for this to work?"

   Categories of assumptions:
   - **User behavior:** "Users will complete the discovery form" / "Users will return to the Explorer between calls"
   - **Data quality:** "Our project data is accurate enough for match scoring" / "Price history is tracked consistently"
   - **Technical:** "The map can handle 100+ pins without performance issues" / "AI can reliably analyze floor plans"
   - **Market:** "Buyers want self-serve exploration" / "Transparency about challenges builds trust rather than scaring buyers"
   - **Operational:** "Advisors will actually use the mirror view" / "Content team can produce 50 master plan videos"

2. **Classify each assumption.**
   - **Known true:** Evidence exists (data, research, precedent)
   - **Believed true:** Strong intuition but no hard evidence
   - **Hoped true:** We want this to be true but have reasons to doubt
   - **Unknown:** We genuinely don't know

3. **For "Believed true" and "Hoped true":**
   - What would it take to validate? (Interview, prototype, experiment, data analysis)
   - What's the cost of being wrong? (Low = proceed. High = validate first.)
   - Can we design the spec to be robust even if this assumption is wrong?

4. **For "Unknown":**
   - Is this a blocking unknown (can't build without knowing) or a non-blocking unknown (can build and learn)?
   - If blocking: what's the fastest way to answer it?

### Output
Assumption map: Table of assumptions, classification, validation method, cost of being wrong.

---

## Framework 4: Kill Criteria (Annie Duke)

### When to Use
After the pre-mortem has surfaced risks. Before engineering begins.

### Process

For each Tiger (top 3-5 risks):
1. **Define the signal.** What observable metric or event would indicate this risk is materializing?
2. **Define the threshold.** At what level does the signal become a problem? (Not "engagement is low" but "less than 20% of users complete the discovery form in the first week")
3. **Define the action.** What do we commit to doing when we see the signal?
   - Pause and investigate?
   - Pivot the approach?
   - Kill the feature?
   - Double down with changes?
4. **Pre-commit.** Write this down BEFORE building. Sunk cost bias makes it nearly impossible to quit after you've invested — pre-committing removes the emotional barrier.

### Output
Kill criteria table: Risk → Signal → Threshold → Action → Owner → Review date

---

## Framework 5: Confidence Assessment (Itamar Gilad)

### When to Use
When deciding whether to commit engineering resources or do more discovery first.

### The Ladder

Rate the overall spec confidence:

| Level | Evidence Type | Confidence | Action |
|-------|-------------|-----------|--------|
| 1 | Authority ("CEO wants it") | Very low | Challenge. Get real evidence. |
| 2 | Thematic ("AI is hot") | Very low | Challenge. Trends don't validate products. |
| 3 | Colleague review | Low | Helpful but still guesses. |
| 4 | Back-of-envelope estimates | Medium | Good for scoping. Not for commitment. |
| 5 | User research / market data | Medium-high | Strong foundation. Can commit to V1. |
| 6 | Prototype / experiment results | High | Can commit to full build. |

**For Propsoch's current spec work:** Most of our confidence is at level 5 (user research from 8 interviews + operational data + market analysis). Some assumptions are at level 3-4. The critique should identify which assumptions are below level 5 and need de-risking.

---

## Execution Flow

### Mode: `/critique [spec]` (Full Critique)

1. **Read the spec fully.** Don't critique section by section — understand the whole first.
2. **Run Pre-Mortem.** Surface Tigers, Paper Tigers, Elephants.
3. **Run Four-Risk Analysis.** Value, Usability, Viability, Feasibility.
4. **Surface Assumptions.** List, classify, identify the dangerous ones.
5. **Assess Confidence.** Where is the spec on the ladder?
6. **Define Kill Criteria.** For top risks.
7. **Deliver verdict.** One of:
   - "Ready to build" — risks are manageable, confidence is sufficient
   - "Ready to build V1, but validate these 3 assumptions in parallel"
   - "Not ready — these assumptions need testing first"
   - "Fundamentally flawed — here's why and what to rethink"

### Mode: `/critique premortem [spec]`
Steps 1-2 only. Fast. 15-minute exercise.

### Mode: `/critique risks [spec]`
Steps 1, 3 only. Four-risk assessment.

### Mode: `/critique assumptions [spec]`
Steps 1, 4-5 only. Assumption surfacing + confidence assessment.

### Mode: `/critique killcriteria [spec]`
Steps 1, 6 only. Requires pre-mortem to have been run first (needs the Tigers).

---

## Perspective Lenses

When running a full critique, evaluate the spec through multiple lenses:

| Lens | Core Question |
|------|--------------|
| **The first-time buyer** | "Would I actually use this? Does it feel overwhelming or helpful?" |
| **The repeat buyer** | "This is designed for first-timers — does it get in my way?" |
| **The advisor** | "Does this make my job easier or harder? Will I actually use the mirror view?" |
| **The ops team** | "What new burden does this create? Content production? Support queries?" |
| **The engineer** | "Is this buildable? What's the ugly part? What will take 10x longer than the PM thinks?" |
| **The skeptic** | "Is this product theater or does it actually move a metric?" |
| **The competitor** | "If I saw Propsoch launch this, would I be worried or amused?" |
| **The 6-month future** | "Will this still make sense in 6 months, or are we building for today's constraints?" |

---

## Propsoch-Specific Critique Checks

Always evaluate against these:

1. **Service-to-product transition:** Does this move from 90/10 toward 30/70? Or does it add product complexity without reducing service load?
2. **Advisor workflow impact:** Does the advisor need to change behavior? If yes, what's the change management plan?
3. **Content production burden:** How much new content needs to be created and maintained? Who does it? What's the ongoing cost?
4. **Data dependency:** Does this require data that exists in the DB? Or data that needs new pipelines? Check against the 46 Sequelize models.
5. **Mobile-first:** Was this designed for mobile? Or is it a desktop spec being squeezed onto mobile?
6. **Bangalore + Mumbai:** Does this work for both cities? Or only Bangalore?
7. **Scale test:** Does this work at 100 users/month? At 1000? Where does it break?

---

## Anti-Patterns

1. **"Looks good!" critique.** If you can't find anything wrong, you haven't looked hard enough.
2. **Critique without solutions.** Every identified risk should come with a mitigation suggestion or a "here's how to find out."
3. **Critiquing style instead of substance.** The spec's formatting doesn't matter. The thinking does.
4. **Optimism bias.** "Users will love this" is not evidence. "8/8 interviewed users said they wanted independent exploration" is.
5. **Anchoring to the spec.** The spec proposes one approach. The critique should ask: "Is this the RIGHT approach, or just the one we thought of first?"

---

## Interactive Questioning Rules (Borrowed from gstack)

- **One issue = one question.** Never batch multiple findings into one question.
- **Lead with your recommendation.** "Do B. Here's why:" — not "Option B might be worth considering."
- **Present 2-3 lettered options** (A, B, C) for every decision. Include "accept the risk" when reasonable.
- **Label with NUMBER + LETTER** (e.g., "3A", "3B") so Ravi can respond quickly.
- **Escape hatch:** If a framework surfaces no issues, say so and move on. Don't force findings.

## Completion Summary

At the end of every /critique run, display:

```
+====================================================================+
|            /critique — COMPLETION SUMMARY                          |
+====================================================================+
| Pre-Mortem         | Tigers: ___ | Paper Tigers: ___ | Elephants: ___|
| Four-Risk Analysis | Value: L/M/H | Usability: L/M/H | Viability: L/M/H | Feasibility: L/M/H |
| Assumptions        | ___ total | ___ known true | ___ believed | ___ hoped | ___ unknown |
| Confidence Level   | [1-6] — [description]                      |
| Kill Criteria      | ___ defined for top risks                   |
+--------------------------------------------------------------------+
| Verdict            | Ready to build / V1 + validate / Not ready / Flawed |
| Top 3 Risks        | 1. ___ 2. ___ 3. ___                        |
| Unresolved         | [list any unanswered questions]              |
+====================================================================+
```
