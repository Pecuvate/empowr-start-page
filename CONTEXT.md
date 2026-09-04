# Empowr Landing Page — Context

Read this after `CLAUDE.md` to orient within the project.

---

## What This Is

Single-page Astro link-in-bio hub for Empowr CIC. Routes visitors to roller skating programmes, shop, donations, and volunteering. Deployed at `start.empowrcic.org`.

**Status:** Live on Netlify
**Domain:** `start.empowrcic.org`
**Branch:** master

---

## Architecture

```
src/                            Astro project root (package.json, astro.config.mjs here)
  src/                          Astro source (pages, components, layouts)
    pages/
      index.astro               Single-page hub
    layouts/
      Layout.astro              Base HTML layout
    components/                 Reusable Astro components
  public/                       Static assets (images, icons)
  dist/                         Build output (gitignored)

design/                         HTML/CSS design docs and mock-ups
publish/                        Image assets, URL wiring, deployment notes
docs/                           Process documentation
netlify.toml                    Netlify config — base = "src", publish = "dist"
```

---

## Key Files

| File | Purpose |
|---|---|
| `src/src/pages/index.astro` | The entire page — edit copy, links, and layout here |
| `src/src/layouts/Layout.astro` | Base HTML shell — meta, fonts, global styles |
| `publish/` | Image assets and URL wiring reference |
| `../workspace-docs/empowr-start-page/memory.md` | Running project state and link registry — in the private hub, not this repo |

---

## Related Projects

| Project | Relation |
|---|---|
| `../empowr-heroes-nextjs/` | Donation platform — linked from this page |
| `../Empowr Main Site/` | Main CIC website — linked from this page |
| `../Empowr EELA/` | Sessions platform — linked from this page |
