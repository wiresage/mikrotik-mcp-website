# MikroTik MCP — static documentation site
# Served by nginx. Build context is this directory (website-src/).
FROM nginx:alpine

# Drop the default nginx site config and use ours.
RUN rm -f /etc/nginx/conf.d/default.conf
COPY nginx.conf /etc/nginx/conf.d/default.conf

# Copy only the site assets — not the Docker/README tooling.
COPY index.html styles.css /usr/share/nginx/html/
# Browser tab and home-screen icons. These must be copied explicitly: the page links to them at the
# site root, and an icon that is missing from the image is a silent 404.
COPY favicon.svg favicon.ico favicon-16.png favicon-32.png apple-touch-icon.png /usr/share/nginx/html/
COPY docs/ /usr/share/nginx/html/docs/

EXPOSE 80

HEALTHCHECK --interval=30s --timeout=5s --start-period=5s --retries=3 \
  CMD wget -q --spider http://localhost/ || exit 1

CMD ["nginx", "-g", "daemon off;"]
