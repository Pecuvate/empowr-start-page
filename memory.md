# Memory — Empowr Landing Page

## Current Status

- Phase: Live — deployed to start.empowrcic.org via Netlify (GitHub auto-deploy on push to master)
- Complete: Astro 6 + Tailwind v4, all 5 sections built, all URLs wired, real images in place, real logo live, performance optimised
- Outstanding: Nothing — page is clean and production-ready

## Key Decisions

- Single-file approach: all CSS stays inline — no build tools, no external stylesheets by design
- `landing.page.guide.html` is the design guide/mockup — the production file name may differ at deploy time
- Five sections established: Hero, Tagline/Links/Kids, Adults/Trusted By, Trustpilot/Donate, Get Involved
- Framework: Astro 6 + Tailwind v4 via PostCSS — do NOT use `@tailwindcss/vite` plugin, incompatible with Astro 6's rolldown resolver. Use `postcss.config.mjs` approach.
- Vite override: do NOT add `"overrides": { "vite": "^7" }` to package.json — breaks Astro's internal PostCSS chunk resolution. The Vite 8 warning is cosmetic; ignore it.
- webapp-testing (Playwright) unavailable — Python is not installed on this machine. Use `npm run dev` + browser for visual QA at 480px.
- Logo source: `F:\Projects\Empowr CIC\_brand\logo.png` — copied to `public/logo.png`. Reference as `/logo.png`. Do not use the emoji placeholder.
- Stats grid: `gap-2` + `px-1` on cards + no tracking on labels. `px-2` = 16px total (8px each side) — easy to underestimate. `overflow-hidden` added to cards as safety net.
- Tailwind `px-N` is N×4px *per side* — e.g. `px-2` = 16px total horizontal, not 8px.

## Performance Baseline (post-optimisation)

- Google Fonts preconnect hints in Layout.astro
- `loading="lazy"` on all below-fold images
- `decoding="async"` on all images
- `<meta name="description">` present
- Logo: `<img>` with `decoding="async"`, no lazy (above fold)

## Preferences

- (None recorded yet)

## Pre-Close Checklist

- [ ] Update Current Status to reflect what changed this session
- [ ] Record any new decisions in Key Decisions
- [ ] Note any outstanding work that was not completed
