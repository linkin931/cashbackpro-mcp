# CashbackPro MCP Server

**AliExpress cashback for AI assistants.** Search products, estimate cashback, and generate personal cashback links — purchases made through them earn the connected CashbackPro user a share of the affiliate commission.

This is a **remote MCP server** (Streamable HTTP). This repository hosts the docs and manifest; the server itself runs at:

```
https://cashbackpro.org/api/mcp
```

- 🌐 Landing & setup guide: [cashbackpro.org/mcp](https://cashbackpro.org/mcp)
- 📦 Official MCP Registry: [`org.cashbackpro/cashbackpro`](https://registry.modelcontextprotocol.io/v0/servers?search=cashbackpro)

## Quick start

### Claude Code

```bash
claude mcp add --transport http cashbackpro https://cashbackpro.org/api/mcp
```

### Any MCP client (JSON config)

```json
{
  "mcpServers": {
    "cashbackpro": {
      "type": "streamable-http",
      "url": "https://cashbackpro.org/api/mcp"
    }
  }
}
```

Works out of the box — no account needed (see [Anonymous mode](#anonymous-mode) below).

## Tools

| Tool | What it does |
|---|---|
| `search_products` | Search AliExpress products (quality-filtered results) |
| `get_product_details` | Product details + estimated cashback |
| `calculate_cashback` | Estimate cashback for an amount by user level (Bronze 30% → VIP 80% of commission) |
| `get_cashback_link` | Generate an affiliate link. With a connected account the purchase is attributed to the user and earns them cashback |

## Connecting your CashbackPro account

To earn cashback, pass your personal token as a Bearer header. Get it at [cashbackpro.org/connect-extension](https://cashbackpro.org/connect-extension) (free account, sign-in with Google), then:

```json
{
  "mcpServers": {
    "cashbackpro": {
      "type": "streamable-http",
      "url": "https://cashbackpro.org/api/mcp",
      "headers": {
        "Authorization": "Bearer <your-token>"
      }
    }
  }
}
```

Full walkthrough with screenshots: [cashbackpro.org/mcp](https://cashbackpro.org/mcp).

## Anonymous mode

Without a token, all tools still work. `get_cashback_link` returns a generic affiliate link — **no cashback is earned** (the commission supports the service), and every response includes a disclosure asking the assistant to tell the user how to connect an account and start earning.

## Notes

- Cashback is credited after AliExpress confirms the order settlement.
- Rate limit: 30 requests/min per IP.
- Source code is not published; this repo exists for documentation and marketplace listings. Issues and questions are welcome in the [issue tracker](../../issues).

---

© [CashbackPro](https://cashbackpro.org) — AliExpress cashback platform.
