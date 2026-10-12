# Portfolio Changelog
## All Changes Made — Prashith Kumar G Portfolio Redesign

---

### BUGS FIXED

| File | Location | Bug | Fix Applied |
|------|----------|-----|-------------|
| `index.html` | `<img id="mypic"">` | Extra double-quote typo (`""`) broke HTML parsing | Corrected to single closing quote |
| `index.html` | `<p class="highlight" class="align">` | Duplicate `class=` attribute — only the first is read by browsers, `align` class was silently ignored | Merged into a single class attribute |
| `style.css` | `.container` | No `grid-template-columns` defined, so the two-column layout collapsed into one column on many browsers | Replaced with proper `grid-template-columns: 1fr 1fr` (now in hero grid) |
| `style.css` | `.btn` | Used `transform: translate(310px, -98px)` as a positional hack — broke at any screen width other than the one it was hard-coded for | Replaced with proper flex layout |
| `style.css` | `.hspace` | `margin-top: -60px` used as a layout spacer — fragile and overlaps on different viewports | Removed; replaced with proper grid/flex gap |
| `style.css` | `.skbox1–4` | All four used negative `margin-top` to simulate rows inside the grid — collapsed on resize | Replaced with a clean flex column inside each category card |
| `style.css` | `.aboutbox`, `.skillbox` | Fixed pixel widths (`width: 1100px`, `width: 1000px`) caused horizontal overflow on any screen narrower than those values | Replaced with fluid `max-width: 100%` and responsive grid |
| `style.css` | `.nav` | `margin-left: 33%` — nav links disappeared off-centre on mobile and tablets | Replaced with `display:flex; justify-content:space-between` layout |
| `index.html` | Hero section | No semantic `<section>` wrapper — content floated in body without landmark | Wrapped in `<section class="hero">` |
| `contact.html` | Commented-out form block | Large commented-out `<form>` block left in production HTML — increases file size and confuses future devs | Removed entirely |

---

### DESIGN CHANGES

#### style.css — Complete Rewrite
- **Design system**: Introduced CSS custom properties (`--bg-deep`, `--accent`, `--text-1`, etc.) for consistent theming across all pages.
- **Typography**: Replaced `Geneva/Verdana/Segoe UI` mix with a curated Google Fonts pair — `Playfair Display` (headings, serif) + `DM Sans` (body, modern).
- **Fluid type**: All font sizes now use `clamp()` — they scale smoothly between mobile and desktop without media query jumps.
- **Color palette**: Replaced the flat `rgb(52,42,42)` background with a layered dark editorial palette (`#181310` body → `#22190f` sections → `#2c2018` cards). Warm amber-orange accent (`#d97c4a`) replaces the old mixed gradient text.
- **Navigation**: Fixed position (`position:fixed`) with glassmorphism (`backdrop-filter:blur`) replaces the old static nav. Added animated underline hover effect. Added hamburger menu for mobile.
- **Hero layout**: Replaced the `display:grid` with no column definition — now properly `grid-template-columns: 1fr 1fr` with full responsive collapse.
- **Profile image**: Added a rotating dashed ring and radial glow behind the photo using `::before` / `::after` pseudo-elements.
- **Buttons**: Replaced the `transform:translate` button hack with two semantic classes — `btn-primary` (filled, accent colour) and `btn-ghost` (outlined). Both have hover, active, and focus states.
- **Social icons**: Replaced plain `<img>` links in a div with a styled `.social-icon` component — 40×40px, bordered, hover lift + colour shift.
- **Sections**: Each page section now has a consistent heading pattern: eyebrow label → h2 → orange divider line. Removes the inconsistent title styles across pages.
- **Scroll animations**: Added IntersectionObserver-driven `.reveal` and `.reveal-stagger` classes — elements fade and slide up as they enter the viewport. No third-party library needed.
- **Skill cards**: Replaced the four `skbox1–4` divs (with negative margins and padded-left hacks) with a clean auto-fit CSS grid of `.skill-cat` cards — one per category.
- **Project cards**: Each project now lives in a `.project-card` with a top-border reveal animation on hover, technology pills, and a category tag.
- **Contact page**: Replaced the raw `<button>` links with `.contact-link` components — icon + label + value, slide-right on hover.
- **Resume card**: Dedicated card on the contact page with a download button replacing the float-hacked `.btn` from the old layout.

#### Responsive (NEW — did not exist before)
- **≤900px (tablet)**: Hero collapses to single column, image moves above text, about stats go horizontal, contact grid collapses.
- **≤600px (mobile)**: Hamburger menu replaces nav links, all grids collapse to single column, section padding reduces, footer stacks vertically.

---

### FILE-BY-FILE SUMMARY

#### `index.html`
- Fixed `<img id="mypic"">` double-quote typo → `id="mypic"`
- Fixed duplicate `class="highlight" class="align"` → `class="highlight"`
- Removed inline `style=""` attributes — moved to CSS classes
- Replaced social icon `<div class="con">` + separate `.btn` with `.hero-actions` flex row and `.hero-socials` flex row
- Added `<nav class="nav">` with logo and hamburger toggle
- Added `<footer>` element

#### `about.html`
- Replaced `<div class="aboutbox">` fixed-width box with `<section id="about">` + responsive `about-grid`
- Added stat cards sidebar (years, technologies, projects, cloud)
- Replaced raw `<p class="aboutcontent">` with semantic `about-body` paragraphs with `<strong>` highlights
- Added `.about-tags` tag cloud at the bottom
- Added scroll reveal JS and hamburger toggle JS

#### `skill.html`
- Replaced `<div class="skillbox">` + four `.skbox1–4` rows (with negative margin hacks) with a CSS auto-fit grid of `.skill-cat` cards
- Each skill now has a `.skill-icon` container + `.skill-name` label, properly flexed
- Added scroll reveal JS and hamburger toggle JS

#### `project.html`
- Replaced `<div class="clg">` cards with `.project-card` components
- Added `.proj-tag` category badge, `.proj-title`, `.proj-desc`, and `.proj-tech` pill row to each project
- Added scroll reveal JS and hamburger toggle JS

#### `contact.html`
- Removed entire commented-out `<form>` block
- Replaced `<button class="cbtn">` links with `.contact-link` components (icon + label + value)
- Added dedicated `.resume-card` sidebar with download button
- Added scroll reveal JS and hamburger toggle JS

---
*Redesign complete — all five pages share one `style.css`, one nav pattern, one footer pattern, and one JS scroll-reveal pattern.*
