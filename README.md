# SoWhatify for Claude

Understand what news, articles and documents mean for *you* — your
[SoWhatify](https://sowhatify.com) profile, templates, perspectives and workflows,
inside Claude.

## Install (Claude Code)

```
/plugin marketplace add Maggern/sowhatify-claude
/plugin install sowhatify@sowhatify
```

Then run `/mcp` and authorize in the browser. No token to copy, and no account
needed up front.

**Claude Desktop or claude.ai:** add `https://sowhatify.com/mcp/?tools=core` as a
custom connector instead (Settings → Connectors). Instructions for every client:
<https://sowhatify.com/connect/claude/>.

## What you get

- The `sowhatify` remote MCP server, signed in with OAuth 2.1.
- Four skills: `sowhatify`, `template-selection`, `competitive-intelligence`,
  `product-impact`.
- `/sowhatify:analyze <url or text>` for a quick one-shot analysis.

See the [plugin README](claude-plugin/sowhatify/README.md),
[INSTALLATION.md](claude-plugin/sowhatify/INSTALLATION.md) and
[SECURITY.md](claude-plugin/sowhatify/SECURITY.md).

This repository is a published copy; changes are made upstream and synced here.
Report problems at <https://sowhatify.com/support.php>.
