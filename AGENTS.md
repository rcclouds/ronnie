# AGENTS.md

## Project Overview
Static HTML obfuscator tool. `index.html` is a client-side script that fetches `n1.html`,
compresses/obfuscates it (LZ-String base64 + chunk transforms), and redirects to a blob URL
that reconstructs the page after human-interaction checks. `scripts/build.js` does the same
at build time (Node.js, deps: minimist + lz-string).

## Setup
- No build step needed for dev — files are static HTML served directly.
- Served via `docker-compose.base44.yml` using nginx:alpine on port 3000.
- The repo directory has 700 permissions, so nginx must run workers as root
  (custom `nginx.base44.conf` with `user root;` is mounted into the container).
- No external credentials or secrets required.

## Verify
- `curl http://localhost:3000/` → 200, serves `index.html`
- `curl http://localhost:3000/n1.html` → 200, serves `n1.html`
- The preview shows the obfuscator tool; it fetches n1.html client-side and creates a blob redirect.
