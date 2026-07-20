---
name: brainstorm
license: MIT
---

# /brainstorm — Structured Ideation Engine

Generate a wide range of non-obvious solutions to a defined problem. Uses a four-stage diverge→converge process grounded in Opportunity Solution Trees, How Might We reframing, 10-Star thinking, and constraint-driven ideation.

This is NOT `/design` (which owns problem clarification) or `/prd` (which owns specification). `/brainstorm` assumes the problem is already understood and produces a ranked set of solution directions with testable hypotheses.

Use `/brainstorm` when:
- You have a clear problem but no solution yet
- You have a solution but want to explore alternatives before committing
- You're stuck in a local optimum and need fresh thinking
- A team discussion needs structured input, not just opinions

## Model Routing

**This skill runs interactively in the main session on Opus.**

For cross-industry analogies (Stage 2), spawn a background research agent if the problem domain is unfamiliar:
```
Agent(
  subagent_type: "general-purpose",
  model: "opus",
  prompt: "Find 5 industries that solved a structurally similar problem to [X].
    For each: company, mechanism, what worked, what failed.
    No hand-waving — name specific products and outcomes."
)
```

## Usage
```
/brainstorm [problem statement]              # Full four-stage process
/brainstorm diverge [problem]                # Stages 1-2 only (generate, don't converge)
/brainstorm converge [list of ideas]         # Stages 3-4 only (evaluate and rank)
/brainstorm reframe [stuck problem]          # Stage 1 only (HMW questions to unstick)
/brainstorm 10star [user journey step]       # 10-Star exercise only
```

---

## The Four Stages

```
Stage 1: REFRAME    → Break the problem into multiple "How Might We" questions
Stage 2: DIVERGE    → Generate 15-25 solution ideas across all HMW questions
Stage 3: EVALUATE   → Score ideas on impact × effort × confidence
Stage 4: CONVERGE   → Select top 3, write testable hypotheses, define experiments
```

Each stage has a clear output. Ravi can redirect after any stage.

---

## Stage 1: REFRAME

### Goal
Convert the problem statement into 5-8 "How Might We" questions that open different solution spaces. Each HMW should suggest a fundamentally different approach.

### Process

**Step 1: State the problem in one sentence.**
If it's vague, ask Ravi to sharpen it. Don't brainstorm against a fuzzy target.

**Step 2: Identify the actors, triggers, and stakes.**
- Who experiences this problem? (May be multiple personas.)
- When does the problem bite? What triggers it?
- What's at stake if it's not solved? (Revenue, time, trust, experience.)

**Step 3: Generate HMW questions using these lenses:**

| Lens | Prompt | Example (phone drop-off problem) |
|------|--------|----------------------------------|
| Remove the step | What if this step didn't exist? | HMW: How might we collect phone numbers without a dedicated input step? |
| Invert the problem | What if the opposite were true? | HMW: How might we make users WANT to give their phone number? |
| Change the timing | What if this happened earlier/later? | HMW: How might we get the phone number after they've seen the value? |
| Change the actor | What if someone else did this? | HMW: How might we let the system infer contact info without asking? |
| Change the channel | What if this happened elsewhere? | HMW: How might we capture phone via WhatsApp instead of a form field? |
| Reduce the friction | What's the smallest version? | HMW: How might we make entering a phone number take 1 tap not 10? |
| Amplify the motivation | What would make this irresistible? | HMW: How might we make the value of sharing a phone number obvious and immediate? |
| Use a constraint | What if we had zero engineering time? | HMW: How might we solve this with copy changes alone? |

**Step 4: Present 5-8 HMW questions.** Ask Ravi which ones feel most promising before moving to Stage 2. Don't proceed with all 8 — pick the top 3-4.

### Output
A numbered list of HMW questions, each opening a different solution direction.

---

## Stage 2: DIVERGE

### Goal
Generate 15-25 solution ideas across the selected HMW questions. Quantity over quality. No evaluation yet.

### Process

For each selected HMW question, generate 4-6 ideas using these techniques:

**Technique 1: Opportunity Solution Tree (Teresa Torres)**
Map the opportunity space: what are the sub-opportunities within this HMW? For each sub-opportunity, what's the simplest solution?

