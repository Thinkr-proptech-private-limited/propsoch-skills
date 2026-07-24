# Agent Style Guides — Install

Six codified AI experts (Next.js, Node.js backend, Playwright QA, PM, Technical Senior PM, Analytics) with a shared security/quality baseline. Full documentation: `agents/README.md`.

## Install into your repo (Claude Code)

1. Copy `agents/` and `.claude/agents/` from this package into your repository root.
2. Verify: open Claude Code in the repo and invoke any agent, e.g. "use the nodejs-backend-engineer agent to review this PR." The agent reads its bundle from `agents/dist/` — if it reports the bundle missing, step 1 was incomplete.
3. Install the mechanical enforcement checklist from `agents/README.md` (gitleaks, branch protection, CI gates). The agents assume it and will flag gaps.

## Install anywhere else (Cursor, Windsurf, API, claude.ai)

Paste the relevant `agents/dist/<role>.md` file as the system prompt or project instructions. Always use `dist/` files — they are self-contained (baseline + role guide). Never paste a `guides/` file directly; it lacks the security baseline.

## Modifying rules

Edit `agents/baseline/` or `agents/guides/`, then run `./agents/build.sh` and commit source + dist together. Never edit `dist/` by hand.
