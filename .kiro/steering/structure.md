# Project Structure

## Top-Level Layout

```
Introduction to HTML and CSS/
├── HTML and CSS/            # Fundamentals: elements, fonts, colors, box model
├── Bootstrap/               # Bootstrap utilities, buttons, backgrounds
├── Developing Layouts/      # Flexbox, carousels, embedded video, cards
├── Responsive Web Design/   # Grid system, media queries, navbars, specificity
├── Website Integration/     # Multi-page SPA-style site with section toggling
├── Coding Mocktests/        # Timed practice tests (Test 1, Test 2)
└── .kiro/                   # Kiro configuration and steering
```

## Folder Conventions

- Each **topic folder** (Bootstrap, Developing Layouts, etc.) contains a root `index.html` + `style.css` demonstrating the core concept.
- **Practice-N/** and **Coding Practice N/** subfolders are individual exercises, each self-contained with their own `index.html` and `style.css`.
- **Assignment-N/** subfolders are graded coding assignments.
- **Coding Mocktests/** groups exercises by test number, with each question in its own descriptively-named folder.

## File Conventions

| File | Purpose |
|------|---------|
| `index.html` | Entry point for every exercise |
| `style.css` | Custom styles (always linked from HTML) |
| `*.png` / `*.jpg` | Local image assets when not using CDN URLs |
| `README.txt` | Occasional exercise description |

## Naming Patterns

- Folder names use title case with spaces (e.g., "Developing Layouts", "Coding Practice 3")
- CSS class names use kebab-case (e.g., `bg-container`, `favourite-place-card-heading`)
- Section IDs use camelCase (e.g., `sectionHomePage`, `sectionFavouritePlaces`)
- Images are hosted on the CCBP CDN (`d2clawv67efefq.cloudfront.net`) or included locally
