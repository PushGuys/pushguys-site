# PushGuys/pushguys-site — Agent Guidance

Static GitHub Pages marketing site for Push Guys, LLC. Plain HTML with inline CSS.
Zero JavaScript, zero dependencies, no build step, no package manager, no CI.
Production host: GitHub Pages, custom domain `pushguys.co` (see `CNAME`).

## Stack

- HTML + inline CSS only (no JS, no framework, no bundler)
- Served in production by GitHub Pages from the `main` branch root
- Any static file server works for local development

## Commands

The repo ships no canonical dev command and no package manager. The adopted local convention:

```bash
# serve from repo root (any static server works; port is arbitrary)
python3 -m http.server 8177 --bind 127.0.0.1
# then open http://127.0.0.1:8177/
```

There are no install, build, lint, typecheck, or test commands — none exist in this repo.
Do not invent any.

## Codebase map

Tiny repo (5 files, no directories) — map inlined here instead of a separate
`codebase-map.md`:

| Path | Purpose |
|---|---|
| `index.html` | Home page — company blurb, contact email, shared nav |
| `about.html` | About page — company background |
| `contact.html` | Contact page — email + postal address |
| `privacy.html` | Privacy policy (effective May 2026) |
| `CNAME` | GitHub Pages custom domain: `pushguys.co` |

All four pages share the same nav (`/`, `/about.html`, `/contact.html`, `/privacy.html`)
and the same inline stylesheet; keep them in sync when adding a page.

## Local verification

1. Start a static server (command above) from the repo root.
2. Fetch each page and assert HTTP 200 plus the expected `<title>` / `<h1>`:
   `/`, `/about.html`, `/contact.html`, `/privacy.html`.
3. Confirm the nav link graph resolves: every `href` on `index.html` must return 200.
4. Confirm unknown paths return 404.

No linter, typechecker, or test suite exists to run.

## Snapshot

- Sandbox snapshot captured during onboarding: `2026-10-14T13:32:11.130Z`
- Snapshot/template ID: `hhz7jagsiohgl0wkf2i2:default` (sandbox `i5wgn9yjhhpfw8jnwmh1l`)

## Validation summary (onboarding, 2026-10-14)

- `dev_stack_healthy: true` — static server up on `127.0.0.1:8177`
- Primary flow verified end-to-end over HTTP: all 4 pages returned 200 with correct
  titles/h1s; full nav link graph resolved; 404 behavior confirmed.
- Evidence limits: no headless browser in the sandbox, so verification used HTTP-level
  content assertions instead of screenshots/console. No lint/typecheck/tests exist.
