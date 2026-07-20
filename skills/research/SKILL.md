---
name: research
license: MIT
---

# /research — Deep Dive Research

Conduct comprehensive research on any topic.

## Model Routing

**This skill uses Opus for deep reasoning.**

- **Data gathering** (Steps 1-3): Run in the current session (Sonnet — fast, cheap)
  - Lenny's corpus search, web search, internal metrics pull
- **Synthesis & Analysis** (Steps 4-5): Spawn a Task sub-agent with `model: "opus"`
  - Pass all gathered data as context in the prompt
  - Opus handles: insight extraction, contrarian analysis, Propsoch implications, recommendations
  - The sub-agent should follow the Research Output Structure below

```
Task(
  subagent_type: "general-purpose",
  model: "opus",
  prompt: "You are TARS, Ravi Agrawal's executive intelligence system.
    Synthesize the following research data into a deep analysis...
    [paste gathered data, sources, Lenny's quotes]
    Follow the Research Output Structure. Apply Propsoch context.
    Challenge assumptions. Flag contrarian views."
)
```

## Usage
```
/research [topic]                   # General research
/research [topic] --quick           # 10-minute summary
/research [topic] --exhaustive      # Leave no stone unturned
/research compare [A] vs [B]        # Comparative analysis
```

---

## Step 0: Mode Selection (Mandatory)

Before any research begins, lock the mode. This determines depth, time investment, and output structure.

| Mode | Trigger | Sources | Depth | Output |
|------|---------|---------|-------|--------|
| **Quick** | `--quick` | 1-2 web searches + internal check | Surface | 5 bullets + confidence + 1 recommendation |
| **Standard** | default | Lenny's + 3-4 web sources + internal data | Balanced | Full Research Output Structure |
| **Exhaustive** | `--exhaustive` | Everything: Lenny's corpus deep scan, 6+ web sources, internal metrics, academic/industry sources | Maximum | Full structure + contrarian views + historical analysis |
| **Compare** | `compare` | Side-by-side evidence for each option | Analytical | Comparison matrix + recommendation |

**Commit fully to the chosen mode.** Quick mode means quick — don't scope-creep into Standard. Exhaustive means leave no stone unturned — don't shortcut.

State the mode and proceed. If the topic clearly implies a mode (e.g., "quick check on X" = Quick), don't ask.

---

## Research Output Structure

### Executive Summary
- Key findings (5 bullets max)
- Confidence level in findings
- Major knowledge gaps

### Background & Context
- What this is and why it matters
- Historical context if relevant
- Current state of affairs

### Deep Analysis
- Core findings organized by theme
- Evidence and sources for each
- Conflicting viewpoints noted
- Data and statistics where available

### Implications
- What this means for Ravi personally
- What this means for Propsoch
- Opportunities identified
- Risks or threats identified

### Recommendations
- Specific actions to take
- Priority order
- Resource requirements

### Sources & Further Reading
- Primary sources used
- Quality assessment of sources
- Recommended deep dives

### Open Questions
- What we still don't know
- How to find out

## Research Modes

### Quick Mode (--quick)
- 10-minute equivalent
- Top 3-5 findings only
- One reliable source per finding
- Good for: Initial scoping, time-sensitive decisions

### Standard Mode (default)
- Comprehensive but focused
- Multiple sources cross-referenced
- Balanced depth and breadth
- Good for: Most research needs

### Exhaustive Mode (--exhaustive)
- Leave no stone unturned
- Academic and industry sources
- Historical analysis included
- Contrarian views actively sought
- Good for: Major decisions, deep expertise building

## Research Quality Standards

1. **Source Hierarchy**:
   - Primary sources > Secondary sources > Opinions
   - Recent > Old (unless historical context needed)
   - Expert practitioners > Journalists > Generalists

2. **Bias Check**:
   - Who wrote this and why?
   - What's their incentive?
   - What are they not saying?

3. **Confidence Levels**:
   - High: Multiple reliable sources agree
   - Medium: Some sources, some inference
   - Low: Limited sources, educated guess

