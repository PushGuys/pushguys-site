---
name: local-dev
description: How to run and verify pushguys-site locally (static GitHub Pages site)
---

# local-dev — PushGuys/pushguys-site

## Context

Repo is a static GitHub Pages site: 4 HTML pages (`index`, `about`, `contact`,
`privacy`) + `CNAME` (`pushguys.co`). Plain HTML with inline CSS. No JS, no
dependencies, no build step, no package manager, no CI, no tests. The repo
prescribes no dev command — this skill records the convention adopted during
onboarding (2026-10-14).

## Start the dev stack

No install step. No services, no database, no env vars, no secrets.

```bash
# from repo root, any static file server; 8177 is the adopted default port
python3 -m http.server 8177 --bind 127.0.0.1
# server listens on http://127.0.0.1:8177/
```

Node (v20) is also available if you prefer `npx serve` — any static server is fine.
Check for a stale server on the port first (`ss -tlnp | grep 8177`).

## Verify (primary flow)

Static-site primary flow = every page loads with the right content and every nav
link resolves. Verify over HTTP (no headless browser was available at onboarding):

```bash
B=http://127.0.0.1:8177
for p in / /about.html /contact.html /privacy.html; do
  curl -s -o /tmp/page.html -w "%{http_code} $p\n" "$B$p"
  grep -o '<title>[^<]*</title>' /tmp/page.html
done
# every nav href on index must be one of the pages above (mailto: is external)
curl -s $B/ | grep -o 'href="[^"]*"'
curl -s -o /dev/null -w 'unknown path -> %{http_code}\n' $B/missing.html   # expect 404
```

Expected at onboarding: all four pages 200 with titles "Push Guys, LLC",
"About – Push Guys, LLC", "Contact – Push Guys, LLC", "Privacy Policy – Push Guys, LLC".

## Proof status

- Lint/typecheck/tests: none exist — nothing to run.
- Screenshots: not capturable in the onboarding sandbox (no headless browser);
  HTTP-level content assertions were the recorded evidence.

## Gotchas

- Keep the nav identical across all four pages; they duplicate the same markup.
- Serving must be from the repo root (pages reference `/about.html` style paths).
- Nothing to build before deploy: GitHub Pages serves `main` root as-is.
