## Purpose

These instructions help an AI coding agent become immediately productive in this repository: a small, static translation-site prototype consisting of a single HTML entrypoint and a CSS stylesheet.

**Quick summary:** - Single-page static site. Main files: [index.html](index.html) and [styles.css](styles.css).

## What this repo is (big picture)

- **Type:** Static marketing site (no backend, no build system, no package manager files present).
- **Entry point:** [index.html](index.html) — contains the full markup, navigation anchors, a placeholder contact form, and a tiny inline script that sets the current year.
- **Presentation:** [styles.css](styles.css) — full visual system (variables in :root, layout utilities, hero, header, responsive grid). Many visuals are pure CSS (logo via ::before/::after, blurred flag backgrounds).

## Architecture and design decisions (what to know)

- The project intentionally avoids JavaScript frameworks. UI behavior is minimal and is implemented inline in `index.html` (example: `document.getElementById('year').textContent = new Date().getFullYear();`). Prefer minimal, non-framework edits.
- Visuals and brand are implemented in CSS only (see the `logo-icon` rules and hero pseudo-elements in [styles.css](styles.css)). When changing visuals, adjust CSS variables in `:root` and related classes.
- The contact form in `index.html` is a placeholder with `onsubmit="return false;"` and a button that triggers `alert(...)`. There is no backend; do not attempt to wire a server unless adding new infrastructure and documenting it.

## Developer workflows (how to test locally)

- No build or test commands are present. To preview locally, open `index.html` in a browser or run a simple HTTP server from the repository root, for example:

```bash
python3 -m http.server 8000
# then open http://localhost:8000 in a browser
```

- Because many CSS backgrounds reference image filenames (e.g., `flag-iceland.png`), verify those assets exist when changing hero/flag styles. Missing images will silently not render (CSS still works).

## Project-specific conventions & patterns

- Single-file content approach: copy/paste edits to `index.html` are expected for content updates (text, sections, anchors). Keep markup semantic: the site already uses `<section id="...">` anchors for navigation.
- CSS-first components: styling uses utility-like classes (`container`, `grid-3`, `badge`, `btn`) rather than component frameworks. When adding elements reuse these existing utility classes to stay consistent.
- Accessibility notes already applied: use `role` and `aria-label` in a few places (e.g., hero card). When adding interactive elements, follow this lightweight pattern (explicit `aria-label` + semantic tags).

## Integration points & external dependencies

- External font loaded from Google Fonts in `index.html` (`Inter` family). No other external JS/CSS libraries.
- No CI, no package.json, no Dockerfile — repo is self-contained. If adding build tooling, update this file to document the new workflow.

## Editing guidelines for AI agents

- Make minimal, focused changes in `index.html` and `styles.css`. For content edits, change `index.html` only. For look-and-feel, prefer adjusting `:root` variables and existing class rules in `styles.css`.
- Preserve the placeholder contact form behavior unless asked to implement a real backend — callouts in the markup make this explicit.
- When introducing new assets (images/icons), add them to the repo and update the CSS background URLs. Search for similar usages in `styles.css` to match sizing/blur patterns.

## Examples (explicit patterns to reuse)

- Logo: CSS-only icon implemented via `.logo-icon::before` and `.logo-icon::after` in [styles.css](styles.css). Edit these rules to change the icon.
- Year injection: inline script near bottom of [index.html](index.html) — keep or replace with a build-time replacement if adding a build step.
- Contact CTA: `.nav-cta` is used for the primary header action; reuse this class for primary CTAs.

## When to ask the maintainer

- If you need a backend (contact form, file uploads, payments), ask before scaffolding — this repo currently has no server or API conventions.
- If you add build tooling (npm, bundler, task runner), update this file with the required commands and a brief migration note so future agents know the new flow.

---

If any part above is unclear or you'd like the agent to expand instructions for a specific change (e.g., add a contact-backend sketch, convert to a static site generator), tell me which area to expand.
