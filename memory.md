# Memory — Empowr Landing Page

## Current Status

- Phase: Live — deployed to start.empowrcic.org via Netlify (GitHub auto-deploy on push to `master`)
- **Branch is deliberately `master`** while the rest of the estate moved to `main` (2026-08-26). Netlify pins a production branch per site, so renaming needs Netlify's setting updated in the SAME pass or pushes land on a branch Netlify isn't watching and deploys stop silently. Registry row confirms `master`. See [[feedback_git_branch_silent_rename]].
- **Package manager is pnpm 11.22.0 as of 2026-08-24 — use `pnpm`, not `npm`.** `netlify.toml` runs `pnpm run build` and pins `NODE_VERSION = "22"` (required: pnpm 11 declares `engines.node >= 22.13`). Astro needs no `nodeLinker: hoisted` workaround. Verified via `netlify build`: output byte-identical to live (15,841 bytes), deployed and re-verified.
- Complete: Astro 6 + Tailwind v4, all 5 sections built, all URLs wired, real images in place, real logo live, performance optimised
- Outstanding: schema.org `sameAs` YouTube handle `@empowr.cic` returned 404 in the 2026-07-30 link audit — inconclusive (may be a bot-block artefact, not confirmed dead); needs a manual browser check, not yet resolved. Trustpilot review URL uses `uk.trustpilot.com` here vs `www.trustpilot.com` on Main Site/EELA — inconsistent but likely harmless (Trustpilot regional subdomains alias to the same profile), not yet standardized.
- **2026-08-29:** Quiz's 7 result links repointed from Wix (`empowrcic.wixsite.com`) to `eela.empowrcic.org` pages — supersedes the 2026-07-30 fix below, which pointed them at Wix. 5 map to a dedicated EELA detail page (Kidz, All Ages, Beginners Foundation, Synkron8, Skate Jam); Roller Disco and Roller Skate Events have no dedicated EELA page yet, so those two land on the nearest live discovery page (`/kids-space`, `/adults`). Pushed to `master` (`2a76def`), Netlify auto-deployed. See `Empowr CIC/Empowr EELA`'s own memory.md for why those two are discovery-page fallbacks, not dedicated pages.
- **2026-08-04:** Added a static `src/public/sitemap.xml` (2 URLs) + restored the `Sitemap:` line in `robots.txt` (commit `78165b0`, branch `master`). Deliberately **not** `@astrojs/sitemap` — two routes don't justify the dependency, `site` config key and build step; a comment in the file records when to switch. **Trailing slashes are canonical here** — Astro's directory build format 301s `/quiz` to `/quiz/`, so the unslashed form would point crawlers at a redirect. This completes the half of the 2026-07-30 link audit that removed the dead `Sitemap:` line rather than building a sitemap.
- **2026-07-30:** `capture_pageview` aligned to `'history_change'` (commit `f73fae8`). **No behavioural change here** — this is an Astro MPA with no `<ClientRouter />`, so navigation between `/` and `/quiz` is a hard load and `true` was already capturing correctly. Changed for fleet consistency and to remove a future trap: `'history_change'` is a strict superset, so if this site ever adopts view transitions it won't silently start dropping data. The Next.js sites *were* genuinely broken by the same value — see the Empowr Heroes DEVLOG.
- **2026-07-28:** This site was the pilot for the Empowr CIC-wide PostHog cookieless-mode migration — `Layout.astro`'s inline PostHog init now uses `cookieless_mode: 'always'` instead of `persistence: 'memory'`, verified live (same session across a multi-page visit). See AnalyticsHub DEVLOG/memory for the full T3 rollout this fed into.
- **2026-07-29:** `LinkButton.astro` had a shared-`rel` bug — hardcoded `rel="noopener noreferrer"` for every destination, Empowr-owned and third-party alike. Added an `empowrOwned` prop; Empowr-owned links now get `noopener` + `?utm_source=empowr-landing&utm_medium=internal`, third-party (Wix/WhatsApp/Trustpilot) unchanged. Same fix in `index.astro`'s raw anchors and `quiz.astro`'s dynamic CTA. Commit `27e5cd7`.
- **2026-07-30:** User reported the quiz link was broken — all 7 quiz-result URLs in `quiz.astro` pointed to `www.empowrcic.org/{kidzspace,sk8-skool,roller-skate-events}`, routes that never existed on the Main Site (Next.js). Fixed to the real live Wix booking pages, matching EELA's `links.ts`. Also fixed a UTM-append bug (bare `?` instead of `&` when the URL already had a query string — broke the roller-disco result specifically). Commit `b0def46`.
- **2026-07-30 (full site link audit, same day):** `llms.txt` had `heroes.empowrcic.org` (typo'd subdomain, doesn't resolve — should be `hero.empowrcic.org`); `robots.txt` advertised a `sitemap.xml` that's never been generated (removed the dead line rather than building a sitemap). The "BECOME A HERO TODAY" CTA in `index.astro` was pointing at the Heroes homepage — repointed to `hero.empowrcic.org/become` (the tier-selection/donation page) per user request, since Heroes' problem is traffic/funnel-friction not content. Commit `f51186b`. Full audit detail: [[project_empowr_link_audit_2026_07_30]] in Claude memory.

## Key Decisions

- Single-file approach: all CSS stays inline — no build tools, no external stylesheets by design
- `landing.page.guide.html` is the design guide/mockup — the production file name may differ at deploy time
- Five sections established: Hero, Tagline/Links/Kids, Adults/Trusted By, Trustpilot/Donate, Get Involved
- Framework: Astro 6 + Tailwind v4 via PostCSS — do NOT use `@tailwindcss/vite` plugin, incompatible with Astro 6's rolldown resolver. Use `postcss.config.mjs` approach.
- Vite override: do NOT add `"overrides": { "vite": "^7" }` to package.json — breaks Astro's internal PostCSS chunk resolution. The Vite 8 warning is cosmetic; ignore it.
- ~~webapp-testing (Playwright) unavailable — Python is not installed~~ — **STALE, corrected 2026-08-26:** Python IS installed and working on this machine. Re-test whether Playwright/webapp-testing runs here before assuming it doesn't. For quick visual QA, `pnpm run dev` + browser at 480px still works.
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
