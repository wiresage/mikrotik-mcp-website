# MikroTik MCP — Website

Source for the **[MikroTik MCP](https://github.com/wiresage/mikrotik-mcp)** project website —
the landing page and documentation for an open-source [Model Context Protocol](https://modelcontextprotocol.io)
server that lets AI assistants manage MikroTik RouterOS devices in plain English — and for its siblings
[routeros-lsp](https://github.com/wiresage/routeros-lsp) (a language server for RouterOS scripts) and
[routeros-skills](https://github.com/wiresage/routeros-skills) (agent skills for RouterOS).

## Layout

| Folder | What it is |
| --- | --- |
| [`website-src/`](website-src/) | The deployable static site — hand-written HTML, one shared CSS file, vanilla JS. Ships with an nginx Dockerfile and compose file. **Start here.** |
| [`website-design/`](website-design/) | The design reference the site is built against: the pages as designed, including the language-server and agent-skills sections. Kept for provenance; not deployed. |

## Quick start

The site is plain static files — no build step. Serve `website-src/` with any static server:

```bash
cd website-src
python -m http.server 8080      # then open http://localhost:8080
```

Or run it in a container:

```bash
cd website-src
docker compose up -d --build    # serves http://localhost:8080
```

See [`website-src/README.md`](website-src/README.md) for the full development and Docker guide.

## License

MIT — see the [main project license](https://github.com/wiresage/mikrotik-mcp/blob/master/LICENSE).
Not affiliated with or endorsed by MikroTik / SIA Mikrotīkls.