Example:
```
HMW: How might we make users WANT to give their phone number?
├── Opportunity: Users fear spam calls
│   ├── Solution: "No spam" guarantee with one-line copy
│   ├── Solution: OTP-less signup (email-only, phone later)
│   └── Solution: WhatsApp-only communication promise
├── Opportunity: Users don't understand why phone is needed
│   ├── Solution: "Your advisor will WhatsApp you" context
│   └── Solution: Show the advisor's photo + name before asking
└── Opportunity: Users are committed but the input is annoying
    ├── Solution: Autofill from browser/Google
    └── Solution: Click-to-call CTA instead of form input
```

**Technique 2: 10-Star Experience (Brian Chesky)**
Walk through the user experience at escalating ambition levels:
- 1-star: Current experience (the problem as-is)
- 3-star: The obvious fix (what a junior PM would propose)
- 5-star: A good solution (what a senior PM would ship)
- 7-star: A remarkable solution (users tell friends about it)
- 10-star: An absurd, magical solution (impossible but reveals true desire)

Then scale back from 10 to find the feasible 6-7 star version. The 10-star version exposes what users actually want beneath the surface request.

**Technique 3: Analogous Inspiration**
How do other industries solve a structurally similar problem?
- Insurance: Long consideration cycle, personal info collection → solved with instant quote (value before data)
- Dating apps: Profile creation friction → solved with progressive disclosure (start with photo, details later)
- Banking: KYC requirements → solved with video verification (one step replaces five)
- Luxury retail: High-intent browsing → solved with concierge approach (human reaches out to you)

Name specific companies and mechanisms, not abstract categories.

**Technique 4: Constraint Flipping**
Apply artificial constraints that force creative solutions:
- "Solve with zero code changes" → forces copy/process solutions
- "Solve in 1 day of engineering" → forces minimal interventions
- "Solve for the 10% who drop off, not the 90% who don't" → forces targeted solutions
- "What would we build if we had 100x the traffic?" → forces scalable thinking
- "What if the user couldn't see the screen?" → forces interaction model rethinking

**Technique 5: Jobs To Be Done Reframe (Bob Moesta)**
What job is the user hiring this step to do? The user isn't "entering their phone number" — they're "getting closer to talking to someone about their home purchase." What other ways could they accomplish that job?

### Rules During Diverge
- No evaluation. Don't say "this won't work because..." — that's Stage 3.
- Weird is good. The absurd idea often contains the seed of the practical one.
- Build on ideas. "Yes, AND..." not "Yes, BUT..."
- Aim for 15-25 total ideas. If you have fewer than 15, you stopped too early.

### Output
A numbered list of 15-25 ideas, grouped by HMW question, with a one-sentence description each.

---

## Stage 3: EVALUATE

### Goal
Score each idea and surface the top 5-7 for deeper evaluation.

### Process

**Step 1: Quick filter.** Remove ideas that violate hard constraints (budget, timeline, team size, technical feasibility). Don't remove "hard" ideas — only impossible ones.

**Step 2: Score remaining ideas on three dimensions:**

| Dimension | 1 (Low) | 3 (Medium) | 5 (High) |
|-----------|---------|------------|----------|
| **Impact** | Moves the metric <5% | Moves it 5-15% | Moves it >15% |
| **Confidence** | Pure hypothesis, no evidence | Some analogous evidence | Data or research supports it |
| **Effort** | >2 weeks engineering | 3-5 days | <2 days or no-code |

**Composite score:** Impact × Confidence × (6 - Effort) — penalizes high effort, rewards high confidence.

**Step 3: Present as a ranked table.** Top 5-7 ideas with scores and one-line rationale for each score.

### Propsoch-Specific Filters

Before scoring, check each idea against:
- Does this work on mobile? (92% of traffic)
- Does this work within the existing Next.js + React stack?
- Does this require new data we don't have?
- Does this create ops burden? (33-person team)
- Does this move us toward product-led (30/70 target)?
- Does this work for both Bangalore and Mumbai?

### Output
Ranked table of top 5-7 ideas with Impact/Confidence/Effort scores.

---

## Stage 4: CONVERGE

### Goal
Select the top 3 ideas and turn them into testable hypotheses with experiment designs.

### Process

**Step 1: Select top 3.** One high-confidence quick win, one medium-effort high-impact bet, one ambitious swing. This portfolio balances certainty with upside.

