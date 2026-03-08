# MindTraker
# MindTrack — Landing Page

Single-file marketing landing page for the MindTrack app. No framework, no build tool, no dependencies. Just HTML, CSS, and vanilla JS.

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
```

Intentionally kept as a single file for portability — can be dropped on any static host with zero configuration.

---

## Sections

| Section | Description |
|---|---|
| `nav` | Fixed navbar with blur backdrop, links, CTA button |
| `.hero` | Full-height hero with animated phone mockup and floating stat cards |
| `.stats-bar` | 4 key numbers — market context |
| `#features` | 6 feature cards grid + live mood check-in widget |
| `#how` (`.steps-section`) | How it works — 4-step flow + progress card visual |
| `#pricing` (`.pricing-wrap`) | 3 pricing tiers (Free / Pro / Store Items) |
| `.sec` (revenue) | 4 revenue stream cards |
| `#download` (`.cta-sec`) | Final CTA section |
| `footer` | Brand + legal line |

---

## Design Tokens

All colors and surfaces are defined as CSS custom properties at the top of the `<style>` block:

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

All animations are pure CSS, no JS involved:

| Name | Used on |
|---|---|
| `fadeUp` | Hero heading, subtext, buttons, phone mockup |
| `floatL / floatR` | Floating stat cards around the phone |
| `pulse` | Green live dot in the hero badge |

Entrance animations use `animation-delay` to stagger elements on load.

---

## Interactive Component

The mood check-in widget (inside `#features`) is the only JS on the page:

```js
const moodMap = { '😭 Awful': "...", '😟 Low': "...", ... };

function pickMood(el, m) {
  document.querySelectorAll('.mood-chip').forEach(c => c.classList.remove('active'));
  el.classList.add('active');
  document.getElementById('mr').textContent = moodMap[m] || '';
}
```

Clicking a mood chip adds `.active` (highlights it via border/bg CSS) and displays a response string below.

---

## Responsive Behavior

Breakpoint at `768px` (inside a single `@media` block at the bottom of the styles):

- `.steps-inner` collapses from 2-column grid to single column
- Floating phone cards (`.fc-l`, `.fc-r`, `.fc-b`) hidden on mobile
- `nav-links` hidden on mobile — hamburger menu not yet implemented

---

## What's Missing / To-Do

- [ ] App store link — replace `href="#"` on all `.btn-primary` download buttons with the real URL once available
- [ ] Mobile hamburger menu — nav links are hidden below 768px with no fallback yet
- [ ] OG meta tags — add `og:title`, `og:description`, `og:image` for link previews
- [ ] Favicon — none set currently
- [ ] Analytics — no tracking script included; add before launch

---

## Deployment

No build step needed. Upload the single `.html` file to any static host:

```bash
# Netlify CLI
netlify deploy --prod --dir .

# Or drag the file to netlify.com/drop
```

> For GitHub Pages, rename the file to `index.html`.

---

## Notes for Review

- CSS class names are intentionally short (`.fc-card`, `.pc`, `.sec`) due to the single-file context — would be refactored into BEM or a component system if this moves to a proper framework
- The phone mockup is pure CSS/HTML — no image assets used anywhere on the page
- Blob backgrounds are `position: absolute` divs with `filter: blur()` — no SVG or canvas
