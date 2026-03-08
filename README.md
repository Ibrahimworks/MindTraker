# MindTrack — Landing Page

Single-file marketing landing page for the MindTrack app. No framework, no build tool, no dependencies. Just HTML, CSS, and vanilla JS.

---

## App Download Link

> **Coming soon — link will be added here.**

Once available, replace every instance of `href="#"` on `.btn-primary` buttons with the real store URL.

---

## Stack

- **HTML5** — semantic structure
- **CSS3** — custom properties, grid, flexbox, keyframe animations
- **Vanilla JS** — mood interaction only (~15 lines)
- **Google Fonts** — `Syne` (headings) + `DM Sans` (body), loaded via `<link>`

No npm. No bundler. No runtime dependencies.

---

## File Structure

```
mindtrack-website.html   ← everything lives here
README.md                ← you are here
```

Intentionally kept as a single file for portability — drop it on any static host with zero configuration.

---

## Assets

Both logos are embedded as base64 directly inside the HTML. No external image files or CDN needed — the page is fully self-contained and works offline.

| Asset | Format | Used in |
|---|---|---|
| App logo (brain) | JPG → base64 | Navbar, phone mockup, footer brand |
| SaturnKM logo | PNG → base64 | Footer credit, CTA section |

---

## Sections

| Section | Selector | Description |
|---|---|---|
| Navigation | `nav` | Fixed navbar, blur backdrop, links, CTA button |
| Hero | `.hero` | Full-height hero, animated phone mockup, floating stat cards |
| Stats bar | `.stats-bar` | 4 market context numbers |
| Features | `#features` | 6 feature cards + live interactive mood check-in |
| How it works | `#how` `.steps-section` | 4-step flow with progress card visual |
| Pricing | `#pricing` `.pricing-wrap` | Free / Pro / Store Items tiers |
| Revenue model | `.sec` (revenue) | 4 revenue stream cards |
| CTA | `#download` `.cta-sec` | Final download call to action |
| Footer | `footer` | Brand, tagline, legal |

---

## Design Tokens

All colors are CSS custom properties at the top of the `<style>` block:

```css
:root {
  --bg: #09090f;
  --surface: #111120;
  --surface2: #16162a;
  --purple: #7c5cfc;
  --purple-light: #a78bfa;
  --purple-glow: rgba(124,92,252,0.18);
  --green: #22d3a5;
  --text: #f0eeff;
  --muted: #8b8aaa;
  --border: rgba(124,92,252,0.15);
}
```

Change the palette here and it propagates everywhere.

---

## Animations

All animations are pure CSS — no JS involved:

| Name | Used on |
|---|---|
| `fadeUp` | Hero heading, subtext, buttons, phone mockup |
| `floatL / floatR` | Floating stat cards around the phone |
| `pulse` | Green live dot in the hero badge |

Entrance animations use `animation-delay` to stagger elements on load.

---

## Interactive Component

The mood check-in widget inside `#features` is the only JS on the page:

```js
const moodMap = { '😭 Awful': "...", '😟 Low': "...", ... };

function pickMood(el, m) {
  document.querySelectorAll('.mood-chip').forEach(c => c.classList.remove('active'));
  el.classList.add('active');
  document.getElementById('mr').textContent = moodMap[m] || '';
}
```

Clicking a chip adds `.active` (highlighted via CSS border/bg) and displays a contextual response string below.

---

## Responsive Behavior

Single breakpoint at `768px` at the bottom of the `<style>` block:

- `.steps-inner` collapses from 2-column grid to single column
- Floating phone cards (`.fc-l`, `.fc-r`, `.fc-b`) hidden on mobile
- `nav-links` hidden on mobile — hamburger menu not yet implemented

---

## To-Do

- [ ] App store link — replace `href="#"` on download buttons once available
- [ ] Mobile hamburger menu — nav links disappear below 768px with no fallback
- [ ] OG meta tags — `og:title`, `og:description`, `og:image` for link previews
- [ ] Favicon — not set
- [ ] Analytics — no tracking script; add before launch

---

## Deployment

No build step. Upload the single `.html` file to any static host:

```bash
# Netlify CLI
netlify deploy --prod --dir .

# Or drag and drop at netlify.com/drop
```

> For GitHub Pages, rename the file to `index.html`.

---

## Notes for Review

- CSS class names are intentionally short (`.fc-card`, `.pc`, `.sec`) due to single-file context — would be refactored to BEM or a component system if moved to a proper framework
- Phone mockup is built entirely with CSS/HTML — no image assets
- Blob backgrounds are `position: absolute` divs with `filter: blur()` — no SVG or canvas
- Logos are base64-inlined to keep the file self-contained and portable
