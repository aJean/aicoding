---
name: welcome-screen
description: Generate a youthful, trendy welcome screen as a single HTML+CSS file. Trigger this skill whenever the user asks for: a welcome page, intro screen, splash screen, landing page, personal homepage, portfolio intro, event promo page, or any UI that should feel fresh, stylish, and vibrant. Also trigger when user says things like "帮我做个欢迎界面", "做个炫的首页", "青春时尚风格页面", "Y2K 风格", "霓虹风格", "时髦的落地页" or any variation. Don't wait for the user to say exactly "welcome screen" — if they want a visually appealing intro page, use this skill.
---

# Welcome Screen Generator

You generate beautiful, youthful, trendy single-file HTML welcome screens. Your output is always one self-contained `.html` file — no external dependencies, everything inlined.

## Core aesthetic: Y2K Neon Gradient

The default style has these characteristics:
- **Background**: deep purple → hot pink gradient (or dark background + neon gradient overlay)
- **Text**: neon/fluorescent yellow (`#F5FF00` or `#FFEF00`), bright white, or vivid pink — never dull or grey
- **Decorative elements**: stars (✦ ✧ ★ ☆), sparkle glows (`text-shadow`/`box-shadow`), wavy lines, floating orbs
- **Typography**: bold rounded font (use Google Fonts `Nunito`, `Poppins`, or `Fredoka One`) + italic accents for contrast
- **Vibe**: playful, energetic, glowing — like a festival poster or early-2000s magazine

Adapt this if the user gives different keywords: "minimal" → clean pastel, "dark" → cyberpunk neon, "soft" → muted peach/lavender. Always read the vibe cue before deciding.

## What to include in the page

Ask yourself: what does this page need to communicate? At minimum include:
- A bold, attention-grabbing **headline**
- A short **subtext** or tagline
- An optional **call-to-action button**
- Visual decorations that match the aesthetic

If the user gave a name, topic, or theme — weave it in. If not, use a generic but fun placeholder (e.g., "Welcome to My World ✦").

## How to build the HTML file

Use pure HTML + CSS (no JS frameworks, no external CSS files). Inline all styles in a `<style>` tag. Google Fonts are OK via `@import` — they're reliable and fast.

### Must-have CSS techniques
- `background: linear-gradient(...)` or `radial-gradient(...)` for layered depth
- `text-shadow` with neon glow effect: e.g., `0 0 8px #FF6FD8, 0 0 24px #FF6FD8`
- `box-shadow` on buttons/cards for glow
- `@keyframes` for at least one subtle animation (float, pulse, shimmer, spin)
- `backdrop-filter: blur(...)` for frosted-glass card effects if there's a content card

### Layout
- Center everything with `flexbox` (`display: flex; align-items: center; justify-content: center; min-height: 100vh`)
- Use `overflow: hidden` on `body` to keep decorations from creating scrollbars

### Decorative elements
Scatter a few absolutely-positioned SVG shapes or Unicode glyphs (✦ ✧ ⬡ ●) across the page. Animate them gently — floating upward, slow rotation, pulsing opacity. Don't overdo it: 3–5 decorations is enough.

### Example glow text style
```css
.headline {
  font-family: 'Fredoka One', cursive;
  font-size: clamp(2.5rem, 8vw, 6rem);
  color: #FFEF00;
  text-shadow: 0 0 10px #FFEF00, 0 0 30px #FF6FD8, 0 0 60px #A855F7;
  letter-spacing: 0.02em;
}
```

### Example float animation
```css
@keyframes floatUp {
  0%, 100% { transform: translateY(0px) rotate(0deg); }
  50% { transform: translateY(-18px) rotate(8deg); }
}
```

## Output

Save the file as `welcome.html` (or a name the user specified) in the current directory. After saving, tell the user:
- Where the file is
- How to open it (e.g., "double-click to open in browser")
- A one-line description of what you made

Don't explain every CSS property. Just ship it and let the visual speak.

## Quality bar

Before finalizing, ask yourself:
- Does it look like something a Gen-Z designer would post on Dribbble? If not, push the colors and animations further.
- Is the text legible against the background? Glow is great, but contrast matters.
- Does it work on mobile? Use `clamp()` for font sizes and `vw`/`vh` units.
- Is the file truly self-contained? No broken image links, no missing fonts (use system fallback or Google Fonts).
