# Blog

Personal blog built with [Zola](https://www.getzola.org/), a Rust-based static site generator.

## Prerequisites

- Zola **0.22.1** (matches the version used in CI — don't use a different version)
- Git (the theme is a submodule, so clone with `--recurse-submodules`, or run `git submodule update --init` afterward)

## Serve locally

```bash
zola serve
```

Starts a local dev server with live reload (default: `http://127.0.0.1:1111`).

## Build

```bash
zola build
```

Outputs the static site to `public/`.

## Check for issues

```bash
zola check
```

Checks for broken links and other content problems.

## Writing a new post

Create a Markdown file in `content/` with TOML frontmatter:

```toml
+++
title = "Post Title"
date = 2026-06-13
+++
```

Posts live at the root of `content/` (not in a subdirectory) to avoid double `/blog/blog/` URLs.

## Images in posts

The site is served from the `/blog` subpath on GitHub Pages. Raw `<img>` tags in markdown must use the `/blog/` prefix:

```html
<img src="/blog/my-image.png" alt="..." />
```

See `CLAUDE.md` for more details on the theme, structure, and customization.
