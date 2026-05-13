# publish

Handles image asset replacement, URL wiring, and deployment of the landing page to its live domain.

## Process

1. Replace each `<div class="image-placeholder">` with an `<img>` using `object-fit: cover` inside the existing wrapper
2. Wire all `href="#"` links to confirmed live URLs (see Constraints for known targets)
3. QA at 480px on mobile and desktop using webapp-testing
4. Deploy via Netlify — see `f:\Projects\_config\guides\deployment.md`

## Inputs and Outputs

- In: real image files, confirmed destination URLs from each programme or platform
- Out: live production landing page

## Tools

- webapp-testing — cross-browser QA and screenshot capture

## Constraints

- Images: `<img>` with `object-fit: cover` inside existing wrappers — do not alter wrapper dimensions
- Known URL targets to wire:
  - Sk8 Skool (15+) button → booking page URL
  - Empowr shop button → shop URL
  - WhatsApp notification button → `wa.me/` link
  - Kids Space card link → kidz space page URL
  - Adults "Find Your Session" button → session finder URL
  - Donate card / Heroes button → `hero.empowrcic.org`
  - Volunteering, donating skates, collaboration, enquiries buttons → respective pages or `mailto:` links
- Do not change any CSS or HTML structure in this workspace — markup changes belong in design/
