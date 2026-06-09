# Typography cheat-sheet (NEW design system)

From `font.style.ts`. Three roles: **title** (headings, 110% LH), **para** (body, 140% LH), **label** (UI text, 110% LH). All sizes are **mobile-first**; `lg:` (≥1024px) switches to desktop. Font family = **Archivo** (set on `<body>` in the template).

> Paste the class string verbatim into the element's `class`. The `var(--font-size-*)` / `var(--font-weight-*)` refer to vars defined in `tokens.css` — they resolve at runtime via the Tailwind CDN.

## title — headings (`leading-[110%]`)

Add `leading-[110%]` once on the element, then one size class:

| variant | mobile→desktop px | weight | class string |
|---|---|---|---|
| xxlarge | 32 → 64 | 400 | `text-[length:var(--font-size-mobile-base-plus-7)] lg:text-[length:var(--font-size-base-plus-7)]` |
| xlarge | 32 → 40 | 400 | `text-[length:var(--font-size-mobile-base-plus-6)] lg:text-[length:var(--font-size-base-plus-6)]` |
| large | 24 → 32 | 400 | `text-[length:var(--font-size-mobile-base-plus-5)] lg:text-[length:var(--font-size-base-plus-5)]` |
| medium | 22 → 24 | 500 | `text-[length:var(--font-size-mobile-base-plus-4)] lg:text-[length:var(--font-size-base-plus-4)] font-[var(--font-weight-medium)]` |
| small | 20 → 22 | 500 | `text-[length:var(--font-size-mobile-base-plus-3)] lg:text-[length:var(--font-size-base-plus-3)] font-[var(--font-weight-medium)]` |
| xsmall | 16 → 18 | 500 | `text-[length:var(--font-size-mobile-base-plus-2)] lg:text-[length:var(--font-size-base-plus-2)] font-[var(--font-weight-medium)]` |
| xxsmall | 14 → 16 | 500 | `text-[length:var(--font-size-mobile-base-plus-1)] lg:text-[length:var(--font-size-base-plus-1)] font-[var(--font-weight-medium)]` |

xxlarge/xlarge/large are weight 400 (apply nothing or `font-[var(--font-weight-regular)]`). For bolder hero, add `font-[var(--font-weight-semibold)]` (real Propsoch hero does this).

## para — body text (`leading-[140%]`)

Add `leading-[140%]` once, then one class. `-strong` = weight 500, else 400.

| variant | mobile→desktop px | class string |
|---|---|---|
| xsmall | 10 → 12 | `text-[length:var(--font-size-mobile-base-minus-1)] lg:text-[length:var(--font-size-base-minus-1)] font-[var(--font-weight-regular)]` |
| small | 12 → 14 | `text-[length:var(--font-size-mobile-base-0)] lg:text-[length:var(--font-size-base-0)] font-[var(--font-weight-regular)]` |
| medium | 14 → 16 | `text-[length:var(--font-size-mobile-base-plus-1)] lg:text-[length:var(--font-size-base-plus-1)] font-[var(--font-weight-regular)]` |
| large | 16 → 18 | `text-[length:var(--font-size-mobile-base-plus-2)] lg:text-[length:var(--font-size-base-plus-2)] font-[var(--font-weight-regular)]` |

`-strong` variants: identical size classes, swap `--font-weight-regular` → `--font-weight-medium`.

## label — UI text, captions, eyebrows (`leading-[110%]`)

| variant | mobile→desktop px | class string |
|---|---|---|
| xxsmall | 9 → 10 | `text-[length:var(--font-size-mobile-base-minus-2)] lg:text-[length:var(--font-size-base-minus-2)] font-[var(--font-weight-regular)]` |
| xsmall | 10 → 12 | `text-[length:var(--font-size-mobile-base-minus-1)] lg:text-[length:var(--font-size-base-minus-1)] font-[var(--font-weight-regular)]` |
| small | 12 → 14 | `text-[length:var(--font-size-mobile-base-0)] lg:text-[length:var(--font-size-base-0)] font-[var(--font-weight-regular)]` |
| medium | 14 → 16 | `text-[length:var(--font-size-mobile-base-plus-1)] lg:text-[length:var(--font-size-base-plus-1)] font-[var(--font-weight-regular)]` |
| large | 16 → 18 | `text-[length:var(--font-size-mobile-base-plus-2)] lg:text-[length:var(--font-size-base-plus-2)] font-[var(--font-weight-regular)]` |

`-strong` variants: swap `--font-weight-regular` → `--font-weight-medium`.

## Weights

`--font-weight-regular` 400 · `--font-weight-medium` 500 · `--font-weight-semibold` 600 · `--font-weight-bold` 700.

## Mapping to HTML

- Page H1 / hero → `title` xxlarge or xlarge
- Section heading (H2) → `title` large / medium
- Card title (H3) → `title` small / xsmall
- Body paragraph → `para` medium
- Fine print / disclaimer → `para` xsmall or `label` small
- Eyebrow / tag / badge → `label` small-strong (uppercase optional via `uppercase tracking-wide`)
