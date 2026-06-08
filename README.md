# ShotAPI — Screenshot & Render MCP Server for AI Agents

> 🇨🇳 中文用户：给 AI Agent 加上"看网页"能力！一条命令连接，无需翻墙，支持微信支付宝。

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
- **Free tier** — 30 screenshots + 30 renders/month (IP-based, no signup)
- **Paid tier** — ¥29/月(标准版5000次) / ¥99/月(专业版20000次) — 支持微信支付宝
- **Paid tier (International)** — $4.90/mo Starter / $9.90/mo Pro

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
| Free | $0/mo | 30 screenshots + 30 renders/month (IP-based) |
| Starter | $4.90/mo | 5,000 each |
| Pro | $9.90/mo | 20,000 each |

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
- **Contact**: shotapi@outlook.com

## License

This repository contains documentation and configuration only. The ShotAPI server software is proprietary.

---

**Keywords**: MCP server, screenshot API, render HTML, AI agent, Claude MCP, Cursor MCP, streamable-http, webpage capture, web screenshot, 截图API, 网页截图, AI截图工具, MCP服务器