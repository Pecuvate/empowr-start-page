# CLAUDE.md

> **This repository is PUBLIC** (`PecuvateOrg/empowr-start-page`).
>
> **Devlog and memory location:** `../workspace-docs/empowr-start-page/`
>
> `DEVLOG.md` and `memory.md` are **not** kept in this repo — they hold operational
> detail that must not be world-readable. Write session entries to the path above,
> in the private Empowr CIC hub. Both filenames are gitignored here, so a copy created
> in this directory is silently never committed.
>
> Never put live identifiers, unremediated security findings, or commercial state
> in any file tracked here. See `../CONTEXT.md` and
> `_config/guides/public-repo-collaboration.md`.

## Identity
Empowr CIC landing page — a single-file static HTML link-in-bio hub (480px mobile-first) routing visitors to roller skating programmes, shop, donations, and volunteering.

## Self-Reference
This file is the map. Workspace detail lives in each CONTEXT.md.

## Routing

| Task | Go to | Read | Skills |
|---|---|---|---|
| HTML/CSS edits, layout, copy, brand tokens | design/ | design/CONTEXT.md | webapp-testing |
| Image assets, URL wiring, deployment | publish/ | publish/CONTEXT.md | webapp-testing |

## Cross-Workspace Flows

- Content update → Deploy: design/ (edit HTML/CSS/copy) → publish/ (swap images, wire URLs) → deploy to Netlify

## Naming Conventions

- CSS classes: kebab-case (`.link-btn`, `.blue-card`)
- File names: kebab-case
- Section comments: `<!-- SECTION N: Name -->`

## File Placement

- HTML source → project root
- Image assets → assets/ (when created)

## Token Management

- Do not read `landing.page.guide.html` in full unless editing markup — read only the relevant section
- Do not load publish/CONTEXT.md unless the task involves images, URLs, or deployment
- Do not load design/CONTEXT.md unless the task involves HTML, CSS, or copy

## Deployment

- Platform: Netlify
- Domain: start.empowrcic.org
- Branch: master

## Skills and Tools Available

| Tool / Skill | Trigger | Purpose |
|---|---|---|
| `/netlify-deploy` | deploying to Netlify | Deploy to Netlify and configure `start.empowrcic.org` |
| `/pre-build-check` | before any deploy | Validate Astro build structure and frontend quality |
| `/pre-deploy-security` | before any deploy | Security hygiene scan — FAILs block the deploy |
| `/webapp-testing` | after any change | Playwright browser preview and screenshot capture at 480px |
| `/simplify` | after a feature is built | Review changed code for reuse, quality, and efficiency |
