# MikroTik MCP — Website

The marketing and documentation site for **[MikroTik MCP](https://github.com/wiresage/mikrotik-mcp)**,
an open-source [Model Context Protocol](https://modelcontextprotocol.io) server that lets AI
assistants manage MikroTik RouterOS devices in plain English, and for its two sibling projects:
[routeros-lsp](https://github.com/wiresage/routeros-lsp), a language server for RouterOS scripts, and
[routeros-skills](https://github.com/wiresage/routeros-skills), agent skills that teach AI agents RouterOS
(listed on [skills.sh](https://www.skills.sh/wiresage/routeros-skills)).

This is a fully static site — hand-written HTML, one shared CSS file, and a little vanilla
JavaScript. There is no build step, framework, or bundler.

## Structure

```
.
├── index.html              # Landing page (MCP server, language server and agent skills bands)
├── styles.css              # Shared design system (dark theme, design tokens)
├── favicon.svg · favicon.ico · favicon-16.png · favicon-32.png · apple-touch-icon.png
├── docs/
│   ├── index.html          # Getting started — installation & testing
│   ├── configure.html      # Integrations — Claude Desktop, MCP Inspector, MCPO
│   ├── reference.html      # API reference — all 22 tool categories
│   ├── examples.html       # Examples — mcp-cli calls, workflows, natural language
│   ├── articles.html       # Articles & tutorials — 25 scenarios, Medium write-ups
│   ├── contributing.html   # Contributing guide
│   ├── lsp.html            # Language server (routeros-lsp) — install, editors, CLI, configuration
│   ├── lsp-rules.html      # routeros-lsp diagnostic rules — all 36, filterable
│   ├── skills.html         # Agent skills (routeros-skills) — 34 skills by area, with repo and skills.sh links
│   └── media/              # Landing-page demo assets (skills replay GIF + reduced-motion poster)
├── Dockerfile              # nginx image that serves this directory
├── docker-compose.yml      # One-command local container
├── nginx.conf              # Static-serving config (gzip, caching, security headers)
└── .dockerignore
```

> The `Dockerfile` copies files explicitly. A new top-level asset (an icon, a page, an image) is
> not in the image until it is added to a `COPY` line — it will 404 on the live site while working
> locally from the folder. `docs/` is copied as a whole, so new pages and `docs/media/` need nothing.

## Local development

The site is plain static files, so any static HTTP server works. Pick one:

```bash
# Python 3 (no install needed)
python -m http.server 8080

# Node
npx serve -l 8080

# PHP
php -S localhost:8080
```

Then open <http://localhost:8080>.

> Open the pages through a server rather than `file://` — the relative links and shared
> stylesheet resolve correctly that way.

## Docker

### docker compose (recommended)

```bash
docker compose up -d --build
```

The site is served at <http://localhost:8080>. Stop it with `docker compose down`.

### Plain Docker

```bash
docker build -t mikrotik-mcp-website .
docker run --rm -p 8080:80 mikrotik-mcp-website
```

The container runs nginx, serves the static files from `/usr/share/nginx/html`, and ships a
healthcheck that pings `/`. Host port `8080` maps to container port `80`; change the left side
of the mapping if `8080` is taken.

## Deployment

The image is a self-contained nginx server, so it runs anywhere that accepts a container
(Fly.io, Render, a VPS, Kubernetes, etc.). For plain static hosting (GitHub Pages, Netlify,
Cloudflare Pages, S3), upload `index.html`, `styles.css`, and the `docs/` folder as-is — no
build is required.

## License

MIT — see the [main project license](https://github.com/wiresage/mikrotik-mcp/blob/master/LICENSE).
Not affiliated with or endorsed by MikroTik / SIA Mikrotīkls.
