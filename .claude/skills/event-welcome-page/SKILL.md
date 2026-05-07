---
name: event-welcome-page
description: Generate a single-file HTML welcome page for events, conferences, meetups, or community gatherings — playful, visually striking, ready to open in a browser. Trigger whenever the user asks for an event landing page, conference welcome page, meetup intro page, hackathon homepage, registration page, 活动欢迎页, 会议欢迎页, 活动主页, 签到页, 报名页, or any "welcome / landing / hero page for X event". Use this even when the user just describes an event and asks for "a page" without explicitly saying "welcome page" — if there's a date, venue, speakers, or schedule involved, this skill applies.
---

# Event Welcome Page

Build a single-file HTML welcome page for an event. The output is one `.html` file the user can open directly in a browser — no build step, no external dependencies (except optional Google Fonts via `<link>`).

## What this skill optimizes for

Event welcome pages compete for attention. Generic hero + 3 columns + footer looks like every other page on the internet — people skim past it. The job here is to make something that **stops the scroll**: a strong visual hook, a sense of personality matching the event, and concrete information (when, where, who) presented with clarity.

The default aesthetic is **playful and visually striking** — think bold gradients, oversized typography, geometric shapes, asymmetric layouts, subtle animations. Not corporate-flat. Not AI-generic-purple-gradient. If the event is genuinely formal (e.g., a medical conference), tone it down — but lean toward expressive by default unless the user signals otherwise.

## Required information

Before writing, make sure you have or can reasonably infer:

1. **Event name** — exact title to feature in the hero
2. **Date and time** — used for the countdown
3. **Venue / location** — physical address, city, or "online"
4. **Tagline or one-line pitch** — a short subtitle under the title

Optional but commonly useful: schedule/agenda, speakers/guests, sponsors, registration link.

If the user hasn't given enough to make the page feel real, ask **once** for the missing essentials in a single concise question — don't interrogate. If they say "just make something up" or it's clearly a demo, invent plausible details and note in the final message which fields you fabricated so they can swap them out.

## Required sections (in order)

Include these by default. Drop a section only if the user explicitly says it's not relevant or there's no data for it.

1. **Hero** — Event name as oversized type, tagline, date/venue line, primary CTA button. Strong background visual (gradient, shapes, pattern, or hero image area).
2. **Time + venue + countdown** — Live JS countdown to the event start. Show days / hours / minutes / seconds. Pair with the venue and date prominently displayed.
3. **Agenda / schedule** — Time-ordered list of sessions or activities. Use a vertical timeline or a clean session-card layout.
4. **Speakers / guests** — Card grid with name, role/affiliation, and a placeholder avatar (initials in a colored circle if no photo URL).
5. **Sponsors** — Logo wall or text-based tiers (Gold / Silver / Community). Use placeholder tiles if no logos provided.
6. **CTA / register** — A second registration call-to-action near the bottom, plus a footer with contact info.

If the user provides only some of these, build what they gave you and skip the rest cleanly — don't fill missing sections with obvious lorem ipsum filler.

## Technical constraints

- **Single file.** All CSS in a `<style>` tag in `<head>`. All JS (countdown) in a `<script>` tag before `</body>`. No external CSS frameworks, no build tools.
- **Self-contained.** Only allowed external resource is Google Fonts via `<link>`. No CDN'd JS libraries, no images from URLs (use CSS gradients, SVG inline, or emoji as visual elements).
- **Responsive.** Must look good on mobile (≤480px) and desktop. Use flexbox/grid, `clamp()` for fluid type, and at least one mobile media query.
- **Accessible basics.** Real semantic HTML (`<header>`, `<main>`, `<section>`, `<footer>`), `lang` attribute, alt text for any images, sufficient color contrast for body text.
- **Modern but supported.** Target evergreen browsers. CSS custom properties, grid, `:has()` are fine. Don't reach for cutting-edge features that need fallbacks.

## Where to write the file

Default to `welcome.html` in the user's current working directory. If a `welcome.html` already exists, pick a non-colliding name (`welcome-<event-slug>.html`) and mention it in the final message. If the user specifies a path, honor it.

## Visual design — how to actually make it look good

This is the hard part. Generic AI output for a "welcome page" is a centered hero with a purple gradient and three feature cards below. **Do not produce that.** See `references/design-patterns.md` for concrete moves that produce distinctive output — color palette construction, type scale, layout systems, animation patterns, and decorative element ideas. Read it before writing any CSS.

Pick **one** strong organizing idea per page (a dominant geometric motif, an unusual layout grid, a striking color treatment) and let the rest of the page support it, rather than throwing every effect at the wall.

## Workflow

1. Confirm or ask for the essential event details (name, date, venue, tagline). Keep this to one short question if anything is missing.
2. Read `references/design-patterns.md` for visual technique options. Pick a direction that fits the event's vibe (a hackathon and a wedding need different energy).
3. Write the full HTML file in one pass. Use real content from the user where given; use clearly-marked placeholders elsewhere.
4. Save to the working directory.
5. In the final message: tell the user the file path, list any details you fabricated, and suggest 1–2 quick tweaks they might want (e.g., "swap the hero gradient", "add real speaker photos by replacing the initials in the `.speaker-avatar` divs").

## Anti-patterns to avoid

- Centered-everything pages with three identical feature cards. Asymmetry and hierarchy are your friends.
- The default purple-to-blue gradient. Pick palettes intentionally — see references.
- Stock motivational copy ("Welcome to the future of X", "Innovate. Inspire. Iterate."). Use the event's actual tone.
- Heavy frameworks just to style a page. This is a single file.
- Excessive scroll-jacking, parallax, or animation that fights the user. Subtle motion only.
- Comments explaining what HTML tags do. The code should be clean enough not to need them.
