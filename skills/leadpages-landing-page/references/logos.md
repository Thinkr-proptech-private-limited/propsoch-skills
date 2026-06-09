# Propsoch logos (in the LeadPages brand kit)

These logos **already exist in the Propsoch LeadPages brand kit** — do not re-upload or inline raw SVG. Reference the brand-kit asset when placing a logo on a page (e.g. via the brand kit's logo URL, or pick the matching asset in the LeadPages editor).

Brand kit: **Propsoch** (default). Primary `#FF6D33`, secondary `#9A4AFB`, text `#212130`.

## Default logo

Unless the user asks for a different one, **always use the colored icon+text lockup** (`propsoch-logo-icon-text-colored.svg`) as the default logo everywhere a logo/icon is placed — navbar, headers, sections. Only switch variants when the user explicitly requests it, or when contrast demands it (e.g. dark/photo background → white variant). Do not pick a different default on your own.

## Brand-kit asset IDs (live)

The 5 logos are uploaded to the Propsoch brand kit (org `Ravi Agrawal`, kit `n1hwa30u1fv4tncdqap7up2s`). Each resolves as an SVG at:

```
https://ravi-agrawal-en9p.pubhtml.com/api/library/<ID>
```

| Variant | viewBox | asset ID |
|---|---|---|
| **Icon + text — colored ★ DEFAULT** | 463×107 | `ko9khmspbelvefuv430rnjdu` |
| Icon (orange "P") | 34×32 | `h86n977fkmb0hng7oti2jc2h` |
| Icon — white | 24×24 | `ofhn7pbhpav0sjwhuelpxctl` |
| Icon + text — mono `#212130` | 139×32 | `jwrre2wvqwz69atnshmg32af` |
| Wordmark | 100×22 | `n7f0s7kegjn48j6c884nevkg` |

Default logo URL (drop into `<img src>`):
`https://ravi-agrawal-en9p.pubhtml.com/api/library/ko9khmspbelvefuv430rnjdu`

> IDs are tied to this brand kit. If a logo 404s, re-list via `get_brand_kit` → `uploadedAssets.logos`, then fetch each `/api/library/<id>` and match by viewBox (above) to re-map.

## Variants

| Logo | Composition | Colors | Use on |
|---|---|---|---|
| **Icon** | "P" mark only | orange `#FF6D33` | favicon, compact/mobile nav, square avatars, social |
| **Icon — white** | "P" mark only | white | dark / orange / photo backgrounds where the orange mark lacks contrast |
| **Wordmark** | "Propsoch" text only | orange + white | when the mark is already shown elsewhere, or tight horizontal space |
| **Icon + text** | mark + "Propsoch" | monochrome `#212130` | mono contexts, light backgrounds, print, watermark |
| **Icon + text — colored** | mark + "Propsoch" | orange `#FF6D33` + dark `#212130` | **primary navbar logo** — default brand lockup on white/light bg |

## Picking a logo

- **Navbar (light bg):** Icon + text — colored (primary lockup).
- **Navbar / header (dark or orange bg):** Icon — white, or the wordmark in white.
- **Footer (dark bg, `bg-neutral-strongest`):** Icon — white, or Icon + text in white.
- **Favicon / tiny:** Icon (orange) or Icon — white per background.
- **Mono / print:** Icon + text (monochrome `#212130`).

## Rules
- Don't recolor outside the brand palette; use the white variant for contrast, not a custom tint.
- Keep clear space ≈ the height of the mark around the lockup.
- Maintain aspect ratio — never stretch.
- On busy photos, prefer the white variant over the colored lockup.