**Step 2: Write a hypothesis for each:**

```
IF we [specific change]
THEN [specific metric] will improve by [estimated %]
BECAUSE [user behavior insight or design principle]
MEASURED BY [Mixpanel event or A/B test metric]
WITHIN [timeframe to see signal]
```

**Step 3: Design the experiment for each:**
- What's the control (current experience)?
- What's the variant (the change)?
- What sample size / duration is needed? (Use Propsoch's traffic numbers.)
- What's the primary metric? What's the guardrail metric?
- What result would make you ship vs iterate vs kill?

**Step 4: Identify dependencies and sequence.**
- Can these run in parallel or must they be sequential?
- What needs to be true before each experiment can start?
- Who owns implementation? Who owns analysis?

### Output
Three experiment cards, each with hypothesis, design, metrics, timeline, and owner.

---

## Interactive Rules

- **One stage at a time.** Present Stage 1 output, get Ravi's direction, then proceed to Stage 2. Don't run all four stages without checkpoints.
- **Lead with recommendation.** "I'd prioritize HMW #2 and #5. Here's why:" — not "which HMW questions interest you?"
- **Quantity beats quality in Stage 2.** Don't self-censor. Generate 20 ideas and let Stage 3 filter.
- **Be specific.** Not "improve the CTA" — "Change the phone step heading from 'Enter Phone Number' to 'Where should we WhatsApp your advisor match?'"
- **Include the smallest possible version.** For every ambitious idea, also state: "The smallest test of this would be..."
- **Cross-industry is mandatory.** At least 3 analogies from other industries in Stage 2. This is where non-obvious ideas come from.

## Propsoch Context (Always Loaded)

When brainstorming for Propsoch, these constraints and context are always active:
- Mobile-first (92% of traffic from mobile ads)
- Next.js + React + framer-motion frontend stack
- 33-person team, 3 frontend engineers (Sukrit, Ravi Anand, Amaan)
- Signup form is 8 steps with 3 conditional exits to WhatsApp Community
- Buyer personas: business families (55-60%), corporate professionals (24-30%), independent professionals (10-15%)
- BLR mature (16-28 homes/month), Mumbai new (building from 0)
- CRM is Zoho, analytics is Mixpanel + GA4, ads are Meta + Google Display + Search
- 90/10 service/product mix targeting 30/70 by EOY 2026

## Lenny's Archive References

When brainstorming touches these domains, check the relevant transcripts:

| Domain | Key Guests | Episode Focus |
|--------|-----------|---------------|
| Opportunity mapping | Teresa Torres | Opportunity Solution Trees, continuous discovery |
| Jobs To Be Done | Bob Moesta | Job switching forces, demand generation |
| First principles | Shishir Mehrotra, Keith Yandell | Decomposition, constraint-driven thinking |
| Product craft | Shreyas Doshi | Pre-mortems, high-leverage activities |
| Growth/conversion | Elena Verna, Gustaf Alstromer | PLG, experimentation, brainwriting |
| Design sprints | Jake Knapp | Structured rapid prototyping |
| Cross-industry | Scott Belsky | First mile experience, messy middle patterns |
| Pricing/packaging | Madhavan Ramanujam | Willingness to pay, monetization experiments |

## Completion Summary

```
+====================================================================+
|            /brainstorm — COMPLETION SUMMARY                        |
+====================================================================+
| Problem              | [one sentence]                              |
| HMW Questions        | [N] generated, [N] selected                 |
+--------------------------------------------------------------------+
| Ideas Generated      | [N] total across [N] HMW questions          |
| Techniques Used      | [list: OST, 10-Star, Analogies, etc.]       |
| Cross-Industry       | [N] analogies from [industries]             |
+--------------------------------------------------------------------+
| Top Ideas            | [N] after evaluation                        |
| Quick Win            | [name] — Impact: X, Effort: X               |
| High-Impact Bet      | [name] — Impact: X, Effort: X               |
| Ambitious Swing      | [name] — Impact: X, Effort: X               |
+--------------------------------------------------------------------+
| Experiments Designed  | [N] with hypotheses + metrics               |
| Total Effort Est.    | [days/weeks]                                |
| Dependencies         | [list blocking items]                       |
+====================================================================+
```
