# Module 1: Foundations & Architecture — Complete Notes

---

## Topic 1.1 — HTML Document Structure

### Core Concepts

Every web page is an HTML document with three required parts:

```html
<!DOCTYPE html>          <!-- Tells browser: use HTML5 standards mode -->
<html>                   <!-- Root element of the DOM tree -->
    <head>               <!-- Metadata: invisible, holds resource links -->
        <link rel="stylesheet" href="style.css">
    </head>
    <body>               <!-- Visible content: what the user sees -->
        <h1>Hello</h1>
    </body>
</html>
```

### How the Browser Processes HTML

```
1. <!DOCTYPE html> → Switches to standards mode (not quirks mode)
2. <html>          → Creates root node of the DOM tree
3. <head>          → Processes metadata, loads CSS (render-blocking) and JS (parser-blocking)
4. <body>          → Constructs visible DOM nodes, paints to screen
```

### Bootstrap CDN Dependency Order

Scripts must be loaded in this exact sequence:

```
1. jQuery (no dependencies)
2. Popper.js (standalone, but Bootstrap needs it)
3. Bootstrap JS (depends on BOTH jQuery and Popper)
```

If reversed, Bootstrap components (carousels, navbars, dropdowns) silently fail.

### Key Attributes

| Attribute | Purpose |
|-----------|---------|
| `integrity="sha384-..."` | SRI hash — browser verifies CDN file isn't tampered with |
| `crossorigin="anonymous"` | Required for SRI to work on cross-origin resources |
| `rel="stylesheet"` | Tells browser this link is a CSS file |

### Gotchas

- **Missing DOCTYPE** → Quirks mode (unpredictable box model rendering)
- **CSS in body** → Flash of Unstyled Content (FOUC)
- **Scripts before dependencies** → Silent failures

---

### Mastery Checkpoint — Answers

**Q1: What happens if you remove `<!DOCTYPE html>`?**  
Browser enters quirks mode. The box model changes unpredictably — `width` might include padding/border in some browsers but not others. Margins, tables, and spacing behave inconsistently across browsers.

**Q2: Why must jQuery load before Bootstrap's JS?**  
Bootstrap's JavaScript internally calls `jQuery(...)` and `Popper.createPopper(...)`. If those aren't loaded yet, Bootstrap hits undefined references and throws errors. Carousels, dropdowns, and navbar toggles break silently.

**Q3: What does the `integrity` attribute do?**  
It contains a cryptographic hash of the expected file contents. Browser downloads the file, computes its hash, and compares. If they match → load it. If they don't match (file was tampered with) → block it. This is Subresource Integrity (SRI).

**Hands-On — Complete Answer:**

```html
<!DOCTYPE html>
<html>
    <head>
        <link rel="stylesheet" type="text/css" href="style.css">
        <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" 
              integrity="sha384-JcKb8q3iqJ61gNV9KGb8thSsNjpSL0n8PARn9HuZOnIxN0hoP+VmmDGMN5t9UJ0Z" 
              crossorigin="anonymous">
        <script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" 
                integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" 
                crossorigin="anonymous"></script>
        <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js" 
                integrity="sha384-9/reFTGAW83EW2RDu2S0VKaIzap3H66lZH81PoYlFhbGU+6BZp6G7niu735Sk7lN" 
                crossorigin="anonymous"></script>
        <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js" 
                integrity="sha384-B4gt1jrGC7Jh4AgTPSdUtOBvfO8shuf57BaghqFfPlYxofvL8/KUEfYiJOMMV+rV" 
                crossorigin="anonymous"></script>
    </head>
    <body>
        <h1 class="main-heading">My Page</h1>
        <button class="button">Click Me</button>
    </body>
</html>
```

---

## Topic 1.2 — Core HTML Elements

### Block vs Inline Elements

| Category | Behavior | Examples |
|----------|----------|----------|
| **Block** | Takes full width, starts new line | `<div>`, `<h1>`–`<h6>`, `<p>`, `<ul>`, `<ol>`, `<li>`, `<nav>` |
| **Inline** | Only takes content width, sits beside others | `<span>`, `<a>`, `<img>`, `<button>` (inline-block) |

**Key insight:** You CANNOT set `width`/`height` on true inline elements (`<span>`, `<a>`). `<button>` and `<img>` are **inline-block** — they accept dimensions but still sit in a line.

