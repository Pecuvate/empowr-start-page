# Empowr Landing Page

Single-page **link-in-bio hub** for Empowr CIC — routes visitors to roller skating programmes, the shop, donations, and volunteering. Mobile-first, designed at 480px.

Built with Astro + Tailwind CSS v4. Deployed on Netlify.

---

## Local Development

The Astro project root is nested at `src/` (so `src/package.json` and `src/astro.config.mjs` sit one level in, with Astro's own `pages/`/`components/`/`layouts/` under `src/src/`).

```bash
cd src
npm install
npm run dev
```

`npm run dev` runs `astro dev --host`, exposing the dev server on the LAN.

Build for production:

```bash
npm run build      # outputs to src/dist/
npm run preview    # preview the production build locally
```

---

## Environment Variables

None. This is a static Astro build with no server-side integrations — all links are hardcoded/wired directly in `src/src/pages/index.astro`.

---

## Deployment

| Field | Value |
|---|---|
| Platform | Netlify |
| Netlify site name | `empowr-start-page` |
| Custom domain | `start.empowrcic.org` |
| Branch | `master` |
| Base directory | `src` |
| Publish directory | `dist` |
| Framework | Astro |

Push to `master` — Netlify builds and deploys automatically. Use `/netlify-deploy` for domain/DNS changes.

---

## Related Projects

| Project | Relation |
|---|---|
| Empowr Heroes (`../empowr-heroes-nextjs/`) | Donation platform — linked from this page |
| Empowr Main Site (`../Empowr Main Site/`) | Main CIC website — linked from this page |
| Empowr EELA (`../Empowr EELA/`) | Sessions platform — linked from this page |