4. **Propsoch Lens**:
   - Always connect findings to Ravi's context
   - "So what?" for every finding

## Research Domains (Context)

When researching, keep in mind Ravi's domains:
- Proptech and real estate (India focus)
- AI/ML applications
- Product management and strategy
- Startup scaling and team building
- Indian market dynamics
- Fundraising and finance

## Internal Sources (Check Before Web)

### Lenny's Podcast Corpus
**Location:** `knowledge/resources/lennys-transcripts/`
**Scope:** 269 episodes, 303 guest folders, 89 topic indexes

For topics touching product, growth, leadership, hiring, AI, or startup strategy:
1. Check topic indexes in `knowledge/resources/lennys-transcripts/index/` for relevant episodes
2. Grep transcripts for specific keywords across `knowledge/resources/lennys-transcripts/episodes/`
3. Read frontmatter (first 15 lines) of matches for guest credentials and episode context
4. For top 3-5 matches, use Task tool with Explore agent to extract key quotes and frameworks
5. Weave expert insights into the research output under a "From the Experts" section

**Topic coverage:** product-management (142 eps), leadership (73), entrepreneurship (52), product-strategy (52), career-development (40), growth-strategy (33), ai (27), hiring (19), team-building (20), company-culture (22), and 79 more topics.

### Internal Data (When Topic Involves Propsoch)
- **Business metrics:** Google Drive sheet `132BnnON8niePEtWCz37RFcMs2l2LlrjHa7hdk9M6BAQ`
- **Sprint/engineering:** Linear (team `fac85860-3e4c-4038-b0ea-2fd8c2efeca7`)
- **Team signals:** Slack channels (use conversations_search_messages for targeted queries)
- **Traffic:** GA4 property `306405671`
- **Product analytics:** Mixpanel project `3524084`
- **Context files:** `knowledge/context/` (team structure, hiring status, competency matrices, business metrics)

### Knowledge Files
- `knowledge/tools/` — MCP tool reference (IDs, common queries, patterns)
- `knowledge/codebase/` — Frontend and backend architecture
- `knowledge/briefs/` — Previous intelligence briefings with flags and patterns

---

## Execution

### Step 1: Scope
- Clarify depth needed (quick / standard / exhaustive)
- Identify if internal sources are relevant

### Step 2: Internal sources (if applicable)
- Search Lenny's corpus for expert perspectives
- Pull internal metrics if topic touches Propsoch operations
- Check knowledge files for existing context

### Step 3: Web research
- WebSearch for current information (2-3 queries)
- WebFetch 2-4 high-quality sources
- Cross-reference multiple sources

### Step 4: Synthesize
- Merge internal expert insights with web research
- Apply Propsoch lens: "So what?" for every finding
- Separate facts from inference, note confidence levels

### Step 5: Deliver
- Follow the Research Output Structure above
- Include "From the Experts" section when Lenny's corpus contributed
- Always end with actionable recommendations
- Store valuable research in `/knowledge/research/`

---

## State Persistence

For research on recurring topics (competitors, market trends, technology evaluations):
1. Save output to `knowledge/research/[topic-slug]-YYYY-MM-DD.md`
2. On future research of the same topic, load prior research and show what changed
3. Flag: new developments, contradicted findings, updated confidence levels

## Completion Summary

```
+====================================================================+
|            /research — COMPLETION SUMMARY                           |
+====================================================================+
| Mode               | Quick / Standard / Exhaustive / Compare       |
| Topic              | [topic]                                       |
| Sources Used       | [count] (Lenny's: X, Web: Y, Internal: Z)    |
+--------------------------------------------------------------------+
| Key Findings       | [count]                                       |
| Confidence         | High / Medium / Low                           |
| Propsoch Actions   | [count] recommendations                      |
| Contrarian Views   | [count] flagged                               |
+--------------------------------------------------------------------+
| Saved to           | knowledge/research/[file] (or "Not saved")    |
+====================================================================+
```
