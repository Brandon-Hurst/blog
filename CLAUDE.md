# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## What This Is

A personal blog built with [Zola](https://www.getzola.org/), a Rust-based static site generator. The live site is at `https://tethered-embedded.io`. Topics: embedded systems, electronics, music, and general musings.

## Commands

```bash
# Serve locally with live reload
zola serve

# Build for production
zola build

# Check for broken links and other issues
zola check
```

## Structure

- `zola.toml` — site config (base URL, theme, Sass compilation, feed generation, extra theme options)
- `content/` — blog posts as Markdown files with TOML frontmatter (`+++` delimited); posts live at the root (not in a subdirectory) to avoid double `/blog/blog/` URLs with the GH Pages subpath
- `static/` — static assets (images, etc.) served at the root
- `templates/` — Tera template overrides (currently empty; theme templates are used directly)
- `sass/` — SCSS overrides (currently empty; theme styles are used directly)
- `themes/terminus/` — the Terminus theme, tracked as a git submodule

## Writing a New Post

Create a Markdown file in `content/`. Frontmatter is TOML between `+++` delimiters:

```toml
+++
title = "Post Title"
date = 2026-06-13
+++
```

Posts are sorted by `date` (set in `content/_index.md`). The filename prefix (e.g. `2-next-post.md`) controls ordering when dates are equal but is otherwise cosmetic.

## Images in Posts

The site is served from the `/blog` subpath on GitHub Pages (`brandon-hurst.github.io/blog`). Raw HTML `<img>` tags in markdown must use the `/blog/` prefix to resolve correctly:

```html
<img src="/blog/my-image.png" alt="..." />
```

Note: `get_url()` is a Tera template function and cannot be used directly in markdown content files — only in templates and shortcodes.

## Theme Customization

The `terminus` theme is configured via `[extra]` in `zola.toml`. Most theme options (color scheme, copyright, layout, etc.) can be set there without overriding templates. The active color scheme is `noir-gold`. To override theme templates or styles, add files to `templates/` or `sass/` — Zola merges these with the theme, with the project-level files taking precedence.

The theme is a git submodule at `themes/terminus/`, forked at `https://github.com/Brandon-Hurst/terminus` and tracking the `bh-custom` branch. Custom changes (e.g. the noir-gold color scheme) live on that branch. To update the theme or add customizations, commit to `bh-custom` in the submodule and push to the fork, then update the submodule pointer in this repo.

## Environment

- Local Zola version: **0.22.1** — the GitHub Actions workflow installs this same version. Don't assume an older version.
