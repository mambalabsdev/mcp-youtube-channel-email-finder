# YouTube Channel Email Finder MCP Server

[![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-youtube-channel-email-finder)](https://www.npmjs.com/package/@mambalabsdev/mcp-youtube-channel-email-finder) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-youtube-channel-email-finder)](https://github.com/mambalabsdev/mcp-youtube-channel-email-finder/blob/main/LICENSE)

An MCP server for the Mamba Labs YouTube Channel Email Finder actor on Apify. Find the email addresses YouTube channels publish, with the source of each.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

Give channels, or a search term with a subscriber range. For each channel you get its stats and any address it publishes in plain text on its about page or linked website, with the page that shows it.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-youtube-channel-email-finder": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-youtube-channel-email-finder"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `find_youtube_channel_emails` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "Find the published business email for @mkbhd."
- "Find home espresso channels with 10,000 to 500,000 subscribers and their published emails."
- "Which of these YouTube channels publish a contact address?"

## Tool

`find_youtube_channel_emails`. One tool. Example arguments:

```json
{
  "channels": [
    "@mkbhd"
  ]
}
```

## Inputs

Every buyer facing input of the actor. Omitted inputs take the actor's own defaults.

| Input | Type | Required | Description |
|---|---|---|---|
| `channels` | array | no | Channel URLs, @handles, or UC channel IDs, up to 500 a run. Clay users: wrap a column in a one item list. |
| `search_terms` | array | no | Optional. Themes to find channels by, such as home espresso. Search results come from YouTube's channel search, up to the maximum per search below. |
| `max_channels_per_search` | number | no | Number as text, 1 to 200. Default 20. |
| `min_subscribers` | number | no | Optional. Number as text. YouTube rounds subscriber counts, so this filter is approximate. |
| `max_subscribers` | number | no | Optional. Number as text. YouTube rounds subscriber counts, so this filter is approximate. |
| `check_websites` | boolean | no | no (default) or yes. yes reads the home page and one contact or about page on a site the channel links to, obeying robots.txt. It finds more addresses and costs more pages per run. |
| `videos_to_check` | number | no | Number as text, 0 to 10. Default 0, which is off. YouTube answered most video page reads with a sign in gate in testing, so this finds little and takes longer. Read only when no address has been found yet. |
| `check_all_sources` | boolean | no | no (default) stops at the first source with an address. yes reads them all, which takes longer. |
| `max_charge_usd` | string | no | Optional. The run stops before a charge would pass this amount. |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `channel-email`, one channel with a published email address found | $0.025 | $0.02375 | $0.0225 | $0.02125 |
| `apify-actor-start`, per run start | $0.01 | $0.01 | $0.01 | $0.01 |

A channel with no published address, a refused page, and refused input are free. Mamba Labs pays the platform costs of the run, Apify proxy traffic included.

## Full actor documentation

[apify.com/mambalabs/youtube-channel-email-finder](https://apify.com/mambalabs/youtube-channel-email-finder)

## License

MIT. See [LICENSE](LICENSE).
