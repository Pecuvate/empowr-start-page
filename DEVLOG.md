# DEVLOG — Empowr Landing Page

Reverse-chronological log of sessions and decisions.

---

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

## 2026-08-04 — sitemap.xml added; robots.txt now declares it

- Added a static `src/public/sitemap.xml` (2 URLs) and restored the `Sitemap:` line in `robots.txt`. Verified live at `start.empowrcic.org/sitemap.xml` after deploy (`78165b0`, branch `master`).
- **Static file rather than `@astrojs/sitemap`** — this site is a deliberately single-page link hub plus the quiz, so the integration would add a dependency, an `astro.config.mjs` `site` key, and a build step to generate two URLs. A comment in the file records when to switch: if routes start being added regularly.
- **Trailing slashes are canonical.** Astro's directory build format 301s `/quiz` to `/quiz/`, so the unslashed form would have pointed crawlers at a redirect. Confirmed by request before writing, not assumed.
- Completes the other half of the 2026-07-30 link audit, which removed the dead `Sitemap:` line rather than build a generator.

## 2026-07-30 — `Layout.astro` PostHog snippet: `capture_pageview: true` → `'history_change'`.

## 2026-07-29 — `src/components/LinkButton.astro`: was never covered by the Main Site/EELA referrer-restoration sweep from a prior session. Hardcoded `rel="noopener noreferrer"`...

## 2026-07-28 — Switched PostHog to `cookieless_mode: 'always'` in `Layout.astro` as the T3 pilot site for the Empowr CIC-wide cookieless rollout; verified live via matching `distinct_id`/`$session_id` across a two-page visit

---

## 2026-06-23 - Migrated Astro project into src/ per MWP structure (netlify.toml base = "src"); added CONTEXT/DEVLOG/agents/skills docs
