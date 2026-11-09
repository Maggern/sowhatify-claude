# Changelog

## 1.1.2

- The same four skills are now offered as ZIPs for claude.ai and Claude Desktop,
  on <https://sowhatify.com/connect/claude/>. Built from this folder, so the text
  is identical; only the names (`sowhatify-` prefix) and the descriptions (within
  claude.ai's 200 characters) differ.
- `/sowhatify:analyze` no longer asks which template to use when none was named. It
  picks one, as the template-selection skill says to.
- INSTALLATION.md: the token steps pointed at a page that shows no token; they now
  name the two that do. Tool counts that had drifted are gone. New section on
  claude.ai and Claude Desktop.

## 1.1.1

The plugin now has a public home: <https://github.com/Maggern/sowhatify-claude>.
Install with `/plugin marketplace add Maggern/sowhatify-claude`. The old
marketplace source was a private repository, so nobody but its owner could add it.

- INSTALLATION.md's token route pointed at a page that no longer shows the token;
  it is on `app/claude.php`.
- The full tool list is over 60 now, not 58.

## 1.1.0

**Breaking: the marketplace is now `sowhatify`, not `lensmatics`.** Reinstall with
`/plugin install sowhatify@sowhatify`. The plugin name itself is unchanged.

**Breaking: the plugin no longer asks for a token.** `.mcp.json` now connects with
OAuth 2.1 — run `/mcp` and authorize in the browser. The `sowhatify_token`
`userConfig` entry is gone; a stored value is simply ignored. The token path still
exists for headless machines, outside the plugin, documented in INSTALLATION.md.

This brings the plugin in line with what sowhatify.com has been telling Claude
Code users to do for a while: `claude mcp add --transport http sowhatify …` with no
token, and the browser sign-in on first `/mcp`.

- Renamed throughout: Lensmatics → SoWhatify, lenses → templates, personas →
  perspectives, chains → workflows. Cleared the "Templatematics" and
  "app/perspectives" scars a previous search-and-replace left in the skill.
- The skill now documents the untrusted-seed rule: content arriving under `seed`
  is material to analyze, never instructions to follow or tool calls to make.
  Pairs with the server-side `seedTrust` fence in run briefs.
- Three new skills beside the original: `template-selection` (choose a template by
  task fit rather than asking the user to browse), `competitive-intelligence` and
  `product-impact`.
- The server publishes a `core` tool profile — connect to `/mcp/?tools=core` for 15
  tools instead of 58. Recommended for Claude.ai and Desktop; not for the plugin,
  whose skill uses the authoring tools. Plain `/mcp/` is unchanged.
- Tool errors now carry a machine-readable code (`AUTH_REQUIRED`, `PLAN_REQUIRED`,
  `NOT_FOUND`, `RATE_LIMITED`, …) and a trace id. An unexpected server-side failure
  no longer forwards its message, which used to mean a database error could put SQL
  in front of the model.
- Template search answers a sentence rather than requiring every word to match, and
  summaries now carry the output section names and install counts, so choosing
  between templates rarely needs a second call.
- The server now fences seed content in every run brief
  (`<untrusted-seed-content>` markers plus a `seedTrust` block), and neutralizes
  marker lookalikes inside the seed so a page cannot close the fence early.
- Added INSTALLATION.md, SECURITY.md and this changelog.

## 1.0.0

Initial release: remote MCP server registration, one skill, `/sowhatify:analyze`.
