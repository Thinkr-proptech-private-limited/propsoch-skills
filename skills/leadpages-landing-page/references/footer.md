# Footer reference

The canonical Propsoch campaign footer (from `src/app/campaigns/_shared/components/footer.tsx`). Dark background, centered on mobile → row layout on desktop, ending with a large "Propsoch" watermark. Reuse this structure; swap copy/links per page.

## Structure (top → bottom)

1. **Logo + tagline** — white icon+text logo (see `logos.md`), then a short tagline.
2. **Social row + legal entity block** — social icon links; below them the registered entity name, RERA, GSTIN, CIN.
3. **Divider** — thin neutral separator.
4. **Bottom bar** — legal nav (Privacy, Terms) on the left, copyright on the right.
5. **Watermark** — oversized "Propsoch" wordmark, orange→dark gradient, decorative.

## Layout rules
- Footer bg: `.bg-neutral-strongest` (#212130). All text uses inverted/light tones (`.text-neutral-inverted`, or inverted at reduced opacity for secondary lines).
- Inner container: centered, `max-width:80rem; margin-inline:auto; padding:3.5rem 1rem;` (→ `padding-top:6rem; padding-bottom:1.5rem;` on desktop).
- Mobile-first: stack + center (`flex-direction:column; align-items:center;`). Desktop `@media (min-width:1024px)`: row + left-align.
- Legal text is small/quiet: `.label-small` / `.label-xsmall` at lower opacity.

## Real legal lines (use verbatim)
- Entity: **Thinkr Proptech Private Limited**
- RERA: **PRM/KA/RERA/1251/446/AG/220927/003103**
- GSTIN: **29AAJCT2519D1ZC** · CIN: **21312215151661**
- Tagline: *"Propsoch is the most advanced real estate research platform for homebuyers in India."*
- Legal links: Privacy Policy (`/meta/privacy`), Terms & Conditions (`/meta/terms`).
- Copyright: `© Copyright Propsoch <year>`.

## HTML pattern (plain CSS, skill classes)

```html
<footer class="bg-neutral-strongest" role="contentinfo" style="width:100%;">
  <div class="footer-inner">
    <!-- top: logo+tagline  |  social + legal entity -->
    <div class="footer-top">
      <div class="footer-brand">
        <!-- white icon+text logo from the brand kit (see logos.md) -->
        <img src="{{LOGO_WHITE_URL}}" alt="Propsoch" style="height:48px;width:auto;" />
        <p class="para-xsmall text-neutral-inverted" style="max-width:20rem;opacity:.8;">
          Propsoch is the most advanced real estate research platform for homebuyers in India
        </p>
      </div>

      <div class="footer-legal">
        <ul class="footer-social">
          <li><a href="#" aria-label="Follow Propsoch">{{SOCIAL_ICON}}</a></li>
          <!-- repeat per network -->
        </ul>
        <p class="label-small text-neutral-inverted">Thinkr Proptech Private Limited</p>
        <p class="label-small text-neutral-inverted" style="opacity:.6;">RERA: PRM/KA/RERA/1251/446/AG/220927/003103</p>
        <p class="label-xsmall text-neutral-inverted" style="opacity:.6;display:flex;gap:1rem;">
          <span>GSTIN - 29AAJCT2519D1ZC</span><span>CIN - 21312215151661</span>
        </p>
      </div>
    </div>

    <!-- divider + bottom bar -->
    <hr class="border-neutral-strong" style="border-top-width:1px;width:100%;opacity:.4;" />
    <div class="footer-bottom label-xsmall text-neutral-inverted" style="opacity:.6;">
      <nav class="footer-links" aria-label="Legal Links">
        <a href="/meta/privacy">Privacy Policy</a>
        <a href="/meta/terms">Terms &amp; Conditions</a>
      </nav>
      <span>&copy; Copyright Propsoch <span id="year"></span></span>
    </div>

    <!-- decorative watermark -->
    <div class="footer-watermark" aria-hidden="true">Propsoch</div>
  </div>
</footer>

<style>
  .footer-inner{max-width:80rem;margin-inline:auto;display:flex;flex-direction:column;align-items:center;gap:3rem;padding:3.5rem 1rem;}
  .footer-top,.footer-brand,.footer-legal{display:flex;flex-direction:column;align-items:center;gap:1rem;width:100%;}
  .footer-social{display:flex;justify-content:center;gap:1rem;list-style:none;padding:0;margin:0;}
  .footer-bottom{display:flex;flex-direction:column;align-items:center;gap:1rem;width:100%;}
  .footer-links{display:flex;gap:1.5rem;}
  .footer-watermark{
    width:100%;text-align:center;font-weight:700;line-height:1;user-select:none;
    font-size:3.5rem;background:linear-gradient(to bottom,var(--orange-70),var(--coolgrey-100));
    -webkit-background-clip:text;background-clip:text;color:transparent;
  }
  @media (min-width:1024px){
    .footer-inner{gap:6rem;padding-top:6rem;padding-bottom:1.5rem;}
    .footer-top,.footer-brand{flex-direction:row;align-items:flex-start;justify-content:space-between;}
    .footer-brand{align-items:flex-start;text-align:left;}
    .footer-bottom{flex-direction:row;justify-content:space-between;}
    .footer-watermark{font-size:12rem;}
  }
</style>
```

> Use the **white** logo variant on this dark footer (`logos.md`). The watermark gradient uses palette vars `--orange-70 → --coolgrey-100` from `colors.css`. Set the year via tiny inline JS (`document.getElementById('year').textContent=new Date().getFullYear()`) or hardcode it.
