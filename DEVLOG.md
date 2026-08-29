# DEVLOG — Empowr Landing Page

Reverse-chronological log of sessions and decisions.

---

## 2026-08-29 — Quiz result links repointed from Wix to eela.empowrcic.org

- `src/src/pages/quiz.astro`: all 7 quiz outcomes (Kidz, All Ages, Roller Disco, Sk8 Skool 15+, Synkron8, Skate Jam, Roller Skate Events) now resolve to `eela.empowrcic.org` pages instead of the old `empowrcic.wixsite.com` links. Five map to a dedicated new EELA detail page (built the same day on that project — see `Empowr CIC/Empowr EELA/DEVLOG.md` 2026-08-29 entries); Roller Disco and Roller Skate Events have no dedicated EELA page yet, so those two land on the nearest live discovery page (`/kids-space`, `/adults`) rather than a dead Wix link.
- Pushed to `master` (`2a76def`) — Netlify auto-deploy triggered, live at `start.empowrcic.org/quiz`.

## 2026-08-26

- Left on `master` while the rest of the estate standardised on `main` - renaming this repo needs Netlify's production branch updated in the same pass, or pushes land on a branch Netlify is not watching and deploys stop with no error surface
- The pnpm migration from 2026-08-24 is unaffected and still verified live

## 2026-08-24

- Migrated to pnpm 11.22.0 (`pnpm import` from package-lock.json), pinned `packageManager`, switched netlify.toml to `pnpm run build`
- `NODE_VERSION` was already `"22"` — first site in the campaign that already met pnpm 11's `engines.node >= 22.13`, so no bump was needed
- Approved the blocked native postinstalls (`esbuild`, `sharp`) — pnpm blocks these by default where npm runs them silently
- Verified via `netlify build` (exit 0): built `dist/index.html` 15,841 bytes, byte-identical to the live site both before and after deploying
- Deployed and verified: deploy `state: ready` in 20s, `/` 200 and `/quiz/` 200
- Gitignored `.netlify/netlify.toml`, a resolved-config snapshot `netlify build` generates that is not source

## 2026-08-14

- Created `README.md` at the project root, closing an M10 gap flagged by the scheduled mwp-health compliance audit.
- Converted a near-miss "Skills and Tools Available" heading in `CLAUDE.md` to the compliant M8 table format.

---

## 2026-08-04 — Added sitemap.xml (2 URLs, static file not @astrojs/sitemap) and restored robots.txt's Sitemap: line; completes the 2026-07-30 link audit

## 2026-07-30 — `Layout.astro` PostHog snippet: `capture_pageview: true` → `'history_change'`.

## 2026-07-29 — `src/components/LinkButton.astro`: was never covered by the Main Site/EELA referrer-restoration sweep from a prior session. Hardcoded `rel="noopener noreferrer"`...

## 2026-07-28 — Switched PostHog to `cookieless_mode: 'always'` in `Layout.astro` as the T3 pilot site for the Empowr CIC-wide cookieless rollout; verified live via matching `distinct_id`/`$session_id` across a two-page visit

---

## 2026-06-23 - Migrated Astro project into src/ per MWP structure (netlify.toml base = "src"); added CONTEXT/DEVLOG/agents/skills docs
