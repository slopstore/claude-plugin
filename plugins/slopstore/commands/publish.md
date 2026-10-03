---
description: Publish the app in this folder to Slop Store so anyone can play it in the browser
argument-hint: "[app folder]"
allowed-tools: Bash(npx slopstore@0.2.3 publish:*), Bash(npx slopstore@0.2.3 status:*)
---

Publish the app in `$ARGUMENTS` (the current folder if that is empty) to Slop Store, following the publish-to-slop-store skill.

Run `npx slopstore@0.2.3 publish --yes --json` in that folder. Then tell the user the app's page link, whether it is live or still being checked, and the claim link if the command printed one.
