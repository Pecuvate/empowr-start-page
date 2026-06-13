# Tech Stack & Design System — Empowr Landing Page

Reference for the start.empowrcic.org link-in-bio hub. For content edits and markup see `design/CONTEXT.md`. For image assets and URLs see `publish/CONTEXT.md`.

---

## Framework & Runtime

| Layer | Technology | Version | Notes |
|---|---|---|---|
| Framework | Astro (SSG) | `^6.3.1` | Static site — no server runtime, no API routes |
| Language | TypeScript | — | Strict mode via `astro/tsconfigs/strict` |
| Styling | Tailwind CSS v4 | `^4.3.0` | via `@tailwindcss/postcss` PostCSS plugin |
| Build output | Static HTML/CSS/JS | — | Outputs to `dist/` — no server-side rendering |
| Package manager | npm | — | — |

**This is the only project in the Empowr CIC workspace that uses Astro** — all others use Next.js. Chosen because the landing page is pure marketing content with no dynamic data requirements.

---

## Dependencies

| Package | Version | Purpose |
|---|---|---|
| `astro` | `^6.3.1` | Framework — components, layouts, pages, SSG build |
| `tailwindcss` | `^4.3.0` | CSS framework |
| `@tailwindcss/postcss` | `^4.3.0` | Tailwind v4 PostCSS integration |

No backend dependencies. No Supabase, Stripe, Resend, or any API client — this is a purely static site.

---

## Source Structure

```
src/
├── components/
│   └── LinkButton.astro       Reusable icon + label button (3 variants)
├── layouts/
│   └── Layout.astro           Root HTML shell — meta, Google Fonts, 480px container
├── pages/
│   ├── index.astro            Main landing page (5 sections)
│   └── quiz.astro             Session-finder quiz (7 questions, 7 outcomes)
└── styles/
    └── globals.css            Tailwind imports + @theme custom tokens
```

---

## Design System

### Styling Approach
Tailwind CSS v4 with `@theme` custom tokens defined in `src/styles/globals.css`. Tokens are used as Tailwind utilities (`bg-blue`, `text-gray`, `border-divider`) — never as arbitrary hex values in components.

**Important build constraint:** Do **not** switch to `@tailwindcss/vite` plugin — it is incompatible with Astro 6's rolldown resolver. The PostCSS pipeline (`postcss.config.mjs`) is the correct approach for this project.

### Color Palette

| Token | Value | Usage |
|---|---|---|
| `--color-blue` | `#4A6FD4` | Primary — buttons (dark variant), borders, text accents |
| `--color-blue-light` | `#7A9BE0` | Secondary blue accents |
| `--color-blue-pale` | `#C5D2F0` | Pale button variant background, stats cards |
| `--color-blue-soft` | `#E8EDF8` | Page background (outside the 480px card) |
| `--color-blue-card-badge` | `#D0DBF5` | Badge backgrounds inside cards |
| `--color-blue-card` | `#5B7FD8` | Darker blue for full-bleed card sections |
| `--color-green` | `#2DC653` | WhatsApp / action button variant |
| `--color-red` | `#E63946` | Accent (value prop inline text colouring) |
| `--color-text` | `#1a1a1a` | Primary body text |
| `--color-black` | `#111` | Heavy headings |
| `--color-gray` | `#666` | Secondary / meta text |
| `--color-divider` | `#ddd` | Section `<hr>` dividers |

**Note:** Landing Page uses a different blue family (`#4A6FD4`) to the Waivers brand blue (`#1a3faa`) and the Heroes blue (`#4A70C2`). These are intentionally distinct applications of the broader Empowr CIC brand.

### Typography

| Font | Weights | Usage | Loading |
|---|---|---|---|
| Nunito | 400, 600, 700, 800, 900 | Body, buttons, labels — `font-sans` | Google Fonts |
| Playfair Display | 700 | Hero `<h1>` only — `font-serif` | Google Fonts |

Both fonts loaded via `<link>` in `Layout.astro` with `preconnect` hints to `fonts.googleapis.com` and `fonts.gstatic.com` for performance.

### Layout

- **Max width:** 480px — mobile-first, the page is designed to be used on a phone
- **Desktop treatment:** The 480px card gets `sm:rounded-3xl sm:shadow-lg sm:my-8` — rounded card floating on the blue-soft background
- **Container:** `max-w-[480px] mx-auto bg-white overflow-hidden` in `Layout.astro`
- **Sections:** vertically stacked, separated by `<hr>` dividers with padding

### LinkButton Component

The only reusable UI component. Three variants:

| Variant | Background | Thumb | Text |
|---|---|---|---|
| `dark` | `bg-blue` (`#4A6FD4`) | `#3a5aaa` | White |
| `pale` | `bg-blue-pale` (`#C5D2F0`) | `#b0c0e8` | Blue |
| `green` | `bg-green` (`#2DC653`) | `#22a847` | White |

Layout: flex row, 70px icon thumbnail on left, label centred in remaining space, min-height 64px. All links open in `target="_blank"`.

---

## Deployment

| Setting | Value |
|---|---|
| Platform | Netlify |
| Domain | `start.empowrcic.org` |
| Branch | `master` (auto-deploy on push) |
| Build command | `npm run build` |
| Publish directory | `dist` |
| Node version | 22 |

**Security headers** applied globally via `netlify.toml`:
- `X-Frame-Options: DENY`
- `X-Content-Type-Options: nosniff`
- `Referrer-Policy: strict-origin-when-cross-origin`
- `Content-Security-Policy` — self, Google Fonts, HTTPS images, inline styles (Tailwind)

No environment variables required — fully static, no secrets.

---

## Key Architectural Decisions

### Static Only — No API Routes
No form handling, no backend, no auth. All interactive actions (donations, bookings, WhatsApp) are outbound links to other Empowr CIC platforms. This keeps the page fast, cheap to host, and zero-maintenance.

### 480px Mobile-First
Designed as a link-in-bio page — the primary entry point is an Instagram or social bio link, so the majority of visitors arrive on phones. The 480px constraint is enforced at the layout level, not with media queries.

### Astro Over Next.js
No dynamic data = no reason for SSR or a Node runtime. Astro outputs pure static HTML. Simpler, faster, lower hosting cost, no cold starts.

### Single `LinkButton` Component
All quick-access buttons share one component with variant props. Adding a new link button requires no new CSS — just a new `<LinkButton>` tag with `href`, `variant`, `icon`, and `label`.
