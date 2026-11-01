# Fahadul Shadhin — Website

A personal website built with Astro, featuring selected projects, professional experience, education, and a Markdown-powered blog. The site uses a warm monochrome design with a persistent light/dark theme toggle.

## Getting started

### With Docker Compose

From the project directory, build and start the website in the background:

```sh
docker compose up --build -d
```

Open [http://localhost:8080](http://localhost:8080). To view container logs, run `docker compose logs -f`; to stop the website, run `docker compose down`.

To run it in the foreground instead, omit `-d` and stop it with `Ctrl+C`:

```sh
docker compose up --build
```

### Local development

Requires Node.js and npm.

```sh
npm install
npm run dev
```

Astro prints the local development URL in the terminal.

## Commands

| Command | Description |
| --- | --- |
| `npm run dev` | Start the development server |
| `npm run build` | Build the static site into `dist/` |
| `npm run preview` | Preview the production build locally |
| `docker compose up --build -d` | Build and run the website in the background |
| `docker compose down` | Stop and remove the website container |

## Content

- Portfolio content is organized in `src/data/`.
- Blog posts are Markdown files in `src/content/blog/`.
- The profile image is stored in `assets/`.

## Tech stack

Astro · TypeScript · Markdown
