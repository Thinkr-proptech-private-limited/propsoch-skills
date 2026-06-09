# Color cheat-sheet (Propsoch semantic tokens)

## ⚠ The double-prefix rule (read first)

Tailwind v4 turns a `@theme` token into a utility by taking the **literal token name** after `--color-`. Our semantic tokens are already named `bg-…`, `text-…`, `border-…`, `icon-…`, so the generated classes carry the prefix twice:

| token in `tokens.css` | generated utility | use it as |
|---|---|---|
| `--color-bg-brand-orange-normal` | `bg-bg-brand-orange-normal` | `class="bg-bg-brand-orange-normal"` |
| `--color-text-neutral-strong` | `text-text-neutral-strong` | `class="text-text-neutral-strong"` |
| `--color-border-neutral-weak` | `border border-border-neutral-weak` | `class="border border-border-neutral-weak"` |
| `--color-icon-brand-orange-normal` | `text-icon-brand-orange-normal` | on SVG/icon `color` |

This is verified against the live repo (`text-text-neutral-normal` appears 160×, `bg-bg-neutral-white` 43×). **Always double-prefix.** A single-prefix class like `bg-brand-orange-normal` will NOT render.

Strength scale: `weakest < weaker < weak < normal < strong < stronger < strongest`.

## Most-used (the 90% set)

**Backgrounds**
- `bg-bg-neutral-white` — page/card white
- `bg-bg-neutral-surface` — light grey section bg
- `bg-bg-neutral-strongest` — near-black footer/section (#212130)
- `bg-bg-brand-orange-normal` — primary CTA button (#ff6d33)
- `bg-bg-brand-orange-weakest` — soft orange highlight block (#fff4ef)
- `bg-bg-brand-purple-weakest` — soft purple highlight block
- `bg-bg-positive-weakest` / `-normal`, `bg-bg-negative-*`, `bg-bg-info-*`, `bg-bg-warning-*` — state blocks

**Text**
- `text-text-neutral-strong` — primary heading text (#212130)
- `text-text-neutral-normal` — body text
- `text-text-neutral-weak` / `-weakest` — muted / captions
- `text-text-neutral-inverted` — white text on dark/orange (#ffffff)
- `text-text-brand-orange-normal` — orange emphasis / links
- `text-text-brand-purple-normal` — purple emphasis
- `text-text-positive-normal`, `text-text-negative-normal`, `text-text-info-normal` — state text

**Borders** (always pair with `border`)
- `border border-border-neutral-weakest` — hairline card border
- `border border-border-neutral-weak` / `-normal` — stronger dividers
- `border border-border-brand-orange-normal` — orange outline button/card

**Icons** (set on the icon's color/`text-`)
- `text-icon-neutral-normal`, `text-icon-neutral-weak`, `text-icon-brand-orange-normal`, `text-icon-positive-normal`, etc.

## Full token families (all available)

Each facet × hue × strength exists in `tokens.css`. Build any class as `<facet-prefix>-<token>`:

- **bg** (`bg-` + token): `bg-neutral-{white,surface,weakest,weaker,weak,normal,strong,stronger,strongest}` · `bg-brand-orange-{weakest,weaker,weak,normal,strong,stronger,strongest}` · `bg-brand-purple-{…same…}` · `bg-{positive,warning,negative,info}-{weakest,weaker,weak,normal,strong,stronger,strongest}`
- **text** (`text-` + token): `text-neutral-{inverted,weakest,weak,normal,strong}` · `text-brand-orange-{weakest,weak,normal,strong}` · `text-brand-purple-{weakest,weak,normal,strong}` · `text-{positive,warning,negative,info}-{weakest,weak,normal,strong}`
- **border** (`border ` + `border-` + token): `border-neutral-{white,weakest,weak,normal,strong}` · `border-brand-orange-{weakest,weak,normal,strong}` · `border-brand-purple-{…}` · `border-{positive,warning,negative,info}-{weakest,weak,normal,strong}`
- **icon** (`text-` + `icon-` token): `icon-neutral-{inverted,weakest,weak,normal,strong}` · `icon-brand-orange-{weakest,weak,normal,strong}` · `icon-brand-purple-{…}` · `icon-{positive,warning,negative,info}-{weakest,weak,normal,strong}`

So e.g. bg→ `bg-bg-positive-normal`, text→ `text-text-info-strong`, border→ `border border-border-brand-purple-weak`, icon→ `text-icon-negative-normal`.

## Direct palette (advanced / decorative only)

Base hues also generate plain utilities (single prefix, no double): `bg-orange-70`, `text-purple-70`, `border-coolgrey-30`, `from-orange-50`, `to-purple-60` (gradients). Shades 10→100 (light→dark). Prefer semantic tokens for UI; use palette only for gradients/illustration.

Brand anchors: orange-70 `#ff6d33` (primary), orange-80 `#ff4b04` (accent), purple-70 `#9a4afb` (secondary), coolgrey-100 `#212130` (text), coolgrey-0 `#ffffff`.

## Spacing (from spacing.css)

Vars `--spacing-base-*` (desktop) + `--spacing-mobile-base-*` (mobile). For LeadPages, prefer plain Tailwind spacing utilities (`px-4 lg:px-8`, `py-12 lg:py-20`, `gap-6`) — simpler than the var-based scale and fully supported by the CDN. Scale reference: base+2=16px, base+3=24px, base+4=32px, base+5=40px, base+6=48px, base+7=64px, base+8=80px, base+9=96px, base+10=120px (desktop).
