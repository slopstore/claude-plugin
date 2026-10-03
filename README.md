# Slop Store plugin for Claude Code

Publish the app you built with Claude Code to [Slop Store](https://slopapp.store), the app store for AI-made apps. Anyone can play it right in the browser, with nothing to install.

## Install

In Claude Code:

```
/plugin marketplace add slopstore/claude-plugin
/plugin install slopstore@slopstore
```

## Use

Say "publish this app to Slop Store", or run `/slopstore:publish`.

Claude runs `npx slopstore@0.2.3 publish --yes` in your app's folder. There is no sign-up to start: the first publish creates a free Slop Store identity and prints a link for attaching the app to your own account. Every app is checked before it goes live, usually within about a minute.

It works with plain HTML, Vite, React, Vue and Svelte, and with Expo, Flutter and Capacitor phone apps, which play in a phone frame.

## What's inside

- `skills/publish-to-slop-store`: when and how to publish, and how to read the result.
- `commands/publish.md`: the `/slopstore:publish` command.

Nothing runs until you ask to publish. The plugin has no hooks and no MCP server. [plugins/slopstore/README.md](plugins/slopstore/README.md) lists exactly what it runs, sends and stores. If you prefer MCP tools: `claude mcp add --transport http slopstore https://slopapp.store/mcp`

## License

MIT
