# Studio Pulse

Marketing site for a full-service communication agency — brand strategy, creative direction, digital, content, and more.

Built with [Astro](https://astro.build) and [Bulma](https://bulma.io), statically generated and dependency-light.

## Features

- **Multi-page site** — Home, About, Blog, Contact.
- **Dark / light mode** — toggle in the navbar; preference persisted in `localStorage` and honors the OS `prefers-color-scheme` on first visit.
- **SPA page transitions** — `<ClientRouter />` provides client-side navigation with a soft fade.
- **Blog with content collections** — posts written in Markdown with typed frontmatter (`src/content/blog/`).
- **Accessibility** — skip link, semantic landmarks and headings, `aria-current` on the active nav item, visible `:focus-visible` outlines, `prefers-reduced-motion` support, form labels + required/autocomplete attributes.

## Tech Stack

| Layer | Choice |
|-------|--------|
| Framework | Astro 7 (static/SSG) |
| CSS | Bulma 1.0.4 + custom global stylesheet |
| Content | Astro Content Collections (`astro/loaders` `glob`) |
| Package manager | pnpm |

## Project Structure

```text
/
├── public/                 # favicon + static assets
├── src/
│   ├── components/
│   │   └── Card.astro      # shared card component
│   ├── content/
│   │   └── blog/           # Markdown blog posts (content collection)
│   ├── content.config.ts   # content collection schema + loader
│   ├── layouts/
│   │   └── Layout.astro    # global layout: head, navbar, footer, theme toggle
│   ├── pages/
│   │   ├── index.astro     # Home
│   │   ├── about.astro     # About
│   │   ├── blog/
│   │   │   ├── index.astro # Blog listing
│   │   │   └── [...slug].astro  # Individual blog post
│   │   └── contact.astro   # Contact
│   └── styles/
│       └── global.css      # design tokens (light/dark) + component overrides
└── package.json
```

## Getting Started

Prerequisites: **Node.js ≥ 22.12** (see `package.json` `engines`).

```sh
pnpm install
pnpm dev
```

Open `http://localhost:4321`.

## Commands

| Command           | Action                                        |
| :---------------- | :-------------------------------------------- |
| `pnpm install`    | Install dependencies                          |
| `pnpm dev`        | Start local dev server at `localhost:4321`    |
| `pnpm build`      | Build production site to `./dist/`            |
| `pnpm preview`    | Preview the production build locally          |
| `pnpm astro check`| Run Astro type checking                       |

## Adding a Blog Post

1. Create a new Markdown file in `src/content/blog/`, e.g. `07-my-post.md`.
2. Add frontmatter matching the collection schema in `src/content.config.ts`:

   ```md
   ---
   title: "My Post Title"
   date: 2025-11-01
   description: "Short summary shown on the blog listing page."
   author: "Team Member"
   tags: [strategy, branding]
   ---

   Your post body in Markdown here.
   ```

3. The post is automatically available at `/blog/my-post/`.

> `date` field supports ISO date strings. `tags` is optional.

## Theming

All colors, surfaces, and borders are CSS custom properties defined in `src/styles/global.css`:

- `:root` — light theme (default)
- `[data-theme="dark"]` — dark theme

The active theme is set on the `<html>` element by the inline script in `Layout.astro` (reads `localStorage`, falls back to `prefers-color-scheme`). During client-side navigation the theme is re-applied via the `astro:page-load` handler.