### The `<div>` Element

`<div>` has no inherent meaning or styling — it's a transparent container for grouping. In this project, it's used to:
- Create flex containers
- Group elements so flexbox treats them as one unit
- Apply shared styles to a set of children

**Why nested divs matter in flexbox:**
```html
<div class="card d-flex flex-row">     <!-- Outer: flex container -->
    <div>                               <!-- Inner: groups text as ONE flex item -->
        <h1>Title</h1>
        <p>Description</p>
    </div>
    <img src="..." />                   <!-- Second flex item -->
</div>
```

Without the inner `<div>`, flex would treat `<h1>`, `<p>`, and `<img>` as THREE separate items in a row.

### Lists

```html
<!-- Unordered (bullets) -->
<ul>
    <li>Item 1</li>
    <li>Item 2</li>
</ul>

<!-- Ordered (numbers) -->
<ol style="list-style-type: lower-roman">
    <li>First</li>    <!-- renders as: i. First -->
    <li>Second</li>   <!-- renders as: ii. Second -->
</ol>
```

List style types: `decimal`, `lower-roman`, `upper-roman`, `lower-alpha`, `upper-alpha`.

### Multiple Classes on Buttons (Composition)

```html
<button class="button button-green">Start</button>
```

- `.button` — shared base (width, height, border-radius, text color)
- `.button-green` — color modifier only (background-color)

The LATER class in the CSS file wins when properties conflict (same specificity → source order decides).

### Gotchas

- **Multiple `<h1>`** on one page — bad for SEO/accessibility. Use `<h2>`–`<h6>` for sub-headings.
- **Missing `alt` on `<img>`** — accessibility violation. Screen readers can't describe the image.
- **Block inside inline** — invalid HTML (`<div>` inside `<p>`). Browser auto-closes the `<p>`, creating broken DOM.

---

### Mastery Checkpoint — Answers

**Q1: Difference between block and inline?**  
Block takes full width and starts a new line. Inline only takes content width and sits beside other inline elements. `<div>` = block, `<button>` = inline-block.

**Q2: Why two nested divs in the Developing Layouts card?**  
The outer div is the flex container. The inner div groups `<h1>` and `<p>` into ONE flex item. Without it, flexbox treats each child independently — you'd get three columns (`h1 | p | img`) instead of two (`text-block | img`).

**Q3: If `.button` and `.button-green` both define `background-color`, which wins?**  
`.button-green` wins because it appears LATER in the CSS file. When specificity is equal (both are single class selectors = 10 points), source order breaks the tie. The ORDER in the HTML `class` attribute does NOT matter.

**Hands-On — Identify 3 problems:**

```html
<body>
    <h1>My Gallery</h1>
    <img src="photo.jpg">              <!-- Problem 1: missing alt attribute -->
    <h1>Beautiful Sunset</h1>          <!-- Problem 2: second h1 (should be h2) -->
    <p>A photo I took. <div class="caption">Shot on iPhone</div></p>  <!-- Problem 3: div inside p (invalid) -->
</body>
```

---

## Topic 1.3 — CSS Fundamentals: Selectors & Properties

### Three Ways to Connect CSS

| Method | Used in project? |
|--------|-----------------|
| External stylesheet (`<link>`) | ✅ Primary (every exercise) |
| Internal stylesheet (`<style>`) | ❌ Never |
| Inline styles (`style="..."`) | ⚠️ Rare (only HTML Lists mocktest) |

### Selector Types and Specificity

| Selector | Syntax | Specificity | Usage in project |
|----------|--------|-------------|-----------------|
| Element | `h1 { }` | 1 | Rare (Specificity Practice files) |
| Class | `.heading { }` | 10 | 95% of all styling |
| ID | `#section { }` | 100 | Not used for CSS (only JS targeting) |

**When specificity is equal → source order wins (later in file beats earlier).**

### Core Properties Reference

| Property | Controls | Values from project |
|----------|----------|---------------------|
| `font-family` | Typeface | `"Roboto"`, `"Bree Serif"`, `cursive` |
| `font-size` | Text size | `12px` – `40px` |
| `font-weight` | Thickness | `normal`, `bold`, `500` |
| `font-style` | Slant | `normal`, `italic` |
| `text-decoration` | Lines on text | `none`, `underline`, `overline` |
| `text-align` | Horizontal position | `left`, `center`, `right` |
| `color` | Text color | Named, hex (`#03449e`) |
| `background-color` | Box fill | Named, hex |

