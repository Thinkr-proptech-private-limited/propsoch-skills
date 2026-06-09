---
name: leadpages-landing-page
description: Use when building, generating, or designing a Propsoch marketing landing page for LeadPages / HTML Pub, or any standalone marketing HTML page that must follow the Propsoch design system (brand colors, Archivo typography). Triggers on "make a landing page", "LeadPages page", "campaign page", "marketing page" in a Propsoch context.
license: MIT
---

# Propsoch LeadPages Landing-Page Builder

Build conversion-focused **marketing landing pages** for LeadPages (HTML Pub) that strictly follow the **Propsoch design system**. The design system ships as **plain CSS** (`references/colors.css` + `references/typography.css`) — no Tailwind, no build step, no runtime JS. Paste both files into the page's `<style>` and use the class names they define.

**Non-negotiable design rules** (enforce on every page):
1. Content width capped at **`max-w-7xl` = 1280px** — wrap every section's inner content in a centered container `max-width:80rem; margin-inline:auto; padding-inline:1rem;` (1rem mobile → 2rem desktop). A `.container-7xl` helper is fine.
2. **Mobile-first + responsive** — base styles target mobile; add `@media (min-width:1024px)` for desktop. The typography classes already do this. Never desktop-only.
3. **Colors only via `colors.css` classes** — `.bg-*`, `.text-*`, `.border-*`, `.icon-*` (see below). Never hand-write hex for UI.
4. **Typography only via `typography.css` classes** — `.title-*`, `.para-*`, `.label-*`. Font is Archivo (load via Google Fonts `<link>`).

## Workflow (follow in order)

### 1. Ask the purpose
Before anything else:
> "What landing page do you want? Tell me its **goal**, the **audience**, the **offer / primary CTA**, the **city/market**, and any tone preference."

Wait for the answer. Don't assume a layout yet.

### 2. Propose a section flow as a wireframe diagram
Pick a sensible sequence from the **section catalog** below and render it **in chat** as an **ASCII wireframe** — stacked boxes, top→down = page order, sketching each section's rough layout (columns, image vs text, button). One-line justification per section underneath. This shows the user the page shape, not just a list.

```
┌──────────────────────────────────────────────┐
│ [logo]                          [ CTA button ] │  Navbar — sticky, logo + primary CTA
├──────────────────────────────────────────────┤
│                                                │
│   BIG HEADLINE                                 │  Hero — headline + subhead + CTA
│   subhead line                                 │       (dark/orange bg, inverted text)
│   [ Get a Callback Now ]                       │
│                                                │
├──────────────────────────────────────────────┤
│   ★★★★★  4.9   |  2000+ homes  |  Google      │  Trust — ratings / counts
├──────────────────────────────────────────────┤
│   Why Propsoch                                 │
│   ┌────┐   ┌────┐   ┌────┐                     │  USP grid — 1-col mobile → 3-col desktop
│   │icon│   │icon│   │icon│                     │
│   └────┘   └────┘   └────┘                     │
├──────────────────────────────────────────────┤
│   “quote…”   “quote…”   “quote…”               │  Testimonials — quote cards (name, city)
├──────────────────────────────────────────────┤
│   1 ──→ 2 ──→ 3 ──→ 4                           │  How it works — numbered steps
├──────────────────────────────────────────────┤
│   Ready to start?        [ Book a call ]       │  CTA poster band — orange/dark
├──────────────────────────────────────────────┤
│   ▸ Question 1                                 │  FAQ — accordion (<details>)
│   ▸ Question 2                                 │
├──────────────────────────────────────────────┤
│ [logo]   links    contact    legal             │  Footer — dark bg, inverted text
└──────────────────────────────────────────────┘
        [ sticky CTA bar — mobile only ]
```

Adapt the boxes to the actual sections chosen for the brief — add/drop rows to match.

### 3. Edit loop
Ask: **"Add, remove, or reorder any section?"** Apply, re-draw the wireframe if changed, repeat until confirmed.

