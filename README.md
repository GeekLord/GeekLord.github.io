<div align="center">

  <a href="https://shobhit.net/"><img src="https://img.shields.io/badge/Website-shobhit.net-blue?style=for-the-badge&logo=google-chrome" alt="Website" /></a> <a href="https://x.com/Shobhit"><img src="https://img.shields.io/badge/Twitter-%40Shobhit-black?style=for-the-badge&logo=x" alt="Twitter" /></a> <a href="https://linkedin.com/in/geeklord/"><img src="https://img.shields.io/badge/LinkedIn-GeekLord-blue?style=for-the-badge&logo=linkedin" alt="LinkedIn" /></a> <a href="https://github.com/GeekLord/"><img src="https://img.shields.io/badge/GitHub-GeekLord-181717?style=for-the-badge&logo=github" alt="GitHub" /></a> <a href="https://g.dev/Shobhit"><img src="https://img.shields.io/badge/Google Dev-Shobhit-blue?style=for-the-badge&logo=google" alt="Google Dev" /></a>

  <img src="https://img.shields.io/badge/HTML-informational?style=for-the-badge&logo=html5" alt="badge" /> <img src="https://img.shields.io/github/stars/GeekLord/GeekLord.github.io?style=for-the-badge&logo=github" alt="badge" /> <img src="https://img.shields.io/github/forks/GeekLord/GeekLord.github.io?style=for-the-badge&logo=github" alt="badge" /> <img src="https://img.shields.io/github/last-commit/GeekLord/GeekLord.github.io?style=for-the-badge" alt="badge" />

</div>

# GeekLord.github.io

Personal GitHub Pages landing page for GeekLord / Shobhit Kumar Prabhakar.

## Performance notes

- The `index.html` page uses a canvas-based matrix rain background plus CSS-powered
  holographic interface effects.
- The matrix animation is intentionally capped to roughly 24 FPS, limits high-DPI
  canvas scaling, pauses while the tab is hidden, and honors
  `prefers-reduced-motion` so the page stays responsive on lower-power devices.
- If you add new visual effects, keep animations bounded and avoid unthrottled
  render loops that run when the page is not visible.
