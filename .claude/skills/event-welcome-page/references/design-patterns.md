# Design Patterns for Distinctive Event Welcome Pages

Read this before writing CSS. The goal is output that doesn't look AI-generic. Pick **one** organizing idea per page and commit to it — don't mix every technique below into a single page.

## Color palettes (avoid the default purple gradient)

The boring default: `linear-gradient(135deg, #667eea, #764ba2)`. Reach for something else. Some directions that work for events:

- **Sunset / vivid analogous**: `#ff6b6b` → `#feca57` → `#ff9ff3`. Warm, energetic. Good for festivals, creative meetups.
- **Electric high contrast**: jet black `#0a0a0a` background with one vivid accent (`#39ff14` neon green, `#ff0080` hot pink, or `#00d4ff` cyan). Reads as "tech / hackathon / underground".
- **Risograph / printed zine**: two flat colors that almost-but-don't-quite clash, like `#e63946` + `#1d3557` on `#f1faee`. Feels handmade.
- **Pastel + one bold**: soft mint `#c4f4d3` background, deep navy `#1a1a2e` type, single hot accent `#ff5722` for CTA. Modern, friendly.
- **Monochrome + paper**: cream `#faf6f0` background, near-black `#1a1614` text, single accent for CTA. Pair with a serif display face for editorial feel.
- **Y2K revival**: chrome gradient (`#e0e0e0` → `#a0a0a0` → white), saturated primaries as accents, glossy shapes.

Define palettes as CSS custom properties at `:root`. Use them everywhere, don't hardcode hex values inline.

## Typography — go big or go home

The hero title should be **oversized**. Think `clamp(3rem, 12vw, 9rem)`, not 48px. Weight contrast matters more than size variety: pair an extreme weight (900 / Black) with a very light one (300) and skip the middle.

Good Google Fonts pairings for events:
- **Space Grotesk** (display) + **Inter** (body) — clean tech feel
- **Bebas Neue** (display, all-caps) + **DM Sans** (body) — poster energy
- **Fraunces** (display serif, with optical sizing) + **Inter** (body) — editorial
- **Archivo Black** (display) + **Archivo** (body) — bold and unified
- **Caveat** or **Permanent Marker** (handwritten accent, used sparingly) + clean sans for body — playful touch
- **Syne** (display, weird and modern) + **Inter** — gallery/conference vibe

Tracking matters: tighten oversized display text (`letter-spacing: -0.04em`), loosen all-caps labels (`letter-spacing: 0.15em`).

Use **fluid type** with `clamp()` everywhere: `font-size: clamp(1rem, 1vw + 0.8rem, 1.25rem)`. Skip media-query font size juggling.

## Layout — break the centered column

Default AI output centers everything in a 800px column. Resist this.

- **Asymmetric hero**: title spans 2/3 of the grid on the left, date/venue card sits in the right 1/3 rotated 2deg.
- **Off-grid date stamp**: a square/circular element with the date in oversized type, positioned absolutely overlapping the hero edge.
- **Vertical text rail**: a thin sidebar with the event name set vertically (`writing-mode: vertical-rl`) running down the page edge.
- **Bento grid**: agenda or features as varied-size grid cells, not three equal cards. Use `grid-template-areas` for control.
- **Marquee strip**: a continuously-scrolling row of text or logos between sections (CSS animation, no JS needed).
- **Sticker-stack speakers**: speaker cards slightly rotated at different angles (`transform: rotate(-3deg)`, `rotate(2deg)`...) overlapping in a grid.

## Decorative elements

Don't leave large flat areas blank. Fill them with:

- **CSS-drawn shapes**: large circles, blobs, or grids drawn with `border-radius`, `clip-path`, or radial gradients. Position with `position: absolute` and `z-index: -1`.
- **SVG patterns inline**: dot grids, diagonal stripes, noise textures. Inline `<svg>` as a background using `data:` URL or as a positioned element.
- **Emoji as visual**: a single oversized emoji (🎉, 🎤, ✨, 🚀) as a graphic element, not a bullet point. Set to ~10rem with low opacity.
- **Gradient blobs**: large soft `radial-gradient` ellipses with `filter: blur(80px)` behind content. Adds depth without imagery.
- **Grain / noise overlay**: a fixed full-screen `::before` with an SVG noise filter at low opacity. Adds texture.

## Countdown — make it the visual centerpiece, not an afterthought

The countdown is one of the few dynamic elements. Treat it as a feature. Some patterns:

- **Flip-card digits**: large boxes with each number, separated, each with a strong color block.
- **Inline narrative**: "**07** days **14** hours **23** minutes until doors open" — large numbers inline with descriptive text.
- **Concentric rings**: SVG circular progress rings for days/hours/minutes — visually striking but more code.

Default to flip-card digits unless you have reason to do otherwise — they're impactful and not too much code.

```js
const target = new Date('2026-06-15T18:00:00').getTime();
function tick() {
  const diff = target - Date.now();
  if (diff <= 0) { /* event started state */ return; }
  const d = Math.floor(diff / 86400000);
  const h = Math.floor(diff % 86400000 / 3600000);
  const m = Math.floor(diff % 3600000 / 60000);
  const s = Math.floor(diff % 60000 / 1000);
  // update DOM elements...
}
setInterval(tick, 1000); tick();
```

## Animation — subtle, not distracting

- **Entrance**: hero text and CTA fade-up on load with `@keyframes` and slight stagger (`animation-delay`). 400-600ms total, no longer.
- **Hover states**: every interactive element needs one. CTA buttons can lift (`transform: translateY(-2px)`) and shift shadow.
- **Floating decorations**: shapes can `animation: float 6s ease-in-out infinite alternate` with `transform: translateY(-20px)`.
- **Marquee**: `@keyframes scroll { to { transform: translateX(-50%); } }` for a logo strip — duplicate content twice for seamless loop.
- **`prefers-reduced-motion`**: wrap non-essential animations in `@media (prefers-reduced-motion: no-preference) { ... }`.

## Mobile

- Hero title still wants to be big on mobile — `clamp()` handles this if you set a sensible min.
- Single column below ~768px is fine, but keep visual personality. Don't strip all decorative elements on mobile.
- Tap targets ≥ 44px. Buttons and links generously padded.
- Test the countdown — it should not break to two lines awkwardly. Use `flex-wrap: wrap` and small gaps.

## Putting it together — recipe templates

If stuck, start with one of these directional combinations:

**"Tech hackathon" recipe**: Black background, neon green accent, Space Grotesk Black for hero, asymmetric grid, marquee strip of "BUILD / SHIP / WIN" between sections, flip-card countdown, sticker-stack speaker grid.

**"Indie meetup" recipe**: Cream background, deep blue text, hot orange CTA, Fraunces display serif, asymmetric layout with rotated date stamp, hand-drawn looking SVG arrows pointing to schedule, soft pastel blobs in corners.

**"Music festival" recipe**: Sunset gradient (coral → yellow → pink), Bebas Neue all-caps, oversized emoji decorations (🎶, ✨), bento grid for lineup, large CTA in a contrasting color block.

**"Corporate-ish but not boring conference" recipe**: Cream + navy + single bright accent, Inter throughout with one weight pairing, restrained asymmetry (one rotated date card), grid agenda with time on the left, simple hover states.

Pick one, then deviate where the event's specifics suggest something different.
