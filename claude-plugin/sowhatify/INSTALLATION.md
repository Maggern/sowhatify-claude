# Installing SoWhatify for Claude

Three ways in for Claude Code; the first is the one to use. Claude.ai and Claude
Desktop take the connector and the skills separately — see section 4.

## 1. The plugin (Claude Code)

```
/plugin marketplace add Maggern/sowhatify-claude
/plugin install sowhatify@sowhatify
```

Then `/mcp` → authorize in the browser. Confirm it worked by asking Claude to
call `whoami`.

You get the MCP server, the four skills, and `/sowhatify:analyze`.

## 2. The connector alone, without the plugin

Useful for development, and for Claude clients that take connectors but not
plugins. Every variant is generated for you, per client, at
<https://sowhatify.com/connect/claude/>.

**Claude Code:**

```
claude mcp add --transport http sowhatify https://sowhatify.com/mcp/
```

**Claude Desktop / Claude.ai:** Settings → Connectors → Add custom connector.
Paste `https://sowhatify.com/mcp/`, leave "Sign in now" selected, leave the OAuth
client on Claude's published identity, and leave Request headers **empty** — that
box is for servers wanting an API key, and this one hands Claude its own
credential through the approval page.

Claude may show "No sign-in — Detected" next to the third option. Ignore it; it
comes from one open discovery endpoint, and sign-in works.

### A shorter tool list for chat

The server publishes its full tool list — over sixty — which is right for the
Chrome extension and for authoring work in Claude Code, but more than a chat
connector needs. Connecting to

```
https://sowhatify.com/mcp/?tools=core
```

lists 15 instead — the ones a normal conversation uses: find a template, run it,
save the result, read your history and profile. Everything else still works if
called; the profile filters what is *listed*, not what is allowed, because a
query parameter the caller controls is the wrong place for a permission check.

Recommended for Claude.ai and Claude Desktop. Not for the plugin, and not for
Claude Code — the skill there uses the authoring tools, which `core` leaves out.
Plain `/mcp/` keeps the full list, so existing connections are unaffected.

## 3. Personal access token (headless, or by preference)

For a machine with no browser, or if you would rather hold a token than run the
OAuth flow.

1. Sign in at <https://sowhatify.com/app/claude.php> and click **Generate MCP
   connection** — or, if you already have one, **Regenerate token** under
   Connections on <https://sowhatify.com/app/account.php#connections>.
2. Copy the token. It is shown once and on its own rather than embedded in a URL
   — the MCP specification forbids access tokens in a query string. Generating a
   new one stops the old one working.
3. ```
   claude mcp add --transport http sowhatify https://sowhatify.com/mcp/ \
     --header "Authorization: Bearer YOUR_TOKEN"
   ```

This replaces the browser sign-in rather than adding to it. The plugin itself no
longer carries a token field, so use this path outside the plugin.

## 4. Claude.ai and Claude Desktop

These have no plugins. Add the connector as in section 2, then upload the skills:

1. Check code execution is on: Settings → Capabilities. Skills need it.
2. Download the skill ZIPs from <https://sowhatify.com/connect/claude/>. Keep
   each one zipped.
3. Customize → Skills → **+** → Create skill → **Upload a skill**, and pick one
   ZIP. Repeat for each.

They are the same four skills, renamed `sowhatify`, `sowhatify-template-selection`,
`sowhatify-competitive-intelligence` and `sowhatify-product-impact` so they read
clearly beside your other skills, with descriptions short enough for claude.ai's
200-character limit. A Team or Enterprise owner can add them for everyone under
Organization settings → Plugins & skills.

The same ZIPs work in Claude Code without the plugin: unzip each into
`~/.claude/skills/`.

## Verifying

```
/mcp
```

should list `sowhatify` as connected. Then:

> Ask SoWhatify who I am.

Claude calls `whoami` and reports the account, plan and verification state.

## Troubleshooting

**`/mcp` shows the server but every call is unauthorized.** The OAuth token
expired or was revoked. Reconnect from `/mcp`.

**The token path works but OAuth doesn't, on your own deployment.** Check that
`.htaccess` carries `CGIPassAuth On` and that
`/.well-known/oauth-protected-resource/mcp` returns metadata — RFC 9728 appends
the resource path to the well-known prefix, and the rewrite for it has to run
*before* the `/mcp` → `/mcp/` redirect.

**A tool rejects your arguments.** Read the error; the server names the field and
what it expected, and refuses rather than silently correcting. Step ids in
particular are assigned by the server: omit `id` when creating workflow steps and
read the real ids back from the result.