### CSS Syntax Rules

- Values are **NOT quoted strings** (unlike most programming languages)
- Exception: font names with spaces (`"Bree Serif"`) and `url("path")`
- Keywords are lowercase: `bold`, `center`, `white`
- Colors use no quotes: `#1a2a3a`, `white`, `green`

### Design Patterns in CSS

1. **Utility classes** — single-purpose (`.h-center { text-align: center; }`)
2. **Component classes** — bundles all card/button styles
3. **Base + modifier** — `.button` (shared) + `.button-green` (override)

### Gotchas

- **Forgetting quotes** on multi-word fonts: `font-family: Bree Serif;` → may fail. Use `"Bree Serif"`.
- **Element selectors are broad**: `p { }` styles EVERY paragraph — hard to override later.
- **Duplicated properties** across classes — refactoring opportunity.
- **CSS comments**: `/* */` only. `//` is invalid in CSS.

---

### Mastery Checkpoint — Answers

**Q1: `p { color: red; }` vs `.description { color: blue; }` on `<p class="description">`?**  
Text renders **blue**. Class selector (specificity 10) beats element selector (specificity 1).

**Q2: Why class selectors instead of element selectors?**  
Classes are reusable (multiple elements share them), explicit (descriptive names), and don't accidentally style unrelated elements. As the project grows, element selectors create unwanted side effects.

**Q3: Difference between `color` and `background-color`?**  
`color` = text ink. `background-color` = box paint. Setting `color: white` on a div turns the TEXT white, not the background.

**Hands-On — Complete Answer:**

```css
.card-component {
    background-color: #1a2a3a;
    color: white;
    font-family: "Roboto";
    font-size: 16px;
    font-weight: bold;
    text-align: center;
    padding: 20px;
    border-radius: 10px;
}
```

---

## Topic 1.4 — The CSS Box Model

### The Four Layers (inside → out)

```
┌──────────────────────────────────────────────────┐
│                   MARGIN                          │  ← transparent, pushes other boxes away
│  ┌────────────────────────────────────────────┐  │
│  │               BORDER                       │  │  ← visible line
│  │  ┌──────────────────────────────────────┐  │  │
│  │  │            PADDING                   │  │  │  ← space inside border
│  │  │  ┌───────────────────────────────┐   │  │  │
│  │  │  │          CONTENT              │   │  │  │  ← text, images
│  │  │  └───────────────────────────────┘   │  │  │
│  │  └──────────────────────────────────────┘  │  │
│  └────────────────────────────────────────────┘  │
└──────────────────────────────────────────────────┘
```

### Total Size Calculation

```
Total width = content + padding-left + padding-right + border-left + border-right + margin-left + margin-right
```

### Margin vs Padding

| | Padding | Margin |
|--|---------|--------|
| Position | Inside border | Outside border |
| Background visible? | Yes | No (transparent) |
| Part of clickable area? | Yes | No |
| Can be negative? | No | Yes |
| Vertical collapse? | No | Yes |

### Padding/Margin Shorthand (Clockwise: Top → Right → Bottom → Left)

```css
padding: 20px;              /* ALL sides */
padding: 20px 10px;         /* top/bottom, left/right */
padding: 20px 10px 5px;     /* top, left/right, bottom */
padding: 20px 10px 5px 0;   /* top, right, bottom, left */
```

### Centering with `margin: auto`

```css
.centered {
    width: 60%;             /* MUST have a fixed width */
    margin: 20px auto;     /* top/bottom: 20px, left/right: auto (centered) */
}
```

**`auto` only works for horizontal centering when the element has a width less than its parent.** Without a width, block elements fill 100% — no remaining space for auto to distribute.

### Border Properties (All Three Required)

```css
border-width: 2px;       /* how thick */
border-style: solid;     /* solid, dashed, dotted, none (DEFAULT IS NONE!) */
border-color: #e0e0e0;   /* what color */

/* Shorthand */
border: 2px solid #e0e0e0;
```

**If `border-style` is missing, no border renders** — this is the most common border bug.

### Border-Radius

```css
border-radius: 0px;      /* sharp corners */
border-radius: 10px;     /* rounded corners */
border-radius: 50%;      /* circle (on square element) */

/* Directional (for partial rounding) */
border-top-left-radius: 25px;
border-top-right-radius: 25px;
/* bottom stays sharp */
```

