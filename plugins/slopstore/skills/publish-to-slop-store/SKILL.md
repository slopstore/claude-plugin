---
name: publish-to-slop-store
description: Publish the web app, game or tool in this project to Slop Store (slopapp.store), the app store for AI-made apps, so anyone can play it in the browser. Use when the user asks to publish, share or post their app on Slop Store, or asks for a public page where people can try what they built.
---

# Publish to Slop Store

Slop Store (https://slopapp.store) is a free app store for apps made with AI. Each published app gets its own page where anyone can play it in the browser, with nothing to install. Phone apps made with Expo, Flutter or Capacitor play in a phone frame.

## Before you publish

- Publishing makes the app public. If the user has not clearly asked to publish to Slop Store, ask first.
- Never publish API keys or other secrets. The CLI refuses a publish that contains a likely key: move the key out of the app instead of working around the check.
- Server-rendered apps (for example Next.js in server mode) are not supported. A static build is, including a Next.js static export (`out/`).

## Publish

Run this in the app's folder:

```bash
npx slopstore@0.2.3 publish --yes --json
```

- Needs Node 18 or newer. There is no account or login step: the first publish creates a free Slop Store identity, saves its key on this computer (it is never printed) and prints a claim link. Show the user that link: opening it while signed in attaches the app to their own account. It expires in 7 days.
- Vite, React, Vue and Svelte projects are built for you. For other tools, build first (for example `npm run build`) and publish the output with `--no-build --dir <folder>`.
- The title comes from the project (`slopstore.json`, the page `<title>`, Expo `app.json`, Flutter `pubspec.yaml`, the Capacitor config or `package.json`). If none is found, the command says so: pass `--title "<title>"`. Tagline and category are optional (`--tagline "What it does in one line"`, `--category auto`).
- To preview without any network call: `npx slopstore@0.2.3 publish --dry-run`.
- If the user already has a Slop Store key, set `SLOPSTORE_API_KEY` instead of creating a new identity.

## Read the result

With `--json`, stdout is exactly one JSON object. Exit codes:

- `0`: live. Give the user the page link (`https://slopapp.store/apps/<slug>`).
- `2`: not approved. Read `reason`, fix the cause, and publish again.
- `3`: waiting for a person, or still being checked. Check later with `npx slopstore@0.2.3 status`.
- `1`: error. The message says what to change.

Every version is checked before it goes live, usually within about a minute.

## Updates

The first publish writes `slopstore.json` with the app's `slug`. Commit it: later runs publish a new version of the same app at the same link. A new version only replaces the live one after it passes the check.

## Without Node

A single-file HTML app can be published with one HTTP call, and the first one needs no key:

```bash
curl -s https://slopapp.store/api/v1/publish \
  -H 'Content-Type: application/json' \
  -d '{"title":"My App","html":"<h1>My App</h1>"}'
```

The response includes `agent.api_key`, shown once. Keep it out of the app's files and send it as `Authorization: Bearer <key>` for later updates. Full reference: https://slopapp.store/llms.txt
