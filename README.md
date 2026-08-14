# EM+X — MCP server

**Finished, on-brand `.pptx` and `.docx` from a brief — quality-gated by an
agentic consulting team.**

EM+X is a remote [MCP](https://modelcontextprotocol.io) server. Connect it to
any MCP-capable client (Claude, ChatGPT, Cursor, Codex, Grok, Copilot, …) and
your assistant can assemble a brief from the conversation, propose a document
structure for your approval, generate a presentation or document through a
multi-agent quality-gate stack, refine it by prompt, preview pages in an
interactive panel, and hand you a download link for the finished file.

- **Claude directory listing:** https://claude.ai/directory/em-x
- **Connector URL:** `https://emplusx.com/api/mcp`
- **Transport:** streamable HTTP
- **Auth:** OAuth 2.1 with dynamic client registration — sign in with your
  EM+X account; no API keys, no parameters to configure
- **Pricing:** works on every plan, including the free tier
  ([pricing](https://emplusx.com/pricing))
- **Docs:** https://emplusx.com/mcp

This repository is a thin, MIT-licensed descriptor for the hosted service —
the connector metadata and install instructions live here; the service itself
runs at emplusx.com.

## Install

### Claude (web / desktop / mobile)

EM+X is a listed connector in the Claude directory: open
[claude.ai/directory/em-x](https://claude.ai/directory/em-x) and click
**Connect** — no URL to paste, and one connect covers claude.ai, Claude
Desktop, and mobile. In the desktop app,
[claude://claude.ai/directory/em-x](claude://claude.ai/directory/em-x)
opens the listing directly.
(Step-by-step: https://emplusx.com/connect)

### Claude Code

```
claude mcp add --transport http emplusx https://emplusx.com/api/mcp
```

### Cursor

[Install in Cursor](cursor://anysphere.cursor-deeplink/mcp/install?name=emplusx&config=eyJ1cmwiOiAiaHR0cHM6Ly9lbXBsdXN4LmNvbS9hcGkvbWNwIn0=)
— or add to `~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "emplusx": {
      "url": "https://emplusx.com/api/mcp"
    }
  }
}
```

### Any other MCP client

Point the client at `https://emplusx.com/api/mcp` (streamable HTTP). The
OAuth flow is discovered automatically per RFC 9728; the browser opens the
EM+X sign-in and you're connected.

## What the tools do

The server exposes 33 tools. The core flow:

| Tool | What it does |
|---|---|
| `create_deliverable` | Files a brief (title, audience, decision, evidence) and proposes a page-by-page structure |
| `update_brief` | Enriches the brief and re-proposes — the server flags thin evidence rather than guessing |
| `confirm_and_generate` | Builds the document through the quality-gate stack (architect, writer, designer, critic, partner review) |
| `refine_deliverable` | Revises a built document by instruction ("tighten section 2") — every revision is a new version |
| `approve_deliverable` | Records sign-off on the exact version reviewed |
| `get_download_link` | Mints an expiring link for the finished `.pptx` / `.docx` |
| `list_templates` / `get_template_upload_link` | Manage the brand-template library from chat |
| `clone_style` | Reuses another project's extracted brand style |
| `show_deliverable_panel` | Opens an interactive panel (MCP Apps): outline review, live build progress, page previews, version compare, refine/approve/download |

The remaining tools power the interactive panel (page previews, version
scrubbing, account/usage display) on hosts that support MCP Apps; on
text-only hosts the flow works through the core tools alone.

## Links

- Product: https://emplusx.com
- Connector docs & FAQ: https://emplusx.com/mcp
- Setup guide: https://emplusx.com/connect
- Pricing: https://emplusx.com/pricing
- Security: https://emplusx.com/security ·
  [Privacy](https://emplusx.com/privacy) · [Terms](https://emplusx.com/terms)
- Support: hello@emplusx.com

## License

The contents of this repository (metadata and documentation) are
[MIT-licensed](LICENSE). The EM+X service is a commercial product of Cubed
Studios, a subsidiary of Cubed Ventures LLC.
