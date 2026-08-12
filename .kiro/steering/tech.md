# Tech Stack

## Languages
- HTML5
- CSS3
- Minimal inline JavaScript (onclick handlers for page navigation)

## Frameworks and Libraries
- **Bootstrap 4.5.2** — loaded via CDN (StackPath)
- **jQuery 3.5.1 Slim** — required by Bootstrap JS
- **Popper.js 1.16.1** — required by Bootstrap JS
- **Google Fonts** — imported via `@import url(...)` in CSS files
- **CCBP UI Kit** — `ccbp-ui-kit.js` script from `d2clawv67efefq.cloudfront.net` (provides `display()` helper for section toggling)

## Build System
None. Files are plain HTML/CSS opened directly in a browser. No bundler, preprocessor, or package manager is used.

## Common Commands
There are no build, test, or compile commands. To view any exercise:
1. Open the `index.html` file in a web browser.
2. Use a local dev server (e.g., VS Code Live Server extension) for a better experience.

## CDN References (standard across exercises)
```html
<!-- Bootstrap CSS -->
<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" integrity="sha384-JcKb8q3iqJ61gNV9KGb8thSsNjpSL0n8PARn9HuZOnIxN0hoP+VmmDGMN5t9UJ0Z" crossorigin="anonymous" />

<!-- jQuery, Popper, Bootstrap JS -->
<script src="https://code.jquery.com/jquery-3.5.1.slim.min.js" integrity="sha384-DfXdz2htPH0lsSSs5nCTpuj/zy4C+OGpamoFVy38MVBnE+IbbVYUew+OrCXaRkfj" crossorigin="anonymous"></script>
<script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.1/dist/umd/popper.min.js" integrity="sha384-9/reFTGAW83EW2RDu2S0VKaIzap3H66lZH81PoYlFhbGU+6BZp6G7niu735Sk7lN" crossorigin="anonymous"></script>
<script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.min.js" integrity="sha384-B4gt1jrGC7Jh4AgTPSdUtOBvfO8shuf57BaghqFfPlYxofvL8/KUEfYiJOMMV+rV" crossorigin="anonymous"></script>
```
