# CLAUDE.md

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

## Skills and Tools

- /webapp-testing — Playwright browser preview and screenshot capture at 480px
