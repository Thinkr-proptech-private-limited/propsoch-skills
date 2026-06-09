# Canonical section library

Derived from real Propsoch landing pages (`src/app/campaigns/_shared/components/`, `(main)/nri/_components/`, `(home)/_components/`). Use these as the menu when proposing a section flow. Order below ≈ the proven default flow.

## Default flow (proven, GHB campaign)

```
navbar → hero → trust/rating-grid → featured-in → why-propsoch (USP)
→ feature/benefit blocks → testimonials → process (how-it-works)
→ stats/counters → CTA poster band → FAQ → footer  (+ sticky CTA overlay)
```

## Section catalog

| section | purpose | key content | notes |
|---|---|---|---|
| **navbar** | top bar | colored logo (left) + primary CTA button (right) | sticky optional; logo = `propsoch-logo-icon-text-colored.svg` |
| **hero** | first impression + primary CTA | H1 (title xxlarge/xlarge), subhead (para large), CTA button, supporting bullets w/ check icons | supports animated word-loop ("safest / verified / trusted way…"); often dark or orange bg w/ `text-text-neutral-inverted` |
| **trust / rating-grid** | instant credibility | star ratings, Google/MagicBricks counts, review badges | sits right under hero |
| **featured-in** | press / logo strip | greyscale partner/press logos in a row | horizontal scroll on mobile |
| **why-propsoch / USP grid** | differentiation | 3–6 cards: icon + title (title small) + para small | grid: 1-col mobile → 3-col `lg:` |
| **feature / benefit blocks** | deep-dive value | alternating image-left/right + copy + CTA | `flex-col lg:flex-row` alternating |
| **testimonials** | social proof | quote cards: avatar, name, city, quote (para medium) | carousel or grid; pull real city names |
| **process / how-it-works** | reduce friction | numbered steps (3–5): step badge + title + para | vertical on mobile, horizontal timeline `lg:` |
| **stats / counters** | quantified proof | big numbers + labels ("2000+ homes analyzed") | animated count-up optional |
| **CTA poster band** | mid-page conversion | bold headline + button on brand-orange or dark bg | `ReadyToStartPoster` equivalent |
| **FAQ accordion** | objection handling | expandable Q/A pairs | use `<details>`/`<summary>` for no-JS accordion |
| **lead-capture form** | collect details | name + phone + city fields → submit | phone is primary field for Indian market |
| **footer** | close | logo, links, contact, legal, social | dark `bg-bg-neutral-strongest` + inverted text |
| **sticky / fixed CTA** | persistent conversion | fixed bottom bar (mobile) w/ phone/CTA | `fixed bottom-0` mobile-only via `lg:hidden` |

## Layout rules (all sections)

- Content wrapper: `max-w-7xl mx-auto px-4 lg:px-8` (hard rule — 1280px max width).
- Vertical rhythm: `py-12 lg:py-20` per section (tune per density).
- Mobile-first: single column default, `lg:` (1024px) introduces multi-column.
- Section bg alternates white ↔ `bg-bg-neutral-surface` for visual separation.

## Brand voice (from real copy)

Confident advisor, benefit-first, plain language, data-backed. Not pushy-broker.
Examples: *"The safest way to buy homes in {city}."* · *"Unbiased, data-backed property advice."* · CTAs like *"Get a Callback Now"*, *"Book a free consultation"*.

## CTA conventions

- Primary button: `bg-bg-brand-orange-normal text-text-neutral-inverted` + `rounded-lg px-6 py-3` + `title xxsmall`/`label medium-strong`.
- Secondary: `border border-border-brand-orange-normal text-text-brand-orange-normal bg-transparent`.
- Indian market: phone-callback CTA outperforms email; lead the form with phone.
