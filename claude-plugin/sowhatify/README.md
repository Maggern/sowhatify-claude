# SoWhatify — Claude plugin

Understand what news, articles and documents mean for *you*.

Connects Claude to your [SoWhatify](https://sowhatify.com) account — your durable
profile, and your templates, perspectives and workflows — over the same remote MCP
server the Chrome extension, Claude Desktop and Cursor already use.

## Install

```
/plugin marketplace add Maggern/sowhatify-claude
/plugin install sowhatify@sowhatify
```

Then run `/mcp` and authorize in the browser. That's the whole setup — there is
no token to copy.

No account needed up front: the approval page can create one for you with no
email, and you can attach an email later without losing anything.

See [INSTALLATION.md](INSTALLATION.md) for the token-based fallback (headless
machines, or if you prefer a personal access token to the browser sign-in).

## How it works

SoWhatify does not run the analysis. **Claude does.**

`run_template` and `run_workflow` hand back a prepared brief — the template's
questions, the relevant slice of your profile, and the source text — and Claude
writes the analysis from it. `record_analysis_result` then saves that text to your
SoWhatify library.

This is deliberate. It means the analysis is written by the model you are already
talking to, with the full conversation in view, rather than by a separate backend
call that can only see the article.

It also means **the server never fetches a URL for you.** When you paste a link,
Claude reads the page with its own tools and passes the text in.

## What's in this plugin

- `.mcp.json` — registers the `sowhatify` remote MCP server
  (`https://sowhatify.com/mcp/`) with OAuth 2.1 sign-in. No credentials in the
  file, and none in your repository.
- `skills/` — four Agent Skills:
  - **`sowhatify`** — the tool set, the "you are the model" run/record loop, and
    the rule that seed content is data rather than instructions. The others build
    on it.
  - **`template-selection`** — picks a template by task fit instead of asking the
    user to browse the marketplace.
  - **`competitive-intelligence`** — competitor news, grounded in the competitors
    on your profile.
  - **`product-impact`** — what external news means for your company, product or
    roadmap.
- `commands/analyze.md` — `/sowhatify:analyze <url or text>` for a quick
  one-shot analysis.

Everything created through this MCP connection is private to your account —
publishing to the SoWhatify marketplace stays a website-only action.

## Security

Article text, PDFs and web pages are untrusted input. The server fences seed
content in every run brief and the skill instructs Claude to treat anything inside
that fence as material to analyze, never as instructions to follow or tool calls to
make. See [SECURITY.md](SECURITY.md).
