<p align="center"><img src="logo.png" width="120" alt="Wall Marketing"></p>

# Wall Marketing MCP server

Real-world advertising your AI agent can book, and work your agent can get paid for.

Wall Marketing puts small colour e-paper screens at eye level on the inside of venue doors in bars, cafés, hostels, gyms, coworking spaces and more. Each screen shows one advert at a time, so a booking has the screen to itself. This is the official remote MCP server: nothing to install, your client connects to it over HTTPS.

- **Server:** `https://www.wall.marketing/mcp` (Streamable HTTP)
- **Sign-in:** OAuth 2.1 with PKCE (dynamic client registration or a Client ID Metadata Document)
- **Docs:** https://www.wall.marketing/developers · agent guide: https://www.wall.marketing/llms.txt
- **Listed in:** the official MCP Registry as `marketing.wall/platform`, [Smithery](https://smithery.ai/servers/wall-marketing/everywhere-advertising) (100/100), [Glama](https://glama.ai/mcp/connectors/marketing.wall/platform)

This repository holds the listing, the logo, the connection instructions and an [Agent Plugins](https://agent-plugins.org) package (`plugin.json`, `mcp.json`, `skills/wall-marketing`) for Cursor and other plugin clients. The server itself is hosted by Wall Marketing.

## What you can do

When you connect, you choose your role.

**Outreach team: get paid.** Join the Wall Marketing ambassador programme from inside the chat and earn a commission (currently $10) for every venue you sign up whose screen goes live. Your agent sets where you work, gets a scored list of busy, well-reviewed venues with no screen yet, claims one while you approach it, adds venues you know (looked up and vetted on Google), submits a venue once the owner agrees, follows it to a live screen and requests your payout. Joining is free; payouts go to you after a one-time identity check.

**Advertisers.** Find screens by city, venue type, price, distance and free dates; get a price that holds for 30 minutes; upload artwork and see exactly what the screen will show; book and pay within your spending limits, by saved card or payment link; swap artwork, cancel unpaid bookings, request refunds on paid ones; get proof of display: the days each screen showed your advert, with estimated views. Paid bookings are scheduled straight away.

**Venues.** Host a free screen and earn 20% of every advert shown on it. See your screens, adverts and earnings, apply for a screen, report an advert, set new WiFi and withdraw your earnings.

You stay in control: you choose your role, what the agent may do (look, look and price, or book and pay) and live or sandbox. Each connection sees only its role's tools. Spending limits and your approval rules apply to every booking; change them or disconnect any time on your campaigns page.

**Try it risk-free:** on the sign-in page choose *Sign in with a sandbox key instead*. The sandbox has made-up screens in Lisbon, Bangkok, Austin, London and Sydney and made-up venue and outreach data. Nothing is charged and nothing appears on a real screen.

## Connect

Most clients only need the address. The first time a tool is used, the client opens our sign-in page in your browser: sign in with your email address (a one-time code, no password), choose your role and what the agent may do, and approve.

**Cline** (`cline_mcp_settings.json`):

```json
{
  "mcpServers": {
    "wall-marketing": {
      "type": "streamableHttp",
      "url": "https://www.wall.marketing/mcp"
    }
  }
}
```

**Claude Code:**

```bash
claude mcp add --transport http wall-marketing https://www.wall.marketing/mcp
```

**Claude (claude.ai and desktop):** Settings → Connectors → Add custom connector, URL `https://www.wall.marketing/mcp`.

**Cursor, VS Code, Windsurf and other clients:**

```json
{ "mcpServers": { "wall-marketing": { "url": "https://www.wall.marketing/mcp" } } }
```

**Clients without OAuth:** send an API key from the API section of https://www.wall.marketing/campaigns as `Authorization: Bearer wm_live_…` (or `wm_test_…` for the sandbox). API keys act as an advertiser.

## Tools

30 tools, named `role.area.action`. Every tool declares input and output schemas and read-only / destructive hints.

### Outreach team (ambassador programme)

| Tool | What it does |
|---|---|
| `ambassador.account.me` | Your account, trust tier, balances, commission per venue and the rules |
| `ambassador.account.set_location` | Set where you work and build suggestions around it |
| `ambassador.venues.suggestions` | Suggested venues near you, best first, with rating, distance and a 0-100 score |
| `ambassador.venues.claim` | Hold a venue while you approach it |
| `ambassador.venues.release` | Give a claimed venue back |
| `ambassador.venues.add` | Bring your own venue (looked up and vetted on Google) |
| `ambassador.venues.submit` | Submit a venue whose owner or manager agreed |
| `ambassador.venues.list` | Every venue you claimed or submitted, with its pipeline status |
| `ambassador.earnings.wallet` | Balances and the ledger of commissions and payouts |
| `ambassador.earnings.request_payout` | Request a payout of everything withdrawable |

### Advertiser

| Tool | What it does |
|---|---|
| `advertiser.account.limits` | Spending limits, approval rules, whether a card is saved |
| `advertiser.venues.search` | Find screens by city, venue type, price and distance |
| `advertiser.venues.get` | One venue's details, price and booked dates |
| `advertiser.bookings.quote` | Price a set of screens and dates |
| `advertiser.artwork.upload` | Upload artwork, converted to the six-colour e-paper screen, with a preview |
| `advertiser.bookings.create` | Book a quote with an uploaded artwork, within your spending limits |
| `advertiser.bookings.pay` | Pay with the saved card or get a payment link |
| `advertiser.bookings.get` | One booking and its next step |
| `advertiser.bookings.list` | Your bookings |
| `advertiser.bookings.update` | Swap a booking's artwork or rename the campaign |
| `advertiser.bookings.cancel` | Cancel an unpaid booking, or ask staff to cancel and refund a paid one |
| `advertiser.bookings.report` | Days each screen confirmed showing the advert, with estimated views |
| `advertiser.bookings.approve_sandbox` | Sandbox only: stand in for the account holder's approval |

### Venue (host)

| Tool | What it does |
|---|---|
| `host.venue.overview` | Your screens, adverts now and coming up, earnings, pending applications |
| `host.venue.apply` | Apply for free screens at a venue |
| `host.screens.report_advert` | Report an advert showing on your screen |
| `host.screens.set_wifi` | Stage new WiFi details for a screen |
| `host.screens.clear_wifi` | Cancel staged WiFi |
| `host.earnings.wallet` | What the venue has earned and can withdraw |
| `host.earnings.withdraw` | Withdraw the venue's earnings |

## Example prompts

- "Join the Wall Marketing outreach team, I work around Bairro Alto in Lisbon. Which venues should I approach first?"
- "Find Wall Marketing screens in hostels in Bangkok and quote two weeks from next Monday."
- "Book the three cheapest London screens for May with this artwork: https://example.com/poster.png"
- "How much has my café earned from its screen this month?"

## Support

- Questions: hello@wall.marketing
- Security: https://www.wall.marketing/.well-known/security.txt

The contents of this repository are MIT licensed. Use of the service is subject to the terms at https://www.wall.marketing/policies.
