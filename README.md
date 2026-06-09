# Propsoch Skills

Internal Claude Code skills for the Propsoch team, distributed as a plugin marketplace. Install once, get updates by re-syncing the marketplace.

## Skills

| Skill | What it does |
|---|---|
| **leadpages-landing-page** | Builds Propsoch marketing landing pages for LeadPages (HTML Pub) that follow the Propsoch design system — brand colors, Archivo typography, spacing tokens, `max-w-7xl`, mobile-responsive. Walks you from page purpose → section flow (Mermaid) → finished standalone HTML. |

## Install (Claude Code)

From within Claude Code, add the marketplace once:
```
/plugin marketplace add Thinkr-proptech-private-limited/propsoch-skills
```

Then install the skill:
```
/plugin install leadpages-landing-page@propsoch-skills
```

The skill is now available across all your projects. Invoke it by asking, e.g.:
> "Make a Propsoch LeadPages landing page for our Bangalore home-buying campaign."

> **Private repo:** authenticate `gh`/git to the `Thinkr-proptech-private-limited` org first, or Claude Code can't clone the marketplace.

## Getting updates

When this repo is updated, pull the latest into your installed copy:
```
/plugin marketplace update propsoch-skills
```
Then reload (`/plugin` → update the plugin if prompted). New token values, sections, or fixes flow through automatically — no reinstall needed.

## What's inside `leadpages-landing-page`

```
skills/leadpages-landing-page/
├── SKILL.md                     # behavior: purpose → diagram → edit → build → publish
└── references/
    ├── tokens.css               # full Propsoch DS @theme (colors + type + spacing), verbatim
    ├── colors.md                # semantic color classes (double-prefix rule)
    ├── typography.md            # title/para/label class strings
    ├── sections.md              # canonical section library + default flow + brand voice
    ├── base-template.html       # standalone page skeleton (navbar/footer/sticky CTA)
    └── logos/                   # 5 brand logo SVGs
```

### Design rules the skill enforces
- Content width capped at `max-w-7xl` (1280px).
- Mobile-first; `lg:` (1024px) for desktop.
- Colors only via baked semantic tokens (`bg-bg-*`, `text-text-*`, `border-border-*`).
- Typography only via the Archivo-based `title`/`para`/`label` scale.

### How the CSS works (no build step)
Pages load the **Tailwind v4 browser CDN** and inline `tokens.css` inside `<style type="text/tailwindcss">`. Every design-system utility resolves in the browser, so the HTML is fully standalone and portable to LeadPages.

> ⚠ Tailwind v4 emits the **literal** token name. A token `--color-bg-brand-orange-normal` becomes the class `bg-bg-brand-orange-normal` (double prefix). This is intentional — see `references/colors.md`.

## Maintaining
Tokens are copied verbatim from `propsoch-fe-v3/src/styles/*`. When the design system changes there, regenerate `tokens.css`, bump the `version` in `.claude-plugin/marketplace.json` + `plugin.json`, and push. Installed users pick it up via `/plugin marketplace update`.

## License
MIT
