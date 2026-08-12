<div align="center">

  <a href="https://shobhit.net/"><img src="https://img.shields.io/badge/Website-shobhit.net-blue?style=for-the-badge&logo=google-chrome" alt="Website" /></a> <a href="https://x.com/Shobhit"><img src="https://img.shields.io/badge/Twitter-%40Shobhit-black?style=for-the-badge&logo=x" alt="Twitter" /></a> <a href="https://linkedin.com/in/geeklord/"><img src="https://img.shields.io/badge/LinkedIn-GeekLord-blue?style=for-the-badge&logo=linkedin" alt="LinkedIn" /></a> <a href="https://github.com/GeekLord/"><img src="https://img.shields.io/badge/GitHub-GeekLord-181717?style=for-the-badge&logo=github" alt="GitHub" /></a> <a href="https://g.dev/Shobhit"><img src="https://img.shields.io/badge/Google Dev-Shobhit-blue?style=for-the-badge&logo=google" alt="Google Dev" /></a>

  <img src="https://img.shields.io/badge/HTML-informational?style=for-the-badge&logo=html5" alt="badge" /> <img src="https://img.shields.io/github/stars/GeekLord/GeekLord.github.io?style=for-the-badge&logo=github" alt="badge" /> <img src="https://img.shields.io/github/forks/GeekLord/GeekLord.github.io?style=for-the-badge&logo=github" alt="badge" /> <img src="https://img.shields.io/github/last-commit/GeekLord/GeekLord.github.io?style=for-the-badge" alt="badge" />

</div>

# GeekLord.github.io

The personal landing page of Shobhit Kumar Prabhakar. Neon on black, terminal typography, a
falling-glyph canvas behind everything, and a holographic panel turning slowly in the corner.

Live at [geeklord.github.io](https://geeklord.github.io/).

## What's in here

```
index.html    the whole site: markup, inline CSS, inline JS
README.md     this file
```

One file. No build step, no dependencies, nothing fetched at runtime. The icons and the
decorative art are inline SVG. Push to the default branch and GitHub Pages serves it.

## Running it locally

Open `index.html` in a browser. If you want a real origin to test against:

```bash
python -m http.server 8000
# then visit http://localhost:8000
```

## Animation, and why it's written this way

The page animates constantly, so it stays away from the effects that make a browser redo work on
every frame. An earlier revision used several of them at once and locked up the main thread: in
headless Chromium at 1440x900 it managed 7.5fps with a worst frame of 693ms, which reads as a
freeze. The current version holds 75fps, a median frame near 13ms, and nothing over 50ms.

What was expensive, and what replaced it:

- A blend mode on the full-screen scanline overlay makes the browser re-composite the entire
  viewport every time the canvas paints. There is no `mix-blend-mode` left anywhere.
- `backdrop-filter` re-blurs whatever sits behind it whenever that content moves, and the canvas
  moves constantly. It's gone from the top bar and all six cube faces.
- Animating `box-shadow`, `filter`, or a 3D transform on a `preserve-3d` parent repaints that
  element's whole subtree. Every looping keyframe now touches `transform` and `opacity` only.
- The glow pools are radial gradients instead of blurred layers, because a blurred layer has to
  be re-rasterized each time it scales.
- The canvas skips `shadowBlur`. A blurred shadow per glyph, per frame, was the most expensive
  call in the loop. Its backing store also stays at CSS-pixel resolution rather than scaling with
  `devicePixelRatio`.
- The canvas loop runs at roughly 18fps and stops completely when the tab is hidden or the
  visitor prefers reduced motion. Resize handling is debounced, since mobile browsers fire
  `resize` on every address-bar shift.

## Accessibility

- Decorative layers carry `aria-hidden`: the canvas, the glow pools, the SVG art, the rotating
  cube, the dots on the terminal window.
- Landmarks are labelled, and the document has exactly one `<h1>`.
- Every link and button has a visible focus indicator, and the page is fully tab-navigable.
- `prefers-reduced-motion` neutralizes the CSS animations and halts the canvas loop.

## Contributing

It's a personal homepage, so it isn't looking for features, but bug reports and fixes are
welcome. Keep everything inside `index.html`, take colours from the `:root` custom properties,
and re-read the two sections above before opening a pull request.
