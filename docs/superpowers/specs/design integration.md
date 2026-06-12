# Client Photo Integration — Design

**Date:** 2026-06-08
**Source:** `~/Desktop/Final Website Photos (edited)/` (client-supplied, organized by page)

## Goal
Place every client-supplied photo into its matching section of the site. Where a
section is currently icon- or text-only, **add** an image slot (full integration).

## Decisions (approved)
1. **Full integration** — add image slots to currently icon/text-only sections.
2. **Home hero photo** replaces the stats `HeroProofCard` in the hero right column
   (stats remain in the `StatsBar` below).
3. **Optimize images** — convert client PNGs → JPG via `sips`, max ~1400px (1800px for
   heroes/banners), quality ~82. Output to `public/photos/`.
4. **Projects** — replace the 9 projects with the client's; titles from photo filenames,
   captions/categories from the PPTX + client-provided fill for gaps.

## Image conversion
All PNGs → `public/photos/<name>.jpg`. Naming scheme below. The conversion is driven by
`scripts/convert-client-photos.sh` (idempotent; re-run safe).

## Per-page mapping

### Home (`HomePage.jsx`)
| Client file | Target | Slot |
|---|---|---|
| Home Page Main Hero Photo | `home-hero.jpg` | Hero right column (replaces HeroProofCard) |
| Who We Work With/Dealers & PMs | `audience-dealer.jpg` | Audience card 1 (overwrite) |
| Who We Work With/Enterprise Clients & Facility Teams | `audience-enterprise.jpg` | Audience card 2 (overwrite) |
| Why OSI (tiles)/Dock to Done | `why-dock-to-done.jpg` | WhyOSI tile "Dock to done" |
| Why OSI (tiles)/Real Infrastructure | `why-real-infrastructure.jpg` | WhyOSI tile "Real infrastructure" |
| Why OSI (tiles)/Total Project Support | `why-total-support.jpg` | WhyOSI tile "Total project support" |
| Why OSI (tiles)/Dealer & Facility Team Fluency | `why-dealer-fluency.jpg` | WhyOSI tile "Dealer and facility team fluency" |
| Services (tiles)/* (6) | `service-tile-<slug>.jpg` | SERVICES[].img (icon→photo; used on Home + Services landing) |

### Services (`ServicesPage.jsx`, `tokens.js`)
- Landing: `services-what-we-offer.jpg`; client-group cards `services-group-dealers.jpg`,
  `services-group-enterprise.jpg`; 4 Why-OSI tiles `services-why-{organized,complex,support,accountable}.jpg`.
- 6 detail pages (`SERVICE_PAGES[slug]`): add `introImg` (Services Overview), `whyImg` (Why OSI),
  and `extra.img` where the extra block exists:
  - installation → overview/why/extra(What We Install)
  - warehousing → overview/why/extra(Why it Matters)
  - asset-management-storage → overview/why/extra(Why it Matters)
  - mac-day2 → overview/why/extra(Who This is For)
  - modular-walls → overview/why (no extra)
  - decommissioning → overview/why (no extra)
  - Names: `svc-<key>-{overview,why,extra}.jpg`

### Industries (`IndustriesPage.jsx`, `tokens.js`)
- Landing: `industries-our-approach.jpg`; 5 env tiles → `INDUSTRIES[].img` = `ind-tile-<slug>.jpg`;
  4 Why-OSI tiles `industries-why-{every-env,beyond,infrastructure,dependable}.jpg`.
- 5 detail pages (`INDUSTRY_PAGES[slug]`): hero `img` = `ind-tile-<slug>.jpg`; add `introImg`
  (Environment Overview) and `whyImg` (Why OSI): `ind-<slug>-{overview,why}.jpg`.

### About (`AboutPage.jsx`)
| Client file | Target | Slot |
|---|---|---|
| Our Approach | `about-our-approach.jpg` | "Our Approach" section (add image) |
| What Makes OSI Different | `about-different.jpg` | "What Makes OSI Different" dark section (add image) |
| OSI Building | `osi-building.jpg` | Building banner (overwrite; shared with Contact) |
| Operations (tiles)/* (6) | `about-ops-<key>.jpg` | Operations tiles (overwrite existing) |

### Contact (`ContactPage.jsx`)
- Building photo → `osi-building.jpg` (same file as About; no code change needed).

### Projects (`tokens.js`, `ProjectsPage.jsx`)
Replace `PROJECTS` with the 9 below. Photos `project-<key>.jpg`.

| Title | cat | result |
|---|---|---|
| Corporate Campus Installation | Corporate | Installed 220 workstations with curved monitors and privacy screens across 3 floors. |
| Custom Furniture Installation | Corporate | Received, delivered, and installed custom modular furniture for a national news station. |
| Training Center Buildout | Education | Reconfigured training room tables, power connections, and AV furniture with 24-hours notice. |
| Dedicated Asset Management | Corporate | Over 25,000 sq ft of dedicated asset management space for a large publicly traded company. |
| Sportsbook Installation | Hospitality | High-end sportsbook arena installation for a national basketball franchise. |
| Quad Privacy Booth | Corporate | Installed phone booths and meeting pods across a 60,000 sq ft corporate floor. |
| Wire-Frame Pod & Lounge | Corporate | Architectural pod and lounge seating installed in a new corporate lobby. |
| Café & Lounge Installation | Hospitality | Collaborative lounge, café seating, and booth furniture delivered for a corporate amenity space. |
| Downtown Tower Restack | Corporate | Multi-floor workstation reconfiguration completed over three weekends with active employees. |

(Categories drive the Projects filter: All/Corporate/Healthcare/Education/Hospitality/Government.)

## Verification
- `npm run build` and `npm run lint` pass.
- Spot-check pages in dev server; confirm no broken/placeholder images.
</content>
</invoke>
