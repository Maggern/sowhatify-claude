# SoWhatify for Claude Code

Understand what news, articles and documents mean for *you*, inside Claude Code.

This repository is the plugin marketplace for [SoWhatify](https://sowhatify.com).
It holds one plugin, `sowhatify`, which adds:

- the SoWhatify connection, with sign-in in the browser and no token to copy,
- four skills Claude uses on its own when they fit: running your Templates,
  picking a Template for you, competitor news, and what news means for your
  company,
- the command `/sowhatify:analyze <url or text>`.

## Install

In Claude Code:

```
/plugin marketplace add Maggern/sowhatify-claude
/plugin install sowhatify@sowhatify
```

Then run `/mcp` and approve the connection in your browser. To check it worked,
ask: "Ask SoWhatify who I am."

More in [the plugin's README](claude-plugin/sowhatify/README.md) and
[INSTALLATION.md](claude-plugin/sowhatify/INSTALLATION.md).

## Using Claude.ai or Claude Desktop?

Plugins are for Claude Code. On claude.ai and in Claude Desktop, add SoWhatify as
a connector and upload the same skills as ZIP files. Both are on
<https://sowhatify.com/connect/claude/>.

## Where this comes from

This repository is generated from SoWhatify's own source and replaced on each
release, so changes made here directly will be overwritten. Report problems at
<https://sowhatify.com/support.php>.
