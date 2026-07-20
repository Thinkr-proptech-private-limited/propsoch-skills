---
name: decide
license: MIT
---

# /decide — Decision Support

Provide structured analysis for decision-making.

## Model Routing

**This skill uses Opus for strategic reasoning.**

- **Data pull** (if decision involves Propsoch data): Run in current session (Sonnet)
  - Business metrics, Linear workload, GA4 traffic, Slack signals
- **Analysis & Recommendation**: Spawn a Task sub-agent with `model: "opus"`
  - Pass the decision context + all gathered data
  - Opus handles: framework selection, trade-off analysis, blind spot detection, recommendation with confidence level

```
Task(
  subagent_type: "general-purpose",
  model: "opus",
  prompt: "You are TARS, Ravi Agrawal's executive intelligence system.
    Analyze this decision using the framework below...
    [paste decision context, data, constraints]
    Apply the Decision Analysis Structure. Be direct. Challenge assumptions.
    State confidence level and key assumptions that must be true."
)
```

## Usage
```
/decide [situation]                 # Analyze a decision
/decide --framework [name]          # Use specific framework
/decide --quick                     # Rapid assessment (2 min)
```

## Decision Analysis Structure

### 1. Frame the Decision
- What exactly is being decided?
- What's the deadline?
- Who are the stakeholders?
- What's the reversibility? (One-way door vs two-way door)

### 2. Options Matrix

| Option | Pros | Cons | Effort | Impact | Risk |
|--------|------|------|--------|--------|------|
| A      |      |      | H/M/L  | H/M/L  | H/M/L|
| B      |      |      | H/M/L  | H/M/L  | H/M/L|
| C (do nothing) | | | - | - | - |

### 3. Key Considerations
- **Time sensitivity**: Can we wait for more information?
- **Reversibility**: How hard to undo?
- **Dependencies**: What else does this affect?
- **Resource requirements**: Money, time, people
- **Opportunity cost**: What are we NOT doing?

### 4. Recommendation
- **TARS recommends**: [Option]
- **Reasoning**: [Why]
- **Confidence**: High/Medium/Low
- **Key assumption**: [What must be true]

### 5. If Wrong
- What's the worst case?
- How would we know we're wrong?
- What's the recovery path?

## Decision Frameworks

### Bezos Regret Minimization
"In 80 years, will I regret NOT doing this?"
- Best for: Career moves, big bets, personal decisions

### Eisenhower Matrix
Urgent/Important quadrants
- Best for: Prioritization, time allocation

### RICE Scoring
Reach × Impact × Confidence / Effort
- Best for: Feature prioritization, roadmap decisions

### First Principles
Break down to fundamentals, rebuild logic
- Best for: Strategic decisions, challenging assumptions

### Reversibility Test
- Two-way door: Decide fast, adjust later
- One-way door: Analyze carefully, get input

### 10/10/10
How will I feel about this in 10 minutes / 10 months / 10 years?
- Best for: Emotional decisions, conflict resolution

## Quick Decision Mode (/decide --quick)

For rapid, on-spot decisions:
1. What's the worst realistic outcome?
2. Can we reverse it easily?
3. Does it align with our priorities?
4. Gut check: Does it feel right?

→ If low downside + reversible + aligned → **Do it**
→ If high downside OR irreversible → **Pause, analyze**

## Propsoch Decision Filters

For any Propsoch decision, also consider:
- Does this serve affluent homebuyers better?
- Does this strengthen our due diligence moat?
- Does this help the team perform?
- Does this move us toward revenue targets?
- Is this the right timing given fundraise status?

## Execution

1. **Clarify the decision** if ambiguous
2. **Pull internal data** when the decision involves:
   - Business metrics → Read Weekly Business Metrics Sheet (`132BnnON8niePEtWCz37RFcMs2l2LlrjHa7hdk9M6BAQ`) via Drive MCP
   - Team capacity → Check Linear current cycle workload (team `fac85860-3e4c-4038-b0ea-2fd8c2efeca7`)
   - Product execution → Read Product Execution Tracker (`1dMzpijNnT1HW-ZGPRgsIu8Wl8lN60saddGgRRRYLIac`)
   - Traffic/conversion → Pull GA4 report (property `306405671`) or Mixpanel (project `3524084`)
   - Reference thresholds and targets in `knowledge/context/BUSINESS_METRICS.md`
3. **List ALL options** including "do nothing"
4. **Be explicit about trade-offs** — use data from step 2 to ground the analysis
5. **Make a clear recommendation**
6. **State confidence level** and key assumptions
