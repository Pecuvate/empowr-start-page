# DEVLOG — Empowr Landing Page

Reverse-chronological log of sessions and decisions.

---

## 2026-08-23

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

## 2026-07-30 — PostHog `capture_pageview` aligned to `'history_change'` (fleet-wide)

- `Layout.astro` PostHog snippet: `capture_pageview: true` → `'history_change'`.
- **No behavioural change today.** This is an Astro MPA with no `<ClientRouter />`, so navigation between `/` and `/quiz` is a hard load and `true` was already capturing correctly. Changed for fleet consistency and to remove a future trap: `'history_change'` is a strict superset (it still fires the initial pageview), so if this site ever adopts view transitions it won't silently start dropping data.
- The Next.js sites were genuinely broken by the same value — see the Empowr Heroes DEVLOG for the full finding. Canonical templates in `_config/guides/posthog-consent.md` updated, including the Astro one.
- Verified: `npm run build` clean (2 pages).

---

## 2026-07-29 — Fixed shared-rel referrer bug + cross-site UTM tagging

- `src/components/LinkButton.astro`: was never covered by the Main Site/EELA referrer-restoration sweep from a prior session. Hardcoded `rel="noopener noreferrer"` for every destination regardless of ownership — the same "one shared `rel` across Empowr-owned and third-party links" bug already found and fixed in a different component during that sweep. Added an `empowrOwned` prop so Empowr destinations get `noopener` only; Wix/WhatsApp/Trustpilot correctly keep `noopener noreferrer`.
- Same fix applied to the two raw `<a>` tags in `index.astro` (eela.empowrcic.org links) and the dynamic quiz-result CTA in `quiz.astro`.
- All Empowr-owned links (to empowrcic.org, hero.empowrcic.org, eela.empowrcic.org) now carry `?utm_source=empowr-landing&utm_medium=internal` — the practical alternative to full cross-domain session linking, ruled out this session as incompatible with `cookieless_mode: 'always'` (full reasoning in AnalyticsHub DEVLOG)
- Verified with `astro build` + inspected generated HTML for correct `rel`/UTM output. Commit `27e5cd7`, pushed to `master`, Netlify auto-deployed

---

## 2026-07-28 — Switched PostHog to `cookieless_mode: 'always'` in `Layout.astro` as the T3 pilot site for the Empowr CIC-wide cookieless rollout; verified live via matching `distinct_id`/`$session_id` across a two-page visit

---

## 2026-06-23 - Migrated Astro project into src/ per MWP structure (netlify.toml base = "src"); added CONTEXT/DEVLOG/agents/skills docs
