---
inclusion: always
---

# GeekLord.github.io

Personal landing page for Shobhit Kumar Prabhakar (GeekLord), served by GitHub Pages at the
repo root. Themed as a "hacker command center": neon-on-black, terminal typography, animated
holographic dashboard.

## Architecture

- **Single-file site.** `index.html` contains all markup, an inline `<style>` block, and an
  inline `<script>` block. Keep it that way.
- **No build step, no dependencies.** No npm, no bundler, no framework, no CDN links, no web
  fonts. The page must open correctly from the filesystem and deploy by pushing to the default
  branch.
- **Zero runtime network calls.** Icons and decorative art are inline SVG. Do not add external
  images, analytics, or trackers.
- Only add a new file when a page genuinely cannot live in `index.html` (for example `CNAME`,
  `robots.txt`, `404.html`). Prefer extending the existing document.

## Content and voice

- Copy uses cyber/terminal metaphors (`root@geeklord`, `sudo deploy`, "Enter mainframe",
  "Operator profile"). Match this register; keep it playful, never edgy or menacing.
- Outbound links point to the real profiles: `shobhit.net`, `github.com/GeekLord`,
  `linkedin.com/in/geeklord`, `x.com/Shobhit`, `g.dev/Shobhit`. Keep these in sync between the
  topbar nav, the hero action buttons, and the operator card link list.
- `README.md` is badge-driven and mirrors the same profile links. Update it alongside link changes.

## CSS conventions

- Colors, surfaces, and borders come from the `:root` custom properties (`--green`, `--cyan`,
  `--purple`, `--red`, `--gold`, `--text`, `--muted`, `--panel`, `--border`). Add a new variable
  rather than hard-coding a hex value; raw `rgba()` is acceptable only for one-off glow and
  shadow tints.
- Class names follow BEM-ish naming: block (`.hero`), element (`.hero__grid`), modifier
  (`.button--primary`, `.glow--a`).
- Declarations inside a rule are ordered roughly layout → box → visual → typography →
  effects → animation, matching the existing blocks.
- Fluid sizing uses `clamp()` and `min()`; avoid fixed pixel widths for layout containers.
- Monospace stack is `"SFMono-Regular", Consolas, monospace`; body stack starts with `Inter`
  and falls back to system fonts.
- Breakpoints are `max-width: 920px` and `max-width: 560px`. Add responsive overrides to those
  existing blocks instead of introducing new breakpoints.
- Decorative layers live on `body::before` / `body::after`, `.matrix`, `.glow`, and `.hero::before`
  / `.hero::after` with negative or low `z-index`. Respect that stacking order when adding visuals.

## Accessibility requirements

These are non-negotiable; verify them after any markup or style change.

- Every purely decorative element carries `aria-hidden="true"` (canvas, glows, SVGs, cube,
  terminal window dots).
- Landmarks and labels stay intact: `aria-label` on `header`/`nav`, `aria-labelledby` on the
  hero section, one `<h1>`.
- Interactive elements keep visible `:focus-visible` styling paired with their `:hover` styling.
- The `@media (prefers-reduced-motion: reduce)` block must keep neutralizing animations and
  transitions, and the matrix canvas must keep honoring `motionQuery` at runtime.
- Do not remove the `<meta name="viewport">` or `<meta name="description">` tags.

## JavaScript conventions

- Vanilla ES2015+ in the inline script. No modules, no transpilation, no libraries.
- Style: `const`/`let`, named function declarations, template literals, single quotes,
  two-space indent, semicolons.
- Canvas animation rules to preserve: device pixel ratio capped at 1.5, ~24 fps throttle via
  `targetFrameMs`, and the animation paused when `document.hidden` or reduced motion is on.
  Always cancel via `window.cancelAnimationFrame` and reset `animationFrame` to `0`.
- Register scroll and resize listeners as `{ passive: true }`.
- Keep the script defensive about performance: this is a static page that should stay instant
  on mobile.

## Verification

There is no test suite or linter. After editing, open `index.html` in a browser and confirm
the hero renders, the matrix canvas animates, links resolve, layout holds at ~360px / ~900px /
desktop widths, keyboard focus is visible through all links and buttons, and enabling
reduced motion stills the page.
