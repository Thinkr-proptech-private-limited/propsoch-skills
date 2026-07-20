---
name: rca
license: MIT
---

# /rca — Root Cause Analysis

Structured data investigation that catches its own blind spots before presenting findings. Use this for any question that requires pulling data from multiple sources, computing metrics, or drawing conclusions about user behavior, funnel performance, or business trends.

This skill exists because data analysis without self-critique produces confidently wrong conclusions. The cost of a wrong conclusion acted upon exceeds the cost of a slower, more careful investigation.

## Model Routing

**This skill runs interactively in the main session.**

- If on Opus: Run directly
- If on Sonnet: Run directly for single-source investigations, spawn Opus sub-agent for multi-source cross-referencing

## Usage
```
/rca [question]                    # Full investigation (all 6 phases)
/rca quick [question]              # Phases 1-4 only (skip deep critique, faster)
/rca critique [prior finding]      # Run Phase 5 against a finding already presented
/rca validate [metric/claim]       # Run Phase 3 only against a specific metric
```

---

## The Investigation Protocol

### Philosophy

Every data point is guilty until proven innocent. Every metric measures something specific — the job is to verify it measures what you think it measures before building arguments on it. The most dangerous analyses are the ones that feel obvious.

### The Six Phases

```
Phase 1: Frame    → What are we actually asking? What would good/bad answers look like?
Phase 2: Gather   → Pull from all relevant sources. Cast wide.
Phase 3: Validate → MANDATORY GATE. Does this data mean what I think it means?
Phase 4: Analyze  → Find patterns, compute rates, compare periods
Phase 5: Critique → MANDATORY GATE. What's wrong with my analysis?
Phase 6: Present  → Findings with confidence levels and known gaps
```

Phases 3 and 5 are non-negotiable. Skipping them is not allowed even in `/rca quick` mode (quick skips deep critique but still runs basic validation and a lightweight self-check).

---

## Phase 1: Frame

Before touching any data source:

1. **State the question in one sentence.** If you can't, the question isn't clear enough yet. Ask Ravi.
2. **Define the answer space.** What would a "good" answer look like? What would a "bad" answer look like? What would a "surprising" answer look like?
3. **Identify the decision this feeds.** Why does this matter? What will Ravi do differently based on the answer?
4. **List hypotheses upfront.** Before looking at data, write 2-3 plausible explanations. This prevents anchoring to the first pattern you see.
5. **Scope the time period.** Default to the longest meaningful range. A single month is almost never enough. Note any known tracking changes, code deploys, or campaign shifts within the period.

**Output:** A framing paragraph (2-4 sentences) that Ravi can redirect before data is pulled.

---

## Phase 2: Gather

Pull data from ALL relevant sources, not just the most convenient one.

### Source Priority for Propsoch

| Question Type | Primary Source | Cross-Reference With |
|---------------|---------------|---------------------|
| Website funnel (views → signup) | Mixpanel events | GA4 page views, CRM leads |
| Actual conversions (signups, members) | Comms API (leads + members) | Mixpanel submissions, Calendly bookings |
| Pitch call bookings | Calendly API | Mixpanel Event Scheduled, CRM Pitch_Date |
| Traffic by channel | GA4 | Mixpanel entry_point (caveat: first-touch) |
| Ad performance | Meta Ads API, GA4 Google Ads dims | CRM UTM fields |
| Revenue / deal data | Comms API /deals | — |
| Page engagement | GA4 (bounce, duration) | Mixpanel interaction events |

### Gathering Rules

- Always pull the full available time range first. Narrow later if needed.
- Pull from at least two sources for any key metric.
- Note the data freshness. When was this data last updated?
- Check for known outages, tracking changes, or code deploys in the period.

**Output:** Raw data tables. No interpretation yet.

---

## Phase 3: Validate (MANDATORY GATE)

For EVERY metric or data point that will inform a finding, run these checks:

### 3A — Metric Definition Audit

- What does this metric actually measure? (Read the code if unsure)
- Is it first-touch, last-touch, or session-scoped?
- What population does it include/exclude?
- When was tracking added? Is pre-tracking data showing as zero or undefined?
- Is there deduplication? Can one user fire this event multiple times?

### 3B — Cross-Source Reconciliation

