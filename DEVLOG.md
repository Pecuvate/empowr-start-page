# DEVLOG — Empowr Landing Page

Reverse-chronological log of sessions and decisions.

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