### Margin Collapse

When two adjacent block elements have vertical margins, they don't add — they **collapse** to the larger value:

```css
.card-1 { margin-bottom: 25px; }
.card-2 { margin-top: 15px; }
/* Actual gap: 25px (not 40px) — larger margin wins */
```

### Gotchas

- **`width` doesn't include padding/border** (standard box model). Bootstrap fixes this with `box-sizing: border-box`.
- **Padding when you need margin** → padding extends the colored background, margin creates empty gap.
- **Directional border-radius** → `border-radius: 25px` rounds ALL corners. Use individual properties for partial rounding.

---

### Mastery Checkpoint — Answers

**Q1: Element with `width: 200px`, `padding: 15px`, `border: 5px solid`, `margin: 10px`. Total horizontal space?**  
200 + 15 + 15 + 5 + 5 + 10 + 10 = **260px**

**Q2: Why does `margin: 20px auto` only center with a fixed width?**  
`auto` distributes remaining space equally on both sides. Without a width, block elements fill 100% of parent — there IS no remaining space to distribute.

**Q3: Adjacent divs with `margin-bottom: 25px` and `margin-top: 15px`. Actual gap?**  
**25px**. Vertical margins collapse — only the larger value survives.

**Hands-On — Updated Tourism Card:**

```css
.tourism-card {
    text-align: center;
    background-color: white;
    padding: 20px;
    border-top-left-radius: 30px;
    border-top-right-radius: 30px;
    border-style: solid;
    border-color: #e0e0e0;
    border-width: 2px;
    border-bottom: none;
}
```

---

## Topic 1.5 — Units of Measurement

### Units Reference

| Unit | Type | Relative to | Project usage |
|------|------|-------------|--------------|
| `px` | Absolute | Nothing (1/96th inch) | Buttons, fonts, padding, margins |
| `vh` | Relative | 1% of viewport height | Full-screen backgrounds |
| `vw` | Relative | 1% of viewport width | Full-width elements, responsive boxes |
| `%` | Relative | Parent element's dimension | Flexible widths (60%, Bootstrap columns) |
| `em` | Relative | Parent's font-size | Not used in project |
| `rem` | Relative | Root font-size | Not used in project |

### Calculation Formula

```
Pixel value = viewport_dimension × (unit_number / 100)

Example (1440px wide, 900px tall viewport):
50vw = 1440 × 0.50 = 720px
75vh = 900 × 0.75 = 675px
33vw = 1440 × 0.33 = 475.2px
```

### Why `100vh` Instead of `100%` for Backgrounds

`100%` requires the parent to have an explicit height. If the parent (`<body>`) has no height set, `100%` of nothing = 0.

`100vh` always means "100% of the browser viewport" regardless of parent — no dependency chain.

### Percentage Nesting

```
Parent: width: 800px
  └── Child: width: 60%  → 480px
       └── Grandchild: width: 50%  → 240px  (50% of 480, not 800!)
```

### Decision Logic in This Project

```
Full-screen background?      → height: 100vh
Fixed-size UI element?       → px
Text size?                   → px
Spacing (padding/margin)?    → px
Flexible-width column?       → % (via Bootstrap grid)
Responsive colored boxes?    → vh/vw
```

### Gotchas

- **`100vw` can cause horizontal scrollbar** — it includes scrollbar width. Block elements already fill parent width naturally.
- **`height: 100%` without parent height** — collapses to 0. Use `100vh` instead.
- **Fixed `px` widths on responsive layouts** — breaks on small screens. Use `max-width` + `width: 100%`.
- **`vh` on mobile** — `100vh` can be taller than visible area due to browser address bar.

---

### Mastery Checkpoint — Answers

**Q1: On 1440×900 viewport: `50vw`, `75vh`, `33vw`?**  
50vw = 720px, 75vh = 675px, 33vw = 475.2px

**Q2: Why `100vh` over `100%`?**  
`100%` needs parent to have explicit height defined. `100vh` references viewport directly — always works without dependencies.

**Q3: Div with `width: 60%` inside `width: 800px` parent, child with `width: 50%`?**  
Div = 480px. Inner child = 240px (50% of 480px).

**Hands-On — Three-Section Landing Page:**

