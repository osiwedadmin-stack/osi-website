# OSI Website

Commercial furniture services company website — Phoenix, AZ. React SPA with hash-based routing.

## Tech Stack

- **Framework**: React 19 + Vite 8
- **Styling**: Tailwind CSS 4 (via `@tailwindcss/vite`, no separate config file)
- **Animation**: Framer Motion 12
- **Icons**: Lucide React
- **Routing**: Custom hash-based router (`src/components/Router.jsx`) — no React Router
- **Language**: JavaScript/JSX only (no TypeScript)

## Commands

- `npm run dev` — Start dev server (Vite HMR)
- `npm run build` — Production build to `dist/`
- `npm run lint` — ESLint
- `npm run preview` — Preview production build

## Project Structure

```
src/
├── main.jsx                    # Entry point (React 19 strict mode)
├── App.jsx                     # Root component, route definitions, providers
├── index.css                   # Tailwind imports, @theme, global styles
├── data/
│   └── tokens.js               # ALL content & design tokens (services, industries, projects, reviews, colors)
├── components/
│   ├── Router.jsx              # Hash-based router with useRoute() hook
│   ├── Primitives.jsx          # Container, Section, Button, Eyebrow, SectionHeading, StatPill, Green, OSILogo, ImgOrPlaceholder
│   ├── Motion.jsx              # FadeIn, Stagger, StaggerItem, CountUp, RotatingWord, MagneticButton
│   ├── Nav.jsx                 # Sticky nav with desktop dropdowns + mobile slide-in menu
│   ├── Footer.jsx              # Dark footer with 4-column grid
│   ├── QuoteModal.jsx          # Quote request modal + QuoteProvider context
│   ├── FinalCTA.jsx            # Reusable end-of-page CTA section
│   └── Icon.jsx                # Lucide icon wrapper
└── pages/
    ├── HomePage.jsx            # Hero with RotatingWord, stats, services grid, projects, reviews
    ├── ServicesPage.jsx        # Landing (/services) + dynamic subpages (/services/:slug)
    ├── IndustriesPage.jsx      # Landing (/industries) + dynamic subpages (/industries/:slug)
    ├── ProjectsPage.jsx        # Filterable project gallery
    ├── AboutPage.jsx           # Company story, team, infrastructure
    ├── ContactPage.jsx         # Quote form + contact info + Google Maps
    └── NotFoundPage.jsx        # 404 page
```

## Routes

| Path | Component | Notes |
|------|-----------|-------|
| `/` | HomePage | Main landing |
| `/services` | ServicesLandingPage | All services overview |
| `/services/:slug` | ServiceSubpage | 6 service detail pages |
| `/industries` | IndustriesLandingPage | All industries overview |
| `/industries/:slug` | IndustrySubpage | 5 industry detail pages |
| `/projects` | ProjectsPage | Filterable portfolio |
| `/about` | AboutPage | Company info |
| `/contact` | ContactPage | Supports `?topic=dealer` or `?topic=enterprise` prefill |
| `*` | NotFoundPage | 404 |

## Design System

### Colors

| Token | Hex | Usage |
|-------|-----|-------|
| Primary Green | `#6DFF00` | Brand accent, buttons, highlights |
| Dark Green | `#5AD400` | Hover states |
| Light Green | `#9BFF5A` | Light accent |
| Green Tint | `#E4FFC9` | Subtle backgrounds |
| Charcoal | `#1A1A1A` | Primary text, dark backgrounds |
| Dark Gray | `#4A4A4A` | Secondary text |
| Mid Gray | `#8A8A8A` | Tertiary text |
| Border Gray | `#EAEAEA` | Borders, dividers |
| Light BG | `#F4F4F4` | Subtle backgrounds |
| Warm White | `#F9F9F5` | Hero/section backgrounds |
| Dark BG | `#0E0E0E` | Dark sections, mobile menu |

### Typography

| Font | Variable | Usage |
|------|----------|-------|
| Archivo | `font-display` | Headings — always `font-black` |
| Inter | `font-sans` | Body text |
| JetBrains Mono | `font-mono` | Labels, technical text |

Heading scale: `text-[76px]` (hero h1) > `text-[56px]` (section h2) > `text-[28px]` (card h3)

### Layout

- Container: `max-w-[1320px]` with `px-6 md:px-10`
- Grid: 12-column system (`lg:grid-cols-12`)
- Section padding: `py-24 md:py-32`
- Animation easing: `[0.16, 1, 0.3, 1]` (used everywhere)

### Button Variants

`primary` | `outlineDark` | `outlineLight` | `ghost` | `ghostLight` | `dark`

All buttons: `rounded-full`, magnetic hover by default, focus-visible ring with brand green.

### Animation Patterns

- `FadeIn`: Viewport-triggered, `y=24px`, `0.7s` duration
- `Stagger`/`StaggerItem`: Staggered children entrance
- `RotatingWord`: Cycling text with vertical slide, `2800ms` interval
- `MagneticButton`: Cursor-following hover, strength `0.18`
- `CountUp`: Number counter on scroll
- All respect `prefers-reduced-motion`

## Content Architecture

All business content lives in `src/data/tokens.js`:
- `SERVICES` — 6 services with slugs, titles, blurbs, icons
- `SERVICE_PAGES` — detailed content for each service subpage
- `INDUSTRIES` — 5 industries
- `INDUSTRY_PAGES` — detailed content for each industry subpage
- `PROJECTS` — 9 portfolio projects with categories for filtering
- `MANUFACTURERS` — 16 partner brands (Steelcase, MillerKnoll, Haworth, etc.)
- `CLIENT_LOGOS` — 5 enterprise clients (Choice Hotels, Wells Fargo, Amazon, State Farm, Phoenix Suns)
- `REVIEWS` — 6 customer testimonials

To add/edit content, modify `tokens.js` — pages render dynamically from this data.

## Key Patterns

- **No React Router** — custom hash router in `Router.jsx`, navigate with `<Link to="/path">`
- **QuoteModal** — accessed via `useQuote()` hook from `QuoteModal.jsx`, wrap app in `QuoteProvider`
- **Dark sections** — pass `dark` prop to `Section` and `SectionHeading`
- **Images** — use `ImgOrPlaceholder` for graceful fallback to diagonal-stripe placeholder
- **Logo** — `OSILogo` component renders `/osi_logo_main.svg` from `public/`, supports `variant="dark"` (default) and `variant="light"` (applies `brightness-0 invert` filter)

## Static Assets

- `public/osi_logo_main.svg` — main company logo
- `public/favicon.svg` — browser favicon
- `public/icons.svg` — icon sprite
