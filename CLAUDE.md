# CLAUDE.md — AI Assistant Guide for an-aurora-ui-demo

## Project Overview

**an-aurora-ui-demo** is a static HTML/CSS landing page and design system showcase for **Aurora UI** — a UI kit inspired by the northern lights, featuring gradient-rich, glassmorphic design aesthetics. It has zero build dependencies and no package manager.

---

## Repository Structure

```
an-aurora-ui-demo/
├── index.html          # Main marketing/landing page
├── styleguide.html     # Design system reference (colors, typography, cards)
├── assets/
│   └── css/
│       └── styles.css  # Single unified stylesheet (~724 lines)
├── README.md           # Minimal project title
└── CLAUDE.md           # This file
```

There is no `package.json`, no build system, no transpilation, and no framework. All code is vanilla HTML, CSS, and JavaScript.

---

## Development Workflow

### Running Locally

Since this is a purely static project, no build step is needed:

```bash
# Option 1: Python (usually pre-installed)
python3 -m http.server 8000

# Option 2: Node.js one-liner (no install)
npx serve .

# Option 3: Open directly in browser
open index.html
```

Then visit `http://localhost:8000`.

### Making Changes

1. Edit `index.html`, `styleguide.html`, or `assets/css/styles.css` directly.
2. Refresh the browser — no build step required.
3. Validate in a modern browser (Chrome 90+, Firefox 88+, Safari 14.1+).

### Deployment

Deploy by copying files to any static host (GitHub Pages, Netlify, Vercel, nginx, Apache). No build command is needed.

---

## Codebase Conventions

### CSS Architecture

All styles live in `assets/css/styles.css`. Follow these established patterns:

**CSS Custom Properties (Variables)**

All design tokens are defined on `:root`. Always use variables — never hardcode colors, radii, or shadows:

```css
/* Colors */
--color-bg: #050917;
--color-surface: rgba(255,255,255,0.04);
--color-accent: #76f9ff;       /* Cyan */
--color-cta: #b47aff;          /* Purple */

/* Gradients */
--gradient-aurora-primary: ...;
--gradient-aurora-secondary: ...;

/* Radii */
--radius-md: 18px;
--radius-lg: 24px;
--radius-pill: 999px;

/* Shadows */
--shadow-soft: ...;
--shadow-panel: ...;
```

**Class Naming — BEM-like**

Use a BEM-inspired pattern: `.block`, `.block__element`, `.block--modifier`:

```
.btn--primary        (modifier)
.plan--featured      (modifier)
.aurora-ring--secondary  (modifier)
```

**Responsive Design**

- Mobile-first: default styles target mobile.
- Single breakpoint via `@media (max-width: 640px)` where layout needs differ.
- Use `clamp()` for fluid sizing instead of multiple breakpoints.
- Use CSS Grid with `auto-fit` / `minmax` for responsive columns.

**Glassmorphism Pattern**

Cards and surfaces use: semi-transparent `rgba` background + `backdrop-filter: blur(...)` + `rgba` border.

**Animations**

Aurora ring animations use long durations (9–12s) and a `pulse` keyframe. Keep effects subtle and performance-friendly (use `transform` / `opacity` for animation, not layout properties).

### HTML Conventions

- Use semantic HTML5 elements (`<header>`, `<main>`, `<section>`, `<footer>`, `<nav>`).
- Every interactive element must have ARIA attributes (`aria-expanded`, `aria-controls`, `aria-label`).
- Decorative visual elements get `aria-hidden="true"`.
- Screen-reader-only text uses the `.sr-only` utility class.

### JavaScript Conventions

- Vanilla JavaScript only — no frameworks, no npm packages.
- Inline `<script>` tags at the bottom of `<body>`.
- Always guard DOM queries: check for element existence before attaching handlers.
- Keep ARIA attributes in sync with UI state (e.g., `aria-expanded` on menu toggle).

### Page Structure (`index.html`)

Each page shares the same header and footer. The landing page sections in order:

1. `<header>` — sticky nav with logo and mobile toggle
2. `.hero` — headline, description, CTA buttons, metrics
3. `.pillars` — three feature cards
4. `.showcase` — tag cloud + visual panel
5. `.pricing` — three pricing tiers (Starter $29 / Creator $79 / Studio $149)
6. `.cta` — email signup form
7. `<footer>` — links and copyright

### Styleguide (`styleguide.html`)

Documents the design tokens and components visually. When adding new components or changing design tokens, update `styleguide.html` to reflect the change.

---

## Design System Reference

| Token | Value | Usage |
|-------|-------|-------|
| `--color-bg` | `#050917` | Page background |
| `--color-surface` | `rgba(255,255,255,0.04)` | Card surfaces |
| `--color-accent` | `#76f9ff` | Cyan highlights, links |
| `--color-cta` | `#b47aff` | Purple CTAs, featured elements |
| `--radius-md` | `18px` | Standard card radius |
| `--radius-lg` | `24px` | Large card radius |
| `--radius-pill` | `999px` | Pill-shaped buttons/tags |

**Font:** Inter (Google Fonts, weights 400–700). Falls back to system-ui.

---

## Key Constraints

- **No build tools.** Do not add Webpack, Vite, Rollup, etc. unless explicitly requested.
- **No frameworks.** Do not add React, Vue, Alpine.js, etc. unless explicitly requested.
- **No package.json.** Do not create one unless the project scope changes.
- **Single CSS file.** Keep all styles in `assets/css/styles.css`. Do not split into multiple files unless the project grows significantly.
- **Accessibility.** Maintain semantic HTML and ARIA attributes on all interactive elements.
- **Performance.** Animate only `transform` and `opacity`. Avoid layout-triggering properties in animations.

---

## Git Workflow

```bash
# Check current branch
git branch --show-current

# Stage and commit
git add index.html styleguide.html assets/css/styles.css
git commit -m "descriptive message"

# Push to remote
git push -u origin <branch-name>
```

Feature branches follow the pattern: `claude/<description>-<session-id>`.

---

## Browser Compatibility Target

| Browser | Minimum Version |
|---------|----------------|
| Chrome  | 90+ |
| Firefox | 88+ |
| Safari  | 14.1+ |
| Edge    | 90+ |

Required CSS features: CSS Custom Properties, CSS Grid, `backdrop-filter`, `clamp()`, radial gradients.

---

## External Dependencies

- **Google Fonts (Inter)** — loaded via `<link>` in `<head>`. Requires internet connection; system fonts are the fallback.
- No other external dependencies.