### 4. Build the page
- `<head>`: Archivo `<link>`, then `<style>` containing the **full contents of `references/colors.css` and `references/typography.css`**, then a tiny page `<style>` for layout helpers (e.g. `.container-7xl`).
- Each section: `<section class="bg-...">` → inner `<div class="container-7xl">` with `padding-block:3rem;` (→ `5rem` desktop).
- Alternate section backgrounds white ↔ `bg-neutral-surface` for separation.
- Colors: `colors.css` classes only. Typography: `typography.css` classes only.
- Logos: **default to `propsoch-logo-icon-text-colored.svg`** everywhere a logo/icon goes, unless the user asks for a different variant (or contrast forces the white one). Reference the brand-kit assets (see `references/logos.md`); don't inline SVG.
- Footer: paste `references/footer.css` into the page `<style>` and use its HTML pattern + real legal lines (RERA/GSTIN/CIN). Footer background is black.
- Buttons: paste `references/buttons.css` and use `.btn .btn-<variant> .btn-<size>` for every CTA (don't hand-style buttons).
- FAQ: paste `references/faq.css` and use its no-JS `<details>/<summary>` accordion pattern (eyebrow + heading + items + support banner).
- Brand voice: confident advisor, benefit-first, data-backed. E.g. *"The safest way to buy homes in {city}."* CTAs like *"Get a Callback Now"*, *"Book a free consultation"*. Indian market: phone-callback CTA beats email.

Generate the whole page, then iterate.

### 5. Output
Write the HTML to a file (default `~/Downloads/<slug>.html`) for review. Then **offer** to publish via the LeadPages MCP `create_page` — free-plan pages expire after 7 days. Don't publish without asking.

## Color classes (from colors.css)

Single-prefix, semantic. Strength: `weakest < weaker < weak < normal < strong < stronger < strongest`.

- **Backgrounds** `.bg-…`: `neutral-{white,surface,weakest,weaker,weak,normal,strong,stronger,strongest}` · `brand-orange-{weakest…strongest}` · `brand-purple-{…}` · `{positive,warning,negative,info}-{weakest…strongest}`
- **Text** `.text-…`: `neutral-{inverted,weakest,weak,normal,strong}` · `brand-orange-{weakest,weak,normal,strong}` · `brand-purple-{…}` · `{positive,warning,negative,info}-{weakest,weak,normal,strong}`
- **Borders** `.border-…` (set `border-style/width` too): `neutral-{white,weakest,weak,normal,strong}` · `brand-orange/purple-{weakest,weak,normal,strong}` · state hues
- **Icons** `.icon-…` (sets `color`): same families as text
- **Palette** (decorative/gradients): `.bg-orange-70`, `.text-purple-70`, `.border-coolgrey-30` … shades 10→100.

Anchors: orange-70 `#ff6d33` (primary CTA), orange-80 `#ff4b04` (accent), purple-70 `#9a4afb` (secondary), coolgrey-100 `#212130` (text), coolgrey-0 `#fff`.

## Typography classes (from typography.css)

- **Headings** `.title-{xxlarge,xlarge,large,medium,small,xsmall,xxsmall}` — 110% line-height, responsive (mobile→desktop). For a bolder hero add `font-weight:600`.
- **Body** `.para-{xsmall,small,medium,large}` (+ `-strong`) — 140% line-height.
- **UI/labels** `.label-{xxsmall,xsmall,small,medium,large}` (+ `-strong`) — 110% line-height.

Mapping: page H1/hero → `title-xxlarge`/`xlarge`; section H2 → `title-large`/`medium`; card H3 → `title-small`/`xsmall`; body → `para-medium`; fine print → `para-xsmall`; eyebrow/badge → `label-small-strong`.

## Section catalog

`navbar` (colored logo + CTA) · `hero` (headline + primary CTA, often dark/orange bg w/ `text-neutral-inverted`) · `trust / rating-grid` (ratings, review counts) · `featured-in` (press/partner logo strip) · `why-propsoch / USP grid` (3–6 icon cards, 1-col→3-col) · `feature / benefit blocks` (alternating image+copy) · `testimonials` (quote cards: avatar, name, city) · `process / how-it-works` (numbered steps) · `stats / counters` (big numbers) · `CTA poster band` (headline + button on orange/dark) · `FAQ` (use `references/faq.css` — no-JS `<details>`/`<summary>` accordion + support banner) · `lead-capture form` (name + phone + city) · `footer` (dark `bg-neutral-strongest`, inverted text) · `sticky / fixed CTA` (fixed bottom bar, mobile-only).

CTA buttons: use `references/buttons.css` classes — `.btn .btn-primary` (orange, default CTA), `.btn .btn-tertiary` (purple), `.btn .btn-outline` (bordered, on white), `.btn .btn-white` (on dark/photo bg). Size with `.btn-lg` / `.btn-xl`.

## Quick reference

| Need | Where |
|---|---|
| Color CSS + class names | `references/colors.css` |
| Typography CSS + class names | `references/typography.css` |
| Logo variants + when to use each | `references/logos.md` |
| Footer CSS + HTML pattern + real legal lines | `references/footer.css` |
| Button CSS + variants/sizes (primary/tertiary/outline…) | `references/buttons.css` |
| FAQ CSS + no-JS accordion HTML pattern | `references/faq.css` |

## Common mistakes

- **Hardcoding hex / font sizes** → use `colors.css` / `typography.css` classes so pages stay on-brand.
- **Forgetting to inline both CSS files** → no class resolves. Both must be in the page `<style>`.
- **Skipping the 1280px container** → content runs edge-to-edge on wide screens. Every section's inner div needs the `max-width:80rem` centered container.
- **Desktop-first** → build mobile first, layer `@media (min-width:1024px)`.
- **Inlining/re-uploading logos** → they're already in the brand kit; reference them (see `logos.md`).
- **Building before the user confirms sections** → always run steps 1–3 first.
