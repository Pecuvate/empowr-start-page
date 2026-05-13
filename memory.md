# Memory — Empowr Landing Page

## Current Status

- Phase: Build complete — dev server running, production build verified
- Complete: Astro 6 + Tailwind v4 project scaffolded, all 5 sections built, design guide converted to components, build passes, dev server confirmed at localhost:4321
- Outstanding: Real images needed (all placeholders are emoji/gradient divs), all `href="#"` links need live URLs wired, git init + Netlify deploy pending

## Key Decisions

- Single-file approach: all CSS stays inline — no build tools, no external stylesheets by design
- `landing.page.guide.html` is the design guide/mockup — the production file name may differ at deploy time
- Five sections established: Hero, Tagline/Links/Kids, Adults/Trusted By, Trustpilot/Donate, Get Involved
- Framework: Astro 6 + Tailwind v4 via PostCSS — do NOT use `@tailwindcss/vite` plugin, incompatible with Astro 6's rolldown resolver. Use `postcss.config.mjs` approach.
- Vite override: do NOT add `"overrides": { "vite": "^7" }` to package.json — breaks Astro's internal PostCSS chunk resolution. The Vite 8 warning is cosmetic; ignore it.
- webapp-testing (Playwright) unavailable — Python is not installed on this machine. Use `npm run dev` + browser for visual QA at 480px.

## Preferences

- (None recorded yet)

## Pre-Close Checklist

- [ ] Update Current Status to reflect what changed this session
- [ ] Record any new decisions in Key Decisions
- [ ] Note any outstanding work that was not completed
