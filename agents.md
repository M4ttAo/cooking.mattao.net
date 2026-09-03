# CookingTao Agent Instructions

## Project

This repository contains the static recipe website published at `https://cooking.mattao.net`.
It is separate from the CV and automation blog repositories.

The site is built with Jekyll and deployed by Cloudflare from the `deploy` branch.
GitHub Actions does not build or deploy the site. Its only responsibility is synchronizing `main`
to `deploy`.

## Repository Structure

- `_recipes/`: one Markdown file per recipe.
- `_data/categories.yml`: ordered categories shown on the homepage.
- `_data/tags.yml`: tag-to-color mappings.
- `_data/profile.yml`: site name and introductory text.
- `_includes/recipe-card.html`: reusable recipe card.
- `_layouts/recipe.html`: layout for individual recipes.
- `recipes/index.md`: complete recipe archive.
- `index.md`: homepage with latest recipes, category board, top recipes and introduction.
- `_sass/_recipes.scss`: recipe-specific design and responsive layout.
- `assets/images/recipes/`: local recipe images.
- `.github/workflows/deploy.yml`: synchronizes `main` to `deploy`.
- `_config.yml`: Jekyll configuration and `recipes` collection definition.

## Recipe Format

Create recipes inside `_recipes/` using a descriptive lowercase slug. The front matter should contain:

```yaml
---
layout: recipe
title: "Recipe title"
permalink: /recipes/recipe-slug/
icon: "🍝"
cover: /assets/images/recipes/recipe-slug/cover.jpg
image: /assets/images/recipes/recipe-slug/cover.jpg
categories: ["Primi"]
tags: ["Primi"]
top: true
---
```

Use `top: true` only for recipes that belong in the homepage's `Ricette Top` section.
Recipes may belong to multiple categories. Every category used in a recipe should exist in
`_data/categories.yml` if it must appear on the homepage board.

Keep recipe content in Italian unless explicitly requested otherwise. Preserve the order and meaning
of existing content: ingredients, procedure, storage instructions and internal images.

## Images

Store all recipe images locally under `assets/images/recipes/<slug>/`.
Use `cover.jpg` for the card and page hero when available. Use descriptive filenames for additional
images and reference them with absolute site paths such as:

```markdown
![Descrizione](/assets/images/recipes/recipe-slug/step.jpg)
```

Do not leave references to Super, `images.spr.so` or remote Unsplash URLs in recipe Markdown.
Check image licensing and availability before importing external images.

## Homepage

The homepage is data-driven. Do not manually duplicate recipe cards in `index.md`.
Adding a recipe to `_recipes/` automatically makes it available to the latest, category and archive
sections. Category order is controlled only by `_data/categories.yml`.

The category board is horizontally scrollable between categories and vertically scrollable inside
each category column. Preserve this behavior on desktop and mobile.

## Design

The visual language is a modern recipe archive inspired by CookingTao:

- warm cream background
- terracotta accent
- soft cards with rounded corners
- `DM Sans` for headings
- `Nunito Sans` for body text
- `IBM Plex Mono` for small metadata and labels
- light/dark theme toggle using the existing theme script

Keep the palette in `_sass/_variables.scss` and reuse CSS variables instead of hardcoding new colors.
Keep the theme toggle accessible and do not replace it with text-only controls.

## Cloudflare and Git

The deployment flow is:

```text
push main
  -> GitHub Actions synchronizes deploy
  -> Cloudflare builds with `bundle exec jekyll build`
  -> Cloudflare publishes `_site`
```

The GitHub workflow must not run Jekyll, Node, Wrangler or a Cloudflare deployment command.
Cloudflare build settings are:

```text
Build command: bundle exec jekyll build
Output directory: _site
Production branch: deploy
```

Do not add PDF generation, Puppeteer, Wrangler configuration or CV-specific files to this repository.
Do not commit `_site/`, `.jekyll-cache/`, `Gemfile.lock` or `node_modules/`.

## Validation

Before finishing changes:

1. Run `git diff --check`.
2. Confirm every local image referenced by a recipe exists.
3. Confirm recipe permalinks are unique.
4. Confirm new categories and tag colors are defined when needed.
5. Run `bundle exec jekyll build` when Ruby and Bundler are available.
6. Do not commit or push unless explicitly requested.
