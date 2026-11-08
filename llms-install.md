# Installing the Censible MCP server

Instructions for an AI agent setting up Censible for a user.

Censible is a hosted, remote MCP server (Streamable HTTP) at:

```
https://api.censible.com.au/mcp
```

There is nothing to install, clone or build, and **no API key**. Don't ask the user for one. Sign-in is OAuth 2.1:
the server answers an unauthenticated request with `401` and a `WWW-Authenticate` header pointing to its metadata,
and the client registers itself and opens a browser for the user to sign in and allow access.

## Steps

1. Add the server to the MCP settings file (for Cline, `cline_mcp_settings.json`), keeping any servers already there:

   ```json
   {
     "mcpServers": {
       "censible": {
         "type": "streamableHttp",
         "url": "https://api.censible.com.au/mcp"
       }
     }
   }
   ```

2. Tell the user: "A browser window will open for Censible. Sign in, or create a free account, then choose
   **Allow**." In Cline, they may need to choose **Authenticate** beside censible in the MCP Servers panel.

3. If the client can't do OAuth to a remote server, use the `mcp-remote` bridge instead (it needs Node.js 18 or
   later), and it opens the same sign-in page:

   ```json
   {
     "mcpServers": {
       "censible": {
         "command": "npx",
         "args": ["-y", "mcp-remote", "https://api.censible.com.au/mcp"]
       }
     }
   }
   ```

4. Check it works: call `search_places` with `{"query": "Parramatta"}`. A list of places with `region_id`s (such as
   `AU_2026_SAL_...`) means it's connected. Then `get_place_figures` with one of those ids returns its headline
   figures.

## If something goes wrong

- **401 after signing in:** the sign-in didn't finish. Remove the server's saved credentials (in Cline, reconnect the
  server) and sign in again.
- **A tool says the plan doesn't include something:** that's expected on the Free plan (for example `rank_places`,
  earlier censuses for most measures, projections). Pass on the message; upgrades are at
  https://censible.com.au/pricing.
- **Anything else:** hello@censible.com.au.

## Using it well

- Find ids first: `search_places` for places, `search_metrics` for measures. Many names exist in several states
  (Richmond is a suburb in VIC, NSW, SA, QLD and TAS), so check the state.
- Leave `metric_ids` out of `get_place_figures` for the headline figures.
- Prefer `abs_value` where a figure has one: it's ABS's own.
- Say projections (2026 to 2041) are projections, not census results.