- Do different sources agree? Within what margin?
- If they disagree by >20%, explain why before proceeding.
- Known divergences (document these, don't rediscover them):
  - Mixpanel Event Scheduled = 54-68% of Calendly active bookings (isActive timeout bug)
  - CRM leads ≠ Mixpanel submissions (CRM includes Meta form entries, manual creation)
  - GA4 sessions ≠ Mixpanel page views (different counting methods, different JS libraries)
  - entry_point is first-touch with 30-day TTL — NOT the page the user was on before clicking a CTA

### 3C — Population Check

- Am I comparing like with like? (Same city, same device type, same time period)
- Am I accidentally including Mumbai in Bangalore numbers or vice versa?
- Am I including localhost/dev traffic?
- Am I including bot/crawler traffic?

### 3D — Denominator Sanity

- Is the denominator what I think it is? (Views, sessions, unique users, events?)
- Could the denominator be inflated by page reloads, bot traffic, or tracking duplicates?
- Is a conversion rate >100%? If so, the numerator and denominator are from different populations.

**Output:** A validation table. For each key metric: what it measures, known limitations, cross-reference result, confidence rating (HIGH/MEDIUM/LOW).

**Gate rule:** If any key metric has LOW confidence, either find a better data source or explicitly flag it in the final presentation. Do not build arguments on LOW-confidence metrics.

---

## Phase 4: Analyze

Now — and only now — interpret the data.

### Analysis Checklist

1. **Trends over time.** Use the longest range available. Note inflection points.
2. **Segmentation.** Break down by device (iPhone/Android/Desktop), city, channel, day-of-week where relevant.
3. **Comparisons.** Compare periods, segments, channels. Use absolute numbers alongside percentages — a 50% rate means different things for 100 users vs 10,000.
4. **Correlations vs causation.** If two things changed at the same time, note the correlation. Don't claim causation unless you can rule out confounders.
5. **Anomaly detection.** Flag months/weeks that deviate >2x from the surrounding trend. Investigate before including in averages.

### Propsoch-Specific Analysis Patterns

- **Always separate BLR and Mumbai.** Combined numbers hide everything.
- **Always separate iPhone, Android, Desktop.** They are three different funnels.
- **Check for code deploy timing.** Git log the relevant component around any inflection point.
- **Check for campaign timing.** Ad budget changes, new campaigns, campaign pauses drive traffic shifts.
- **Check for seasonal patterns.** Real estate has seasonality (Q4 is slow, Jan-Mar is peak).

**Output:** Findings as numbered items with supporting data.

---

## Phase 5: Critique (MANDATORY GATE)

Before presenting findings, attack your own analysis.

### 5A — Alternative Explanations

For each finding, list at least two alternative explanations for the same data. State which the data supports, which it can't distinguish between, and what additional data would disambiguate.

### 5B — Assumption Inventory

List every assumption the analysis makes. Classify:
- **Verified:** Code/data confirms this assumption
- **Reasonable:** Likely true but not explicitly verified
- **Assumed:** Taken for granted, could be wrong

For each ASSUMED item: what happens to the conclusion if this assumption is wrong?

### 5C — Missing Data

What data would strengthen this analysis but doesn't exist or wasn't pulled?
What questions does this analysis raise that it can't answer?

### 5D — Confidence Assessment

Rate overall confidence: STRONG / MODERATE / WEAK / SPECULATIVE (per data-interpretation.md rule).

### 5E — Pre-Mortem

"If Ravi reads this analysis and says 'this is wrong,' what's the most likely reason?" Write that down. Then either fix it or flag it.

**Gate rule:** If the pre-mortem identifies a fatal flaw, go back to Phase 2 or 3. Do not present.

---

## Phase 6: Present

### Structure

```
## Question
[One sentence]

## TL;DR
[2-3 sentence answer with confidence level]

## Key Findings
[Numbered, each with:]
- The finding (one sentence)
- Supporting data (table or numbers)
- Confidence: STRONG/MODERATE/WEAK
- Caveat (if any)

## What This Does NOT Tell Us
[Explicitly list questions this analysis can't answer]

## Recommendations
[Numbered, each tied to a finding]

## Open Questions
[What would make this analysis stronger]
```

### Presentation Rules

- Lead with the answer, not the methodology.
- Every number gets a source label: [Mixpanel], [GA4], [CRM], [Calendly], [Calculated].
- Never say "the data clearly shows" — say "Mixpanel data for Dec-Apr indicates."
- If a finding is WEAK confidence, say so before Ravi has to ask.
- Tables beat paragraphs for numeric data.
- Absolute numbers alongside percentages. Always.

---

## Propsoch Data Gotchas Checklist

Run through this before presenting. If any apply and you didn't account for them, go back.

- [ ] `entry_point` is first-touch (30-day TTL), not last-page-before-signup
- [ ] Mixpanel captures 54-68% of Calendly bookings (isActive timeout)
- [ ] CRM `/leads` + `/members` must be summed (separate Zoho modules)
- [ ] `/members` endpoint currently returns error — use `/deals` as proxy
- [ ] Form step events (Selected Area, Budget, etc.) don't carry the selected value
- [ ] Community Exit event lacks typology/budget/exitReason properties
- [ ] City tracking (`city` property) started Sep 22, 2025 — pre-Sep is undefined
- [ ] Use URL-based split (`/get-started` vs `/get-started-mumbai`) for city, not city property on form events
- [ ] `Initiated Pitch Call Flow` fires from 7+ locations — not a funnel step
- [ ] Dec-Jan Mixpanel views are inflated by Display traffic (16K-19K with <15% start rate)
- [ ] Feb 2026 Mixpanel had a brief `city=bengaluru` (lowercase) variant alongside `Bangalore`
- [ ] GA4 and Mixpanel count differently — don't mix GA4 sessions with Mixpanel events as if they're equivalent
- [ ] Google Ads cost data NOT available through GA4 — need Google Ads console
- [ ] `$device=undefined` in Mixpanel is mostly desktop browsers, not missing data
- [ ] PreSales joins Calendly calls — they don't outbound-schedule calls
- [ ] Budget thresholds for Community Exit are confirmed correct by Ravi — don't question them

---

## Completion Summary

```
+====================================================================+
|            /rca — COMPLETION SUMMARY                               |
+====================================================================+
| Question           | [one sentence]                                |
| Sources Used       | [list]                                        |
| Time Period        | [range + justification]                       |
| Cross-Referencing  | [which sources were compared]                 |
+--------------------------------------------------------------------+
| Findings           | [N] total                                     |
|   STRONG           | [N]                                           |
|   MODERATE         | [N]                                           |
|   WEAK             | [N]                                           |
| Gotchas Applied    | [N] of 16 checked                             |
| Alternative Expl.  | [N] considered                                |
| Open Questions     | [list]                                        |
+====================================================================+
```
