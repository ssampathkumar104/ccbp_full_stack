# CCBP Introduction to HTML and CSS — Complete Syllabus

## Progress Tracker

| Module | Status |
|--------|--------|
| Module 1: Foundations & Architecture | ✅ Complete |
| Module 2: Intermediate Mastery | ⬜ Not Started |
| Module 3: Advanced Concepts | ⬜ Not Started |
| Module 4: Ecosystem, Testing & Production Readiness | ⬜ Not Started |

---

## Module 1: Foundations & Architecture ✅

### 1.1 — HTML Document Structure
- DOCTYPE, `<html>`, `<head>`, `<body>` anatomy
- How browsers parse HTML (DOM construction)
- The role of `<link>` and `<script>` tags in the `<head>`

### 1.2 — Core HTML Elements
- Block vs inline elements (`<div>`, `<p>`, `<h1>`–`<h6>`, `<span>`)
- Semantic meaning and why element choice matters
- Buttons, images (`<img>`), anchors (`<a>`), lists (`<ol>`, `<ul>`)

### 1.3 — CSS Fundamentals: Selectors & Properties
- Linking CSS (`<link rel="stylesheet">` vs inline vs internal)
- Element selectors, class selectors, ID selectors
- Core properties: `color`, `background-color`, `font-family`, `font-size`, `font-weight`, `text-align`, `text-decoration`

### 1.4 — The CSS Box Model
- Content → Padding → Border → Margin
- `border-width`, `border-style`, `border-color`, `border-radius`
- `padding` shorthand and directional variants
- `margin` shorthand, auto margins, and margin collapse

### 1.5 — Units of Measurement
- Absolute: `px`
- Relative: `%`, `vh`, `vw`, `em`, `rem`
- When to use which unit (design rationale from this project)

### 1.6 — CSS Backgrounds
- `background-color`, `background-image: url()`
- `background-size: cover` vs `contain`
- `background-position`, `background-repeat`
- Full-viewport background pattern (`height: 100vh; width: 100vw;`)

### 1.7 — Google Fonts Integration
- `@import url(...)` pattern
- Font stacks and fallback strategy
- Font families used in this project (Roboto, Bree Serif, Caveat, Lobster, etc.)

---

## Module 2: Intermediate Mastery

### 2.1 — Flexbox Layout (via Bootstrap Utilities)
- `d-flex`, `flex-row`, `flex-column`
- `justify-content-start`, `justify-content-center`, `justify-content-end`, `justify-content-between`
- `align-items-center`
- Nesting flex containers

### 2.2 — Bootstrap 4 Grid System
- `container` → `row` → `col-*` hierarchy
- 12-column math
- Responsive breakpoints: `col-sm-*`, `col-md-*`, `col-lg-*`, `col-xl-*`
- Combining multiple breakpoint classes on one element

### 2.3 — Card-Based UI Patterns
- Building cards with custom CSS (background, border-radius, padding)
- Image + text horizontal cards using flexbox
- Vertical product cards (Shopping Card pattern)
- Card containers with shadow and spacing

### 2.4 — Bootstrap Navigation Bars
- `navbar`, `navbar-expand-lg`, `navbar-light`/`navbar-dark`
- `navbar-brand` with logo image
- `navbar-toggler` for mobile hamburger menu
- `collapse`, `navbar-collapse`, `navbar-nav`, `nav-link`
- `ml-auto` for right-aligned nav items

### 2.5 — Bootstrap Carousel Component
- `carousel slide`, `data-ride="carousel"`
- `carousel-indicators`, `carousel-inner`, `carousel-item`
- Previous/Next controls with `carousel-control-prev`/`next`
- Multiple carousels on one page (unique IDs)

### 2.6 — Embedding External Content
- Bootstrap `embed-responsive` wrapper
- `embed-responsive-16by9` aspect ratio class
- YouTube iframe embedding

### 2.7 — Multi-Section SPA Navigation (CCBP UI Kit)
- Architecture: all "pages" as `<div id="section...">` in one HTML file
- The `display('sectionId')` JavaScript function
- `onclick` handlers for navigation
- Navigation flow: Home → List → Detail → Back

---

## Module 3: Advanced Concepts

### 3.1 — CSS Specificity & the Cascade
- Specificity scoring: inline > ID > class > element
- How the cascade resolves conflicts
- Exercises from Specificity Practice 1–6
- `!important` and why to avoid it

### 3.2 — Responsive Web Design Principles
- Mobile-first vs desktop-first
- Bootstrap breakpoint system internals (576px, 768px, 992px, 1200px)
- How `col-12 col-sm-6 col-md-4 col-lg-3` stacks/unstacks
- Responsive images with `img-fluid` and `w-100`

### 3.3 — CSS Gradients & Advanced Backgrounds
- Linear gradients (`background-image: linear-gradient(...)`)
- Overlay techniques
- Fixed backgrounds vs scrolling backgrounds

### 3.4 — Multi-Page Website Architecture
- Section-based SPA pattern vs true multi-page
- The `ccbp-ui-kit.js` show/hide mechanism
- State management via DOM visibility
- Back navigation patterns
- Trade-offs: single-file simplicity vs code maintainability

### 3.5 — Building a Complete Responsive Website
- Anatomy of the Food Munch project (most complex exercise)
- Fixed navbar with smooth scroll to sections
- Responsive grid for menu items (col-12 → col-md-6 → col-lg-3)
- Image ordering with Bootstrap `order-*` classes
- Footer and social media icon integration (Font Awesome)
- `d-none` / `d-md-block` for conditional visibility

### 3.6 — CSS Reusability Patterns
- Utility-first approach (Bootstrap classes)
- Component-scoped custom CSS
- When to use Bootstrap vs custom styles
- Naming conventions: BEM-like kebab-case

---

## Module 4: Ecosystem, Testing & Production Readiness

### 4.1 — CDN Architecture & Dependency Management
- Why CDN over local files (performance, caching, availability)
- Integrity hashes (`integrity="sha384-..."`) and SRI (Subresource Integrity)
- `crossorigin="anonymous"` attribute
- CDN failure scenarios and fallback strategies

### 4.2 — Browser Developer Tools for CSS
- Inspecting elements and computed styles
- Box model visualization in DevTools
- Live-editing CSS in the browser
- Responsive design mode / device emulation
- Network tab for verifying CDN loads

### 4.3 — Debugging Common CSS Issues
- Elements not visible (zero height, overflow hidden, display none)
- Styles not applying (specificity conflicts, typos, wrong selector)
- Layout breaking (missing container/row, wrong column math)
- Background images not loading (path issues, CORS)
- Carousel not working (missing jQuery/Popper, duplicate IDs)

### 4.4 — Code Organization & Maintenance
- One `index.html` + one `style.css` per exercise
- Extracting reusable CSS patterns
- When a single-file approach becomes technical debt
- Refactoring opportunities in this codebase

### 4.5 — Deployment & Hosting Static Sites
- Opening HTML files directly in a browser
- Local development servers (Live Server extension)
- Deploying to GitHub Pages, Netlify, Vercel
- Asset path considerations (relative vs absolute URLs)

### 4.6 — Accessibility & Best Practices
- `alt` attributes on images
- `aria-hidden`, `aria-label`, `aria-controls`
- `sr-only` class for screen readers
- Semantic HTML vs `<div>` soup
- Color contrast and readability

### 4.7 — Performance Optimization for Static Sites
- Minimizing HTTP requests (CDN consolidation)
- Image optimization (appropriate sizes, formats)
- CSS file size and specificity overhead
- Render-blocking resources (`<link>` in head vs deferred)
- Lighthouse audits
