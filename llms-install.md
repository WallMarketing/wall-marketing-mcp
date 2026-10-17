# Installing the Wall Marketing MCP server (for Cline and other agents)

This is a hosted remote server. There is nothing to clone, build or install, and no API key to put in the config.

1. Add this entry to `cline_mcp_settings.json` (merge it into any existing `mcpServers`):

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

2. Save. Cline connects and the server answers 401 with an OAuth `WWW-Authenticate` header pointing at `https://www.wall.marketing/.well-known/oauth-protected-resource/mcp`. Cline then opens the sign-in page in the browser.
3. Ask the user to sign in with their email address (they get a one-time code), choose a role (advertiser, venue or outreach team) and approve. To try it without an account, they choose **Sign in with a sandbox key instead** and paste a `wm_test_` key from https://www.wall.marketing/campaigns; the sandbox uses made-up data.
4. Check it works by calling `advertiser.venues.search` (advertiser) or `ambassador.account.me` (outreach team).

If the client cannot do OAuth, use an API key header instead (advertiser role only):

```json
{
  "mcpServers": {
    "wall-marketing": {
      "type": "streamableHttp",
      "url": "https://www.wall.marketing/mcp",
      "headers": { "Authorization": "Bearer wm_live_or_wm_test_key" }
    }
  }
}
```

Keys are made in the API section of https://www.wall.marketing/campaigns. Full docs: https://www.wall.marketing/developers
