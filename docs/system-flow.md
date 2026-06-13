# System Flow — Empowr Landing Page

What the site does, page by page. For tech details see `docs/tech-stack.md`. For content edits see `design/CONTEXT.md`.

---

## Overview

Two pages. No forms, no auth, no backend.

```
start.empowrcic.org/        Link-in-bio hub — 5 sections routing to all Empowr services
start.empowrcic.org/quiz    Session-finder quiz — 7 questions → 1 of 7 session recommendations
```

---

## Landing Page (`/`)

Single scrolling page with 5 sections separated by dividers.

---

### Section 1 — Hero

The first thing visitors see. Establishes identity and social proof.

- **Logo** — Empowr CIC circular logo badge (above-fold, not lazy-loaded)
- **Heading** — "Empowr CIC" (Playfair Display, 42px — only serif use on the page)
- **Social handle** — "@empowr.cic" (gray, links to Instagram)
- **Value prop** — Three-line mantra with inline colour coding:
  - "Live by growing." (red)
  - "Grow by learning." (blue)
  - "Learn by doing." (black)
- **Trust badge** — "EMPOWERING THE COMMUNITY, TRUSTED BY MANY"
- **Description paragraph** — Explains who Empowr CIC is and what they do
- **Quiz CTA** — "✨ Discover Your Next Session 🛼" → `/quiz`
- **Stats grid** — 3 cards: 25K+ Attendances / 10K+ Students / 5+ Locations

---

### Section 2 — Quick Links + Kids Space

Primary navigation links and the children's programme entry point.

**Three `LinkButton` components:**

| Button | Variant | Destination |
|---|---|---|
| 🏠 Empowr Home | dark | `https://www.empowrcic.org` |
| 🛒 Empowr Shop | pale | `https://empowrcic.wixsite.com/empowrcic/shop` |
| 💬 WhatsApp Notification | green | WhatsApp group invite link |

**Kids Space card:**
- Photo of children roller skating (lazy-loaded)
- Age badge: "AGES 5 YEARS – 15 YEARS"
- Heading: "Roller Skating For Children"
- Description: classes, camps, discos
- Link: "Open kidz space ~>" → `https://eela.empowrcic.org/kids-space`

---

### Section 3 — Adults + Trusted By

Adult programme entry point with institutional trust signals.

**Adults card** (full blue-card background `#5B7FD8`):
- Photo of adults learning to skate (lazy-loaded)
- Badge: "THROUGH HANDS-ON EXPERIENCES..." (white, uppercase)
- Heading: "Learning as Adults (15+)" (white)
- Description: Sk8 Skool, SYNKRON8, skate jams
- CTA: "FIND YOUR SESSION 🛼" → `https://eela.empowrcic.org/adults`

**Trusted By logos:**
- Lewisham Council
- Department for Education (DfE)
- Young Mayor of Lewisham

---

### Section 4 — Social Proof + Donate

Community validation and fundraising entry point.

**Trustpilot review card:**
- Star rating icon
- "Rated excellent by our members" with link to `https://uk.trustpilot.com/review/empowrcic.org`
- Featured review quote

**Heroes donation card** (blue-card background):
- Community photo (lazy-loaded)
- Heading: "**REAL CHANGE** STARTS HERE" — "REAL CHANGE" in gold (`#FFD700`)
- Description: explains how donations fund the mission
- CTA: "🏆 BECOME A HERO TODAY ~>" → `https://hero.empowrcic.org/`

---

### Section 5 — Get Involved

Four community engagement pathways at the foot of the page.

| Button | Variant | Destination |
|---|---|---|
| 🙋 Volunteering | pale | `mailto:general@empowrcic.org` |
| 🛼 Donating Skates | dark | `https://www.empowrcic.org/b4e` |
| 🤝 Collaboration | pale | `mailto:general@empowrcic.org` |
| ✉️ General Enquiries | dark | `mailto:general@empowrcic.org` |

---

## Session Finder Quiz (`/quiz`)

A 7-question branching quiz that recommends the right roller skating session for each visitor. Entry point: the "Discover Your Next Session" CTA on the landing page.

**UI elements:**
- Progress bar (fills as questions are answered)
- Question counter ("Question X of 7")
- Yes/No buttons (some with custom labels e.g. "Children's classes" / "Fun session")
- Result card: session tag, name, description, booking link, "Start again" button

### Decision Tree

```
Are you booking for a child aged 5–15?
├── YES → Would you like to join in and skate together?
│         ├── YES → Are you both beginners looking to learn and level up?
│         │         ├── YES → Sk8 Skool for All Ages
│         │         └── NO  → All Ages Roller Disco
│         └── NO  → What are you looking for?
│                   ├── Children's classes → Sk8 Skool 4 Kidz
│                   └── Fun session        → All Ages Roller Disco
│
└── NO  → Are you a beginner roller skater looking to level up?
          ├── YES → Are you looking for a structured course?
          │         ├── YES → Sk8 Skool (15+)
          │         └── NO  → Do you want dance routines on skates?
          │                   ├── YES → SYNKRON8 Roller Dance
          │                   └── NO  → Relaxed community session?
          │                             ├── YES → Skate Jam (15+)
          │                             └── NO  → Sk8 Skool (15+)
          │
          └── NO  → Do you enjoy dancing or moving to music?
                    ├── YES → SYNKRON8 Roller Dance
                    └── NO  → Relaxed open session?
                              ├── YES → Skate Jam (15+)
                              └── NO  → What are you looking for?
                                        ├── Skate socially        → Skate Jam (15+)
                                        └── Special event night   → Roller Skate Events (15+)
```

### Session Outcomes

| Session | Age | Description | Booking Link |
|---|---|---|---|
| Sk8 Skool 4 Kidz | 5–12 | Structured children's classes | `empowrcic.org/kidzspace` |
| Sk8 Skool for All Ages | All 5+ | Family co-learning sessions | `empowrcic.org/kidzspace` |
| All Ages Roller Disco | All 5+ | Lights, music, fun for everyone | `empowrcic.org/kidzspace` |
| Sk8 Skool (15+) | 15+ | Structured beginner adult course | `empowrcic.org/sk8-skool` |
| SYNKRON8 Roller Dance | 15+ | Weekly beginner roller dance with music | `empowrcic.org/sk8-skool` |
| Skate Jam (15+) | 15+ | Open community session, relaxed, social | `empowrcic.org/sk8-skool` |
| Roller Skate Events (15+) | 15+ | One-off special themed event nights | `empowrcic.org/roller-skate-events` |

---

## Link Map — Full Outbound URLs

| Section | Label | Destination |
|---|---|---|
| Hero | Quiz CTA | `/quiz` (internal) |
| Quick Links | Empowr Home | `https://www.empowrcic.org` |
| Quick Links | Empowr Shop | `https://empowrcic.wixsite.com/empowrcic/shop` |
| Quick Links | WhatsApp | WhatsApp group invite |
| Kids | Kidz Space link | `https://eela.empowrcic.org/kids-space` |
| Adults | Find Your Session | `https://eela.empowrcic.org/adults` |
| Social Proof | Trustpilot | `https://uk.trustpilot.com/review/empowrcic.org` |
| Donate | Become a Hero | `https://hero.empowrcic.org/` |
| Get Involved | Volunteering | `mailto:general@empowrcic.org` |
| Get Involved | Donating Skates | `https://www.empowrcic.org/b4e` |
| Get Involved | Collaboration | `mailto:general@empowrcic.org` |
| Get Involved | General Enquiries | `mailto:general@empowrcic.org` |
