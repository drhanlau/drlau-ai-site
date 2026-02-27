# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Personal portfolio website for Dr. Lau Cher Han — built with Jekyll 4.3+ and deployed to GitHub Pages. Content is authored in Markdown/HTML with Liquid templating.

## Commands

```bash
# Install dependencies
bundle install

# Local development server (with live reload)
bundle exec jekyll serve

# Production build (matches CI)
bundle exec jekyll build --future

# Clean generated files
bundle exec jekyll clean
```

There are no test or lint commands configured.

## Deployment

Push to `main` triggers GitHub Actions (`.github/workflows/jekyll.yml`) which builds with Ruby 3.3 and deploys to GitHub Pages. The `--future` flag is used in both local serve and CI builds.

## Architecture

**Template hierarchy:** `_layouts/default.html` is the base layout (includes header, nav, footer). `_layouts/post.html` extends default for blog posts.

**Includes:** `_includes/header.html` (meta, fonts, CSS), `_includes/nav.html` (fixed navbar), `_includes/footer.html` (footer + IntersectionObserver scroll animations).

**Pages:** Root-level `.md`/`.html` files become top-level pages (about, media, speaking, contact, blog, astro, chinapress articles). `index.html` is the home page with hero section.

**Blog posts:** `_posts/` directory, permalink pattern `/blog/:title/`, default layout `post`.

**Styling:** Single custom CSS file at `assets/css/style.css` — no CSS framework. Uses CSS custom properties for theming, glassmorphism effects, and staggered fade-in animations (`.reveal` class + IntersectionObserver).

**Plugins:** `jekyll-feed` (RSS at /feed.xml), `jekyll-seo-tag` (Open Graph/Twitter/schema.org metadata).

## Content Conventions

- Blog posts use filename format `YYYY-MM-DD-title.md` with YAML front matter (layout, title, date)
- Pages use front matter with `layout: default` and `title`
- Images go in `assets/images/`
- Use `{{ site.baseurl }}` prefix for internal links and asset paths
