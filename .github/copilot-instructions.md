<!-- Copilot Instructions for repository: "Site vitrine 2026" -->
# Copilot instructions

Below are concise, actionable guidelines for AI coding agents working in this repository.

## Big picture
- This is a static HTML/CSS/JS template (Colorlib-derived) with optional PHP form handling. Primary pages live at the repository root (e.g. `index.html`, `about.html`, `pricing.html`).
- Client assets are organized as: `css/` (production CSS), `scss/` (source SCSS partials), `js/` (site JS), `js/vendor` (third-party libs), `img/` (images & galleries), `fonts/`.
- `js/main.js` is the main behavior entrypoint: modify it for cross-page scripting and plugin initialization.
- Forms use `contact.html` + `contact_process.php` — testing form submission requires a PHP-capable server (see Developer workflows below).

## Key files to inspect when changing behavior
- `index.html` — demonstrates structure, CSS includes, and how navigation/menu are wired.
- `js/main.js` — primary JS file: Owl carousel, SlickNav, MagnificPopup, Isotope, WOW, scroll helpers, and counters.
- `scss/style.scss` and the `_*.scss` partials — SCSS source; partials begin with `_` and are compiled into `css/style.css`.
- `css/style.css` — shipped CSS (generated); prefer editing SCSS and regenerating CSS.
- `contact_process.php` — server-side form processor; changes here must be tested under PHP.

## Project-specific conventions & patterns
- SCSS partials: files in `scss/` named `_*.scss` are imported into `style.scss`. Keep variables in `_varriable.scss` and layout in named partials (e.g. `_header.scss`, `_footer.scss`).
- Vendor JS is included directly; do not change vendor files unless updating a library. Reference `js/vendor/jquery-1.12.4.min.js` for compatibility with existing plugins.
- Responsive/mobile menu uses SlickNav wired in `js/main.js` via `ul#navigation` and a `.mobile_menu` container.
- Image assets referenced by HTML are relative (e.g. `img/gallery/1.png`); maintain paths when moving assets.

## Developer workflows (as-discerned)
- Preview static pages: open `index.html` in a browser or use a simple file server.
- Compile SCSS (no build system provided): recommended command (install Dart Sass):
```
sass scss/style.scss:css/style.css --no-source-map
```
- Test PHP form handling (required for `contact_process.php`): run a PHP server from repository root:
```
php -S localhost:8000
```
Then open `http://localhost:8000/contact.html` to test submissions.

## Editing guidance for AI agents
- When changing interactive behavior, update `js/main.js` (single spot for plugin init). Example: to adjust slider timing, edit the `$('.slider_active').owlCarousel({...})` block.
- When changing styles, edit `scss/` partials and regenerate `css/style.css`; do not edit generated CSS directly unless making a quick hotfix — note in the commit message if so.
- Keep plugin initialization and selectors consistent with markup in `index.html` and other pages (e.g., `#navigation`, `.popup-image`, `.grid`, `.portfolio-menu`).
- Preserve compatibility with jQuery 1.x patterns used across the codebase (no modern ES module assumptions).

## Integrations & external dependencies
- Third-party front-end libraries used: jQuery (vendor), Owl Carousel, Magnific Popup, Isotope, SlickNav, WOW, CounterUp, Gijgo. Updates may require testing across browsers due to old jQuery.
- No package.json / npm build configured; dependency updates are manual (replace files in `js/vendor/` and adjust includes in HTML).

## Safety / licensing notes
- This is a Colorlib template; `readme.txt` contains license notes. Do not remove or alter copyright attribution without confirming license.

## Quick checklist for PRs
- Confirm SCSS → CSS steps if styles changed (include the generated `css/style.css` in PR or document the compile step).
- If JS behavior changes, test homepage and at least one other page that uses the same components (e.g., `gallery.html`).
- If modifying `contact_process.php`, verify form submission via a local PHP server.

If any of the above sections are unclear or you'd like me to include more examples (CSS variable locations, common selectors, or sample commands), tell me which area to expand.
