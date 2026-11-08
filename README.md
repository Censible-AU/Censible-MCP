<p align="center"><img src="logo.png" width="96" height="96" alt="Censible"></p>

# Censible MCP server

The Australian Census for any place, as tools for your AI assistant. Ask Claude, ChatGPT, Cursor or any MCP client
about a suburb, postcode, council or region and it answers from the ABS Census (2011, 2016 and 2021), with
projections to 2041.

```
https://api.censible.com.au/mcp
```

A hosted, remote server (Streamable HTTP). There's nothing to install and no API key: the first time your assistant
connects, it opens a Censible page where you sign in (or sign up, free) and allow it.

## What you can ask

- "Which Melbourne suburbs are most like Brunswick, but with cheaper rent?"
- "Which Queensland suburbs have the highest median household income?"
- "How many people live within 3 km of Parramatta station, and how old are they?"
- "How have my saved areas changed since 2016?"

Behind the answers:

- **649 measures** across population, work, education, income and housing, curated from the ABS Census DataPacks.
- **Every standard place** on current (2026) boundaries: suburbs, postcodes, councils, state electorates, statistical
  areas (SA2 to SA4), capital cities and states, each with Australia to compare against.
- **ABS's own figures** wherever ABS publishes one, so counts and medians match QuickStats.
- **Areas worked out properly:** several places pooled, a circle around a point, or minutes' drive or walk from one.
  Counts are summed first and each measure's formula applied last, so shares and medians are right.
- **Projections** for 2026, 2031, 2036 and 2041, always labelled as projections.

## Connect

### Claude (web, desktop and mobile)

1. Open **Settings › Connectors** and choose **Add custom connector**.
2. Name it **Censible** and paste `https://api.censible.com.au/mcp`.
3. Choose **Connect**, then sign in and allow Claude.

### ChatGPT

1. Open **Settings › Apps & Connectors**. Under Advanced settings, turn on **Developer mode**.
2. Choose **Create**, name it **Censible**, paste `https://api.censible.com.au/mcp` and pick **OAuth**.
3. Sign in and allow ChatGPT.

### Claude Code

```sh
claude mcp add --transport http censible https://api.censible.com.au/mcp
```

Then type `/mcp` in Claude Code, choose censible, and sign in.

### Cursor

Add to `~/.cursor/mcp.json` (or your project's `.cursor/mcp.json`):

```json
{
  "mcpServers": {
    "censible": {
      "url": "https://api.censible.com.au/mcp"
    }
  }
}
```

Then in **Cursor Settings › MCP**, choose **Connect** beside censible and sign in.

### Cline

Add to `cline_mcp_settings.json` (MCP Servers › Configure):

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

Then choose **Authenticate** beside censible and sign in.

### VS Code (GitHub Copilot)

Add to `.vscode/mcp.json`:

```json
{
  "servers": {
    "censible": {
      "type": "http",
      "url": "https://api.censible.com.au/mcp"
    }
  }
}
```

### Other clients

Any client that supports remote MCP servers with OAuth works with the address above. For one that only runs local
servers, bridge it with [mcp-remote](https://www.npmjs.com/package/mcp-remote):

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

## Tools

| Tool | What it does | Plan |
|---|---|---|
| `search_places` | Find places by name, postcode or code, for their ids | Free |
| `places_at_point` | The suburb, postcode, council, electorate and regions containing a point | Free |
| `search_metrics` | Find measures by words or topic, for their ids | Free |
| `get_place_figures` | Figures for up to 20 places side by side | Free |
| `list_saved_areas` | Your saved areas (from the web app or `save_area`) | Free |
| `saved_area_figures` | Figures for one of your saved areas | Free |
| `save_area` | Save an area to your account, where the web app shows it too | Free |
| `rank_places` | The places with the highest or lowest value of a measure | Explore |
| `find_similar_places` | Places like one you know, or that meet criteria | Explore |
| `area_figures` | Figures for places pooled, a circle, a drawn shape, or a drive or walk time | Team |
| `list_site_sets` | Your site sets (your own locations, such as stores) | Team |
| `site_set_figures` | Each site's catchment figures | Team |
| `site_contrast` | What sets your best-performing sites apart from the rest | Network |

Every tool except `save_area` only reads.

## Plans

Every plan includes the MCP server, Free too, with a month's requests for your whole team.

- **Free:** the topics ABS publishes in QuickStats, for 2011, 2016 and 2021, for every suburb, postcode, council and
  statistical area from SA2 to state.
- **Explore:** all 649 measures for 2021, state electorates and SA1s, ranking and finding similar places.
- **Team:** 2011 and 2016 for every measure, catchments and custom areas, and your own sites, for a whole organisation.
- **Network:** projections to 2041, and your sites' performance.

What a plan doesn't include is left out of answers (or refused, when asked for by name), and your assistant is told
why. Prices and limits: [censible.com.au/pricing](https://censible.com.au/pricing).

## Privacy

Your assistant sees the census figures your plan has, plus your own saved areas and site sets, never anyone else's.
Disconnect it any time from **Use with AI** in the [Censible app](https://app.censible.com.au).

## About the data

Census figures are from the Australian Bureau of Statistics, Census of Population and Housing, 2011, 2016 and 2021,
under [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Censible curates them, carries them onto current
boundaries and adds projections and modelled figures; these are Censible's estimates, not ABS figures. The 2026 Census
results are due from 2027.

## Support

[hello@censible.com.au](mailto:hello@censible.com.au) · [censible.com.au](https://censible.com.au)

This repository holds the server's documentation and listing files. The server itself is hosted by Censible and its
code isn't published here. See [LICENSE](LICENSE).
