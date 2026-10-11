# Repository Guidelines

## Project Structure & Module Organization

This repository hosts a small, dependency-free personal website. `index.html` is the application entry point and contains all page markup and CSS. Static media belongs under `assets/`; profile and favicon images currently live in `assets/images/`. `README.md` provides the repository summary. Keep new assets organized by type, and use root-relative paths such as `/assets/images/avatar.jpeg` when they must work from any page on the GitHub Pages site.

## Build, Test, and Development Commands

No compilation or package installation is required. To preview the site locally, run:

```sh
python3 -m http.server 8000
```

Then visit `http://localhost:8000`. Use `git diff --check` before committing to catch trailing whitespace and malformed conflict markers. Run `git status --short` to verify that only intended files are included in the change.

## Coding Style & Naming Conventions

Follow the existing four-space indentation in HTML and CSS. Use semantic HTML where practical, lowercase kebab-case CSS classes (for example, `.main-content` and `.social-link`), and descriptive lowercase asset filenames. Reuse the CSS custom properties in `:root` instead of duplicating colors, and keep dark-mode overrides in the existing `prefers-color-scheme` block. External links that open a new tab must retain `target="_blank"` and `rel="noopener"`. Avoid adding frameworks or build dependencies for changes that can remain plain HTML and CSS.

## Testing Guidelines

There is currently no automated test framework or coverage requirement. Manually verify changes in a browser at desktop and narrow mobile widths. Check both light and dark system themes, confirm all external links, and ensure the avatar and favicon load without console or network errors. For layout changes, compare hover, focus, wrapping, and responsive behavior around the existing 768 px breakpoint.

## Commit & Pull Request Guidelines

Recent commits use short, imperative summaries such as `Fix X button class and remove dead CSS` and `Add Google Scholar link to social links section`. Keep each commit focused and explain the user-visible result. Pull requests should include a concise description, testing notes, and linked issue when applicable. Attach before-and-after screenshots for visual changes, ideally showing desktop and mobile views plus dark mode when styling is affected.
