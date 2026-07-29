# DEVLOG — Empowr Landing Page

Reverse-chronological log of sessions and decisions.

---

## 2026-07-29 — Fixed shared-rel referrer bug + cross-site UTM tagging

- `src/components/LinkButton.astro`: was never covered by the Main Site/EELA referrer-restoration sweep from a prior session. Hardcoded `rel="noopener noreferrer"` for every destination regardless of ownership — the same "one shared `rel` across Empowr-owned and third-party links" bug already found and fixed in a different component during that sweep. Added an `empowrOwned` prop so Empowr destinations get `noopener` only; Wix/WhatsApp/Trustpilot correctly keep `noopener noreferrer`.
- Same fix applied to the two raw `<a>` tags in `index.astro` (eela.empowrcic.org links) and the dynamic quiz-result CTA in `quiz.astro`.
- All Empowr-owned links (to empowrcic.org, hero.empowrcic.org, eela.empowrcic.org) now carry `?utm_source=empowr-landing&utm_medium=internal` — the practical alternative to full cross-domain session linking, ruled out this session as incompatible with `cookieless_mode: 'always'` (full reasoning in AnalyticsHub DEVLOG)
- Verified with `astro build` + inspected generated HTML for correct `rel`/UTM output. Commit `27e5cd7`, pushed to `master`, Netlify auto-deployed

---

## 2026-07-28

- Switched PostHog from `persistence: 'memory'` to `cookieless_mode: 'always'` in `src/layouts/Layout.astro` (`61a162d`) — this was the T3 pilot site for the wider Empowr CIC cookieless rollout (see AnalyticsHub DEVLOG)
- Verified live: a real-browser (non-headless-UA) two-page visit produced the same `distinct_id`/`$session_id` across both pageviews, confirming PostHog's cookieless server hash mode correctly groups a visit into one session instead of memory mode's one-session-per-pageview behaviour
- Requires the PostHog project-level "Cookieless server hash mode" toggle (Project Settings → Web analytics) to be enabled — done manually, no API/MCP path exists for it

---

## 2026-06-23

- Migrated Astro project into `src/` per MWP structure — netlify.toml updated with `base = "src"`
- Added CONTEXT.md, DEVLOG.md, agents.md, skills.md for MWP compliance
- Added `## Identity` and `## Self-Reference` headings to CLAUDE.md