```css
.section-1 {
    height: 30vh;
    background-color: green;
}
.section-2 {
    height: 50vh;
    background-color: blue;
}
.section-3 {
    height: 20vh;
    background-color: red;
}
```

Total = 100vh (fills entire viewport, no scroll).

---

## Topic 1.6 — CSS Backgrounds

### Two Types of Backgrounds

1. **Solid color** — `background-color: #333;` (no network request)
2. **Image** — `background-image: url("...");` (requires sizing instructions)

### Layer Stack (bottom → top)

```
Content (text, buttons)     ← topmost
background-image            ← middle
background-color            ← bottom (fallback if image fails)
```

### The Full-Screen Hero Pattern (Most Repeated Pattern)

```css
.bg-container {
    background-image: url("https://example.com/hero.jpg");
    height: 100vh;
    background-size: cover;
    background-position: center;
    background-repeat: no-repeat;
    background-color: #333;    /* fallback */
    color: white;
    text-align: center;
}
```

### `background-size` Explained

| Value | Fills element? | Shows full image? | Repeats? | Empty space? |
|-------|---------------|-------------------|----------|-------------|
| `cover` | ✅ Always | ❌ May crop | Never | Never |
| `contain` | ❌ May have gaps | ✅ Always | Never | Yes |
| (not set) | No | At natural size | YES (tiles) | Depends |

**`cover`** — scales UP to fill completely. Crops overflow. NEVER repeats.  
**`contain`** — scales to fit INSIDE. Shows everything. May have letterbox gaps.  
**Default (no size)** — image at natural dimensions, tiles/repeats to fill.

### `background-position`

Controls which part of the image is anchored when `cover` crops:

| Value | Keeps | Crops from |
|-------|-------|-----------|
| `center` | Center of image | All edges equally |
| `top` | Top edge | Bottom |
| `bottom` | Bottom edge | Top |
| (default `0% 0%`) | Top-left corner | Right and bottom |

### `url()` Syntax

```css
/* All valid */
background-image: url(https://example.com/img.jpg);       /* no quotes */
background-image: url("https://example.com/img.jpg");     /* double quotes */
background-image: url('https://example.com/img.jpg');     /* single quotes */

/* Local file (relative to CSS file) */
background-image: url("chatbot.png");
```

Best practice: always use quotes.

### Gotchas

- **No height + background-image** → element collapses to 0px, background invisible.
- **Missing `background-size: cover`** → image displays at natural size, may tile or show only a corner.
- **White text on light image** → unreadable. Use dark images or overlay text on a colored card.
- **`background-image` vs `<img>`** → Use `background-image` for decoration, `<img>` for content that carries meaning (accessibility).

---

### Mastery Checkpoint — Answers

**Q1: Difference between `cover` and `contain`?**  
`cover` fills the element completely, may crop edges of the image. `contain` shows the entire image, may leave empty space filled by `background-color`. Neither ever repeats.

**Q2: Image fails to load, element has both `background-color: #333` and `background-image`?**  
User sees the `#333` dark gray background (the fallback color shows through). If neither was set, they'd see the default white/transparent background.

**Q3: Why does Navbar & Banner use `background-position: center` while Tourism doesn't?**  
The Banner has a centered design composition (focal point in the middle). With `center`, cropping happens equally from all edges, keeping the subject visible. The Tourism page uses a generic ocean photo where the default (top-left anchor) works fine.

**Hands-On — Music App Section:**

```css
.music-app {
    background-image: url('https://example.com/night-sky.png');
    height: 60vh;
    background-size: cover;
    background-position: center;
    background-color: #0a1628;
    color: white;
    text-align: center;
    font-family: "Bree Serif";
    font-size: 28px;
}
```

---

## Topic 1.7 — Google Fonts Integration

### How Web Fonts Work

```
1. Browser parses CSS → finds @import url("fonts.googleapis.com/...")
2. Requests font CSS from Google
3. Google returns @font-face rules with .woff2 file URLs
4. Browser downloads font files
5. Font becomes available for font-family declarations
6. Text re-renders with the loaded font
```

### The Standard Import Line (Used in Every CSS File)

