# Propsoch Skills

Claude Code skills for the Propsoch team, distributed as a plugin marketplace.

## leadpages-landing-page

Builds Propsoch marketing landing pages for LeadPages that follow the Propsoch design system (brand colors + Archivo typography as plain CSS, 1280px max width, mobile-responsive). Walks you from page purpose → section wireframe → finished HTML.

## critique

Stress-test product specs, PRDs, and design decisions before committing engineering resources. Uses structured frameworks (pre-mortem, assumption mapping, four-risk analysis) to surface blind spots. Ravi's favourite — run it in loops with `/prd` until every line has been challenged.

## prd

Co-author, review, or edit PRDs with the rigour of a prolific product leader. Grounded in Propsoch's context and startup pragmatism. Use with a doc link to find what's missing.

## decide

Structured decision support for product, design, and engineering choices. Given enough context it walks you through an options matrix, key trade-offs, and a clear recommendation with confidence level.

## brainstorm

Four-stage diverge→converge ideation engine. Generates non-obvious solutions using Opportunity Solution Trees, How Might We reframing, and constraint-driven thinking. Assumes the problem is already understood.

## rca

Root cause analysis for bugs, metric drops, or business anomalies. Pulls data from multiple sources, self-critiques its own conclusions before presenting findings, and structures a clear investigation report.

## research

Deep-dive research on any topic. Comprehensive, structured, with clear sourcing. Use for market research, competitor analysis, or any topic that needs thorough coverage.

## Install in Claude Code

**1. Add the marketplace:**
```
/plugin marketplace add Thinkr-proptech-private-limited/propsoch-skills
```

**2. Install a skill:**
```
/plugin install leadpages-landing-page@propsoch-skills
/plugin install critique@propsoch-skills
/plugin install prd@propsoch-skills
/plugin install decide@propsoch-skills
/plugin install brainstorm@propsoch-skills
/plugin install rca@propsoch-skills
/plugin install research@propsoch-skills
```

**3. Verify:** run `/plugin` and confirm `leadpages-landing-page` is listed (restart Claude Code if not).

**4. Use it:** in any project, ask — *"Make a Propsoch LeadPages landing page for our Bangalore campaign."*

## Update

```
/plugin marketplace update propsoch-skills
```

## License

MIT
