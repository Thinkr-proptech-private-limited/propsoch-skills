# Firmwide AI Agent Style Guides

Six codified experts for startups (6-10 engineers) that lean hard on AI-generated code and need guardrails: code quality, credential hygiene, and review discipline. Each expert operates in two modes — **Architecture** (design, options, trade-offs) and **Review** (severity-ranked findings with an explicit verdict).

Version: 1.0.0 (2026-07-19)

## Layout

```
agents/
  baseline/FIRMWIDE_BASELINE.md   # shared rules: secrets, AI-code policy, severity, modes — EDIT HERE
  guides/*.md                      # six role guides — EDIT HERE
  dist/*.md                        # generated self-contained bundles — DISTRIBUTE THESE, never edit
  build.sh                         # baseline + guide → dist. Run after every edit.
```

Rule: **edit source, ship dist.** A dist file always contains the full baseline, so no agent ever runs without the security rules. If you paste a `guides/` file somewhere directly, you have shipped an agent with no credential guardrails — that is the one misuse this layout exists to prevent.

## Using the agents

- **Claude Code**: wrappers in `.claude/agents/` invoke each expert as a subagent. Copy `agents/` + `.claude/agents/` into your repo root.
- **Cursor / Windsurf / API / claude.ai**: paste the relevant `dist/*.md` file as the system prompt or project instructions. One file, complete.
- After editing any source file: `./agents/build.sh`, commit source + dist together.

## Operating pipeline — who runs when

| Stage | Agent | Trigger | Output |
|---|---|---|---|
| 1. Problem + spec | product-manager | New initiative | Spec per its artifact contract |
| 2. Spec review | technical-senior-pm (+ analytics-expert for metrics) | Spec drafted | Verdict on the spec |
| 3. Tracking plan | analytics-expert | Spec approved | Tracking plan, PII-classified |
| 4. Architecture proposal | nextjs-engineer / nodejs-backend-engineer | Spec approved | 2-3 options + recommendation |
| 5. Architecture review | technical-senior-pm (contracts, arbitration) + playwright-qa-engineer (test strategy) | Proposal drafted | Contract approval + test plan |
| 6. PR review (every PR) | Matching engineer agent + playwright-qa-engineer; analytics-expert when events/SQL change | PR opened | Verdict: APPROVE / REQUEST CHANGES / BLOCK |
| 7. Pre-release | playwright-qa-engineer | Release candidate | E2E green + flake report |
| 8. Post-release | analytics-expert | Shipped | Metric readout vs the spec's goal |

Minimum viable adoption: stage 6 only. Add stages 1-5 as the team feels the pain of skipping them.

## Human AI-usage policy

The agents enforce rules on artifacts. These five rules bind the humans:

1. AI-generated code is untrusted input. You own every line you merge; if you can't explain a line, you don't merge it.
2. An agent BLOCKER verdict stops the merge. Overriding one requires a second human and a written reason in the PR.
3. Never paste secrets, customer data, or production credentials into any AI tool. Use placeholders.
4. Mechanical gates are not optional and agents do not replace them (see below).
5. Keep AI-assisted PRs under 400 changed lines. Split otherwise.

## Mechanical enforcement — install before the agents

Agents are the second layer of defense. Layer one is mechanical:

- [ ] gitleaks (or trufflehog) in pre-commit **and** CI
- [ ] `.env*` in `.gitignore`, verified by a CI check
- [ ] Branch protection: no direct pushes to main, ≥1 human review required
- [ ] CI required checks: lint, type check (`tsc --noEmit` with checkJs for JS repos), tests
- [ ] Committed lockfile + `npm audit` in CI + Renovate/Dependabot

Every agent will file a MAJOR finding when it detects one of these missing. That is by design.

## Versioning

Bump `Version:` in the baseline (and the affected guide), run `build.sh`, note the change below.

### Changelog
- 1.0.0 (2026-07-19) — initial release: baseline + 6 role guides + dist pipeline.
