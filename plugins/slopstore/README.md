# Slop Store

Publish the app you built with Claude Code to [Slop Store](https://slopapp.store), a free app store for apps made with AI, so anyone can play it in the browser with nothing to install. Ask Claude to "publish this app to Slop Store", or run `/slopstore:publish`.

It works with plain HTML, Vite, React, Vue and Svelte, and with Expo, Flutter and Capacitor phone apps, which play in a phone frame.

## What it runs, sends and stores

- It runs one command in your app's folder: `npx slopstore@0.2.3 publish --yes --json`. npx downloads the `slopstore` package, version 0.2.3, which has no dependencies, from the npm registry.
- For Vite, React, Vue and Svelte projects the command first runs your project's own `build` script, installing dependencies when `node_modules` is missing. For Expo, Flutter and Capacitor projects it runs their web build in a temporary folder.
- It uploads the built app's files to https://slopapp.store. For phone apps it also uploads a small set of your source files that the reviewer reads and that are never served. Every version is checked before it goes live. Nothing is sent anywhere else.
- The first publish creates a free Slop Store identity. Its key is saved on your computer in `~/.config/slopstore/config.json` (`%APPDATA%\slopstore\config.json` on Windows) and is never printed. The command also writes `slopstore.json`, which holds the app's slug, in your project.
- If Node isn't available, the skill can instead send a single HTML file to `https://slopapp.store/api/v1/publish` with curl.

The plugin has no hooks, no MCP server and no background activity: nothing runs until you ask to publish. Publishing makes the app public, so Claude asks first when you haven't clearly asked to publish to Slop Store.

## License

MIT
