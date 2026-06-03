# ShotAPI — Screenshot & Render MCP Server for AI Agents

Give AI agents eyes — let Claude, Cursor, and other agents capture webpages and render HTML directly through MCP.

**One command to connect, zero setup:**

```bash
# Claude Code (remote mode — no install needed)
claude mcp add --transport streamable-http shotapi https://aiphotoshop.mynatapp.cc/mcp

# Claude Desktop / Cursor — add to config JSON:
# "shotapi": { "type": "streamable-http", "url": "https://aiphotoshop.mynatapp.cc/mcp" }
```

## Features

| Tool | Description |
|------|-------------|
| `screenshot_one_liner` | Capture a webpage as JPEG — just pass a URL |
| `screenshot` | Full control: viewport, full-page, element selector, format |
| `render` | HTML/CSS → image. Turn markup into a visual preview |

- **Direct access** — China tunnel, no VPN needed
- **Free tier** — 100 screenshots + 100 renders/month (IP-based, no signup)
- **Paid tier** — 20K+ calls/month with API Key ($9.90/mo Pro, $29.90/mo Business)

## Connection Modes

### Remote (Streamable HTTP) — Recommended

Zero local install. Free tier shares server quota across all remote users.

```bash
# Claude Code
claude mcp add --transport streamable-http shotapi https://aiphotoshop.mynatapp.cc/mcp

# Claude Desktop (claude_desktop_config.json)
{
  "mcpServers": {
    "shotapi": {
      "type": "streamable-http",
      "url": "https://aiphotoshop.mynatapp.cc/mcp"
    }
  }
}

# Cursor (.cursor/mcp.json)
{
  "mcpServers": {
    "shotapi": {
      "type": "streamable-http",
      "url": "https://aiphotoshop.mynatapp.cc/mcp"
    }
  }
}
```

### Local (Stdio) — For Paid Users

Set `SHOTAPI_KEY` env var for dedicated paid quota (not shared with free pool).

```bash
# Claude Code
claude mcp add screenshot-api -e SHOTAPI_KEY=your_key python mcp_stdio.py

# Claude Desktop
{
  "mcpServers": {
    "screenshot-api": {
      "command": "python",
      "args": ["mcp_stdio.py"],
      "env": { "SHOTAPI_KEY": "your_key", "SHOTAPI_BASE_URL": "https://aiphotoshop.mynatapp.cc" }
    }
  }
}
```

## Pricing

| Tier | Price | Quota |
|------|-------|-------|
| Free | $0/mo | 100 screenshots + 100 renders/month (IP-based) |
| Starter | $4.90/mo | 5,000 each |
| Pro | $9.90/mo | 20,000 each |
| Business | $29.90/mo | 100,000 each |

Chinese users can pay via [爱发电](https://afdian.com/a/shotapi/plan) (WeChat/Alipay).

## API Reference

### Screenshot

```
GET /v1/screenshot?url=https://example.com&width=1280&height=720&format=jpeg&block_ads=true
GET /v1/screenshot?url=https://example.com&fullpage=true
GET /v1/screenshot?url=https://example.com&selector=.main-content
```

Parameters: `url` (required), `width`, `height`, `fullpage`, `selector` (CSS), `format` (png/jpeg/webp), `block_ads`, `wait_for`, `ttl`

### Render

```
POST /v1/render  Body: {"html": "<h1>Hello</h1>", "width": 1280, "format": "png"}
```

Parameters: `html` (required), `width`, `height`, `format`

## Links

- **Website**: https://aiphotoshop.mynatapp.cc
- **Docs**: https://aiphotoshop.mynatapp.cc/docs
- **English Docs**: https://aiphotoshop.mynatapp.cc/en/docs
- **Pricing**: https://aiphotoshop.mynatapp.cc/en/pricing
- **Swagger**: https://aiphotoshop.mynatapp.cc/api-docs
- **Contact**: contact@shotapi.com

## License

This repository contains documentation and configuration only. The ShotAPI server software is proprietary.