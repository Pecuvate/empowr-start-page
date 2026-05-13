# design

Handles all Astro component markup, Tailwind styling, brand token adjustments, and copy editing for the landing page.

## Process

1. Run `npm run dev` — dev server starts at `http://localhost:4321`
2. Edit components in `src/components/`, page in `src/pages/index.astro`, or tokens in `src/styles/globals.css`
3. Verify layout in browser at 480px viewport width
4. Confirm brand tokens are used — do not introduce arbitrary colour values outside `globals.css`

## Inputs and Outputs

- In: copy changes, design feedback, brand direction
- Out: updated `landing.page.guide.html`

## Tools

- webapp-testing — Playwright browser preview and screenshot capture at 480px mobile viewport

## Constraints

- Stack: Astro 6 + Tailwind v4 via PostCSS (`postcss.config.mjs`) — do not switch to the `@tailwindcss/vite` plugin (incompatible with Astro 6's rolldown resolver)
- Typography: `Nunito` (`font-sans`) for body, `Playfair Display` (`font-serif`) for hero `h1` only — do not apply `font-serif` elsewhere
- Brand tokens live in `src/styles/globals.css` under `@theme` — all custom colours registered there
- Max viewport width is 480px (`max-w-[480px]` on body) — all layout decisions must be mobile-first
- `landing.page.guide.html` is the original design reference — do not edit it
