# Propsoch Skills

Internal Claude Code skills for the Propsoch team, distributed as a plugin marketplace. Install once, get updates by re-syncing the marketplace.

## Skills

| Skill | What it does |
|---|---|
| **leadpages-landing-page** | Builds Propsoch marketing landing pages for LeadPages (HTML Pub) that follow the Propsoch design system — brand colors + Archivo typography as **plain CSS** (no build step), 1280px max width, mobile-responsive. Walks you from page purpose → section-flow wireframe → finished standalone HTML. |

## Install (Claude Code)

**Step 0 — one-time: authenticate to the org.** This repo is private, so Claude Code must be able to clone it. In your terminal:
```
gh auth login
```
Pick GitHub.com → HTTPS → your account in the `Thinkr-proptech-private-limited` org. (Already logged in? `gh auth status` to confirm.)

**Step 1 — add the marketplace.** Inside Claude Code, run:
```
/plugin marketplace add Thinkr-proptech-private-limited/propsoch-skills
```
This registers the repo as a plugin source (clones it locally).

**Step 2 — install the skill:**
```
/plugin install leadpages-landing-page@propsoch-skills
```

**Step 3 — verify.** Run `/plugin` and confirm `leadpages-landing-page` is listed/enabled. (Restart Claude Code if it doesn't appear.)

**Step 4 — use it.** In any project, just ask:
> "Make a Propsoch LeadPages landing page for our Bangalore home-buying campaign."

The skill activates automatically and walks you through purpose → wireframe → build.

## Getting updates

When this repo is updated, pull the latest into your installed copy:
```
/plugin marketplace update propsoch-skills
```
New colors, typography, or fixes flow through automatically — no reinstall needed.

## What's inside `leadpages-landing-page`

```
skills/leadpages-landing-page/
├── SKILL.md                # behavior: purpose → diagram → edit → build → publish
└── references/
    ├── colors.css          # Propsoch palette + semantic color classes (plain CSS)
    ├── typography.css       # Archivo title/para/label classes (plain CSS, responsive)
    └── logos.md            # the 5 brand-kit logos + when to use each
```

### Design rules the skill enforces
- Content width capped at **1280px** (`max-w-7xl`).
- Mobile-first; `@media (min-width:1024px)` for desktop.
- Colors only via `colors.css` classes (`.bg-*`, `.text-*`, `.border-*`, `.icon-*`).
- Typography only via `typography.css` classes (`.title-*`, `.para-*`, `.label-*`).

### How the CSS works (no build step)
The design system ships as **plain CSS** — `colors.css` and `typography.css` define CSS variables plus ready-to-use utility classes. Paste both into the page's `<style>` and use the class names. No Tailwind, no CDN, no runtime JS — fully standalone and portable to LeadPages.

### Logos
The 5 Propsoch logo variants already live in the **LeadPages brand kit**. The skill references them rather than inlining SVG — see `references/logos.md` for which variant to use where.

## Maintaining
`colors.css` / `typography.css` values are copied verbatim from `propsoch-fe-v3/src/styles/*`. When the design system changes there, regenerate them, bump `version` in `.claude-plugin/marketplace.json` + `plugin.json`, and push. Installed users pick it up via `/plugin marketplace update`.

## License
MIT