```css
@import url("https://fonts.googleapis.com/css2?family=Bree+Serif&family=Caveat:wght@400;700&family=Lobster&family=Monoton&family=Open+Sans:ital,wght@0,400;0,700;1,400;1,700&family=Playfair+Display+SC:ital,wght@0,400;0,700;1,700&family=Playfair+Display:ital,wght@0,400;0,700;1,700&family=Roboto:ital,wght@0,400;0,700;1,400;1,700&family=Source+Sans+Pro:ital,wght@0,400;0,700;1,700&family=Work+Sans:ital,wght@0,400;0,700;1,700&display=swap");
```

### Fonts Available After Import

| Font | Usage in project |
|------|-----------------|
| **Roboto** | Primary body font (headings, paragraphs, buttons) |
| **Bree Serif** | Decorative headings (Music Page, Shopping) |
| **Caveat** | Handwritten feel (Diwali page) |
| **Lobster** | Decorative display |
| **Playfair Display** | Elegant serif headings |
| **Open Sans** | Alternative body text |
| **Source Sans Pro** | Clean sans-serif |
| **Work Sans** | Modern geometric |

### Weight/Style Decoding

```
family=Roboto:ital,wght@0,400;0,700;1,400;1,700

Decoded:
ital=0, wght=400 → Roboto Regular
ital=0, wght=700 → Roboto Bold
ital=1, wght=400 → Roboto Italic
ital=1, wght=700 → Roboto Bold Italic
```

### `display=swap` Parameter

Tells browser: show fallback font immediately, swap in web font when loaded (FOUT). Without it, text may be invisible until font arrives (FOIT).

### Two Ways to Load Fonts

| Method | Where | Performance |
|--------|-------|-------------|
| `@import` in CSS | CSS file line 1 | Slower (delays CSS parsing) |
| `<link>` in HTML | `<head>` section | Faster (earlier discovery) |

This project uses `@import` exclusively (simpler for learning, self-contained in CSS).

### Proper Font Stack (Fallback Chain)

```css
/* Project's approach (no fallback) */
font-family: "Roboto";

/* Better (with fallback chain) */
font-family: "Roboto", Arial, sans-serif;
```

If primary font fails → use similar system font → use any font in that category.

### Gotchas

- **`@import` MUST be line 1** of CSS (before any rules). Otherwise ignored.
- **Inconsistent casing** — `"Bree serif"` vs `"Bree Serif"`. Match Google's exact casing.
- **Loading unused fonts** — this project loads 10 families but uses 1–2 per exercise. Wastes bandwidth.
- **No fallback stack** — if Google is down, text renders in browser default serif (looks completely different).
- **Using `font-weight: bold` without loading weight 700** — browser fakes boldness (blurry).

---

### Mastery Checkpoint — Answers

**Q1: Google Fonts CDN unreachable, `font-family: "Roboto"` with no fallback?**  
Browser falls back to its default font (typically Times New Roman — a serif). The page still works functionally but looks completely different from the intended design.

**Q2: Why `display=swap`?**  
Shows fallback font immediately while web font downloads (FOUT). Without it, text might be invisible until the font loads (FOIT) — worse user experience.

**Q3: Loading 10 fonts but using only 1–2. Practical cost?**  
1. Wasted bandwidth (~50-100KB per unused font family)
2. Slower page render (more data to download before `@import` completes)

**Hands-On — Load Only What You Need:**

```css
@import url("https://fonts.googleapis.com/css2?family=Playfair+Display:wght@700&family=Open+Sans&display=swap");

.heading {
    font-family: "Playfair Display", Georgia, serif;
    font-weight: bold;
    font-size: 36px;
}

.body-text {
    font-family: "Open Sans", Arial, sans-serif;
    font-weight: normal;
    font-size: 16px;
}
```

Key points:
- Only load the fonts you need (`:wght@700` for bold Playfair only)
- Always include fallback stacks (similar system font → generic category)
- `display=swap` for better perceived performance

---

## Module 1 Summary — Key Takeaways

1. **HTML = structure.** DOCTYPE → html → head (metadata) → body (content).
2. **CSS = presentation.** Selectors target elements; properties apply visual changes.
3. **Box Model = every element's anatomy.** Content + padding + border + margin.
4. **Units matter.** `px` for precision, `vh`/`vw` for viewport-relative, `%` for parent-relative.
5. **Backgrounds = visual depth.** `cover` fills completely, `contain` shows entirely.
6. **Fonts load from the network.** `@import` → download → render. Always include fallbacks.
7. **Specificity resolves conflicts.** Class (10) > element (1). Equal specificity → source order wins.
