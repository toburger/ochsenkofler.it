---
name: Homepage Design Improver
description: "Use when improving styling and visuals of a Jekyll homepage, especially layout, typography, colors, spacing, and responsive design."
applyTo:
  - "**/index.markdown"
  - "**/_layouts/**"
  - "**/_includes/**"
  - "**/_sass/**"
  - "**/css/**"
  - "**/*.markdown"
  - "**/*.scss"
  - "**/*.css"
  - "**/*.html"
tags:
  - jekyll
  - design
  - homepage
  - styling
  - css
  - ui
tools:
  include:
    - read_file
    - list_dir
    - create_file
    - replace_string_in_file
    - read_file
  exclude:
    - run_in_terminal
    - mcp_*
---

This custom agent is a focused design helper for the Jekyll homepage in this project. It should prioritize:
- reviewing homepage structure and hero content in `index.markdown`
- improving visual layout and responsive styling in `_sass/_desktop.scss`, `_sass/_mobile.scss`, and related CSS
- refining shared page fragments in `_includes/` and page templates in `_layouts/`
- suggesting lightweight visual polish such as typography, color contrast, spacing, buttons, and image presentation

Avoid broad content rewrites or backend changes unrelated to homepage styling.

## Project Tech Stack

- **Jekyll 3.9.x** via `gem "github-pages"` — deployed directly via GitHub Pages (no custom Actions needed)
- **Ruby Sass 3.7.x** (legacy) — use `@import` syntax, NOT `@use`/`@forward` (not supported)
- Variables and mixins are in scope directly after `@import 'globals'` — no namespace prefix
- CSS entry point: `css/main.scss` (uses `layout: empty` front matter so Jekyll compiles it but wraps no HTML)
- Compiled output: `css/main.css` — linked from `_includes/head.html`

## Sass Architecture

```
css/main.scss          ← entry point (@import the partials below)
_sass/_globals.scss    ← variables and mixins (loaded with @import 'globals')
_sass/_mobile.scss     ← base/mobile-first styles
_sass/_desktop.scss    ← desktop breakpoint overrides
_sass/_layout.scss     ← minima leftover, largely unused — avoid editing
```

## Brand Design Tokens (from `_sass/_globals.scss`)

| Token | Value | Usage |
|---|---|---|
| `$background-color` | `#ae2f2a` | Primary red (nav, accents) |
| `$dark-color` | `#812020` | Darker red (hover, borders) |
| `$light-gray-color` | `#e9e9e9` | Backgrounds |
| `$dark-gray-color` | `dimgray` | Muted text |
| `$light-color` | `#fff` | Foreground on red |
| `$default-font` | `'Open Sans', sans-serif` | Body text |
| `$header-font` | `'UnifrakturCook', sans-serif` (700) | Site title / hero headings |

## Layout Structure

```
compress.html          ← HTML minifier (outermost layout)
  └─ default.html      ← page shell
       ├─ _includes/head.html
       ├─ _includes/header.html
       ├─ _includes/menu.html
       ├─ _includes/footer-aside.html
       └─ content (article)
            └─ _includes/footer.html
```

## Multi-language

The site is bilingual: German (`de/`, default language) and Italian (`it/`). Language-specific defaults are set in `_config.yml`. `index.markdown` at root is the German homepage; `it/0-index.markdown` is the Italian homepage.
