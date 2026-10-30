# Meta Ads MCP by AdPlug, for Grok Bot and Cursor

AdPlug is a hosted MCP server that safely connects Meta Ads to Grok Bot and Cursor.

Your agent can check campaigns, flag what needs attention and, on a paid plan, make the changes you approve.

The plugin adds one remote MCP server, `https://api.adplug.app/mcp/meta-ads`, and nothing else. There's no code, no script and no hook in it.

## Install in Grok Bot

Send your Bot this message:

> Add a custom MCP server called AdPlug Meta Ads at https://api.adplug.app/mcp/meta-ads

Click **Authorize** on the card it posts, then **Continue**, then sign in to AdPlug in the browser tab that opens and click **Approve**. The approval screen says "Cursor wants to access your AdPlug account". That's expected: Grok Bot connects apps through Cursor.

## Install in Cursor

Add `https://api.adplug.app/mcp/meta-ads` as a server in Cursor's MCP settings, or put this in `.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "adplug-meta-ads": {
      "url": "https://api.adplug.app/mcp/meta-ads"
    }
  }
}
```

The first time you connect, a browser tab opens on AdPlug's sign-in. Sign in, or create a free account, and click **Approve**.

## What you need

- An AdPlug account. The free plan connects one ad platform, comes with a monthly request limit and is view only: your agent can read your accounts and preview changes, but not apply them. A paid plan lets the agent make changes: see [adplug.app/pricing](https://adplug.app/pricing).
- Meta Ads connected once in AdPlug, at [adplug.app/dashboard/connections](https://adplug.app/dashboard/connections), with your own Facebook sign-in.

There's no API key or client ID to set up. Sign-in is OAuth 2.1 with dynamic client registration and PKCE.

## What your agent can do

- **Reads:** your ad accounts, Facebook Pages and linked Instagram accounts, in one call. Account, campaign, ad set and ad performance, with breakdowns by age and gender, placement, device and country, and your choice of attribution window. Campaigns, ad sets, ads, audiences, catalogues, product sets and lead forms. A delivery check that says why an ad isn't running and what to fix. Targeting search for interests, locations, job titles and more, with an audience size estimate. Meta's public Ad Library, to look up a competitor's ads. Meta's [Ad Library API](https://www.facebook.com/ads/library/api) only returns a commercial ad if it was shown in the EU, and Meta asks you to confirm your identity once before your first search.
- **Changes:** create and edit campaigns, ad sets and ads. Pause, switch on, archive or delete them. Budgets, bids and spend caps. Custom audiences, lookalikes, catalogues, product sets, lead forms, automated rules, A/B tests and custom conversions. A new ad runs an existing creative or one of your Page's posts.

`adplug_get_status` tells the agent whether Meta Ads is connected and what your plan allows.

## Example prompts

- "Compare my Meta Ads campaigns last week against the week before. Flag the biggest movers in spend and cost per result, and tell me why they moved."
- "Which of my Meta ads should be running but aren't delivering, and what's blocking each one?"
- "Which ads are fatiguing, with frequency up and click-through rate down, and what should we test instead?"
- "Check my pixel is still firing and my conversions are still recording, and flag anything that stopped."

## How changes are kept safe

- Change tools come in pairs: a preview, which shows the exact change without making it, and an execute, which makes it. AdPlug's tool descriptions tell the agent to preview first and wait until you confirm. That's an instruction to the agent, not a block on the server.
- AdPlug's server creates every new campaign, ad set and ad paused, whatever the agent asks for.
- On the free plan, the change tools refuse to apply anything.
- On Max and Agency plans, a team owner can set a teammate to View only for Meta Ads. AdPlug then hides and blocks the change tools for that teammate.
- Grok Bot and Cursor can also ask you before a tool runs, depending on your settings.
- Every call is logged on the [usage page](https://adplug.app/dashboard/usage) of your AdPlug dashboard.

## Your data and where it goes

Every tool call goes to one endpoint, `https://api.adplug.app/mcp/meta-ads`. Sign-in goes through AdPlug's pages on adplug.app and its sign-in provider, Supabase (named in api.adplug.app's OAuth metadata). The plugin adds no software and runs no scripts on your computer.

Account data travels between Meta Ads and your agent through AdPlug's servers at api.adplug.app. Reports are fetched live and not kept. AdPlug logs each call's tool, ad account and time for your usage page, never its arguments or results. Facebook sign-in tokens are stored encrypted.

- Privacy policy: [adplug.app/privacy](https://adplug.app/privacy)
- Terms: [adplug.app/terms](https://adplug.app/terms)
- Data processing agreement: [adplug.app/dpa](https://adplug.app/dpa)

## Support and links

- Email [support@adplug.app](mailto:support@adplug.app) and Daniel Popa, AdPlug's founder, will reply, usually the same business day.
- Website: [adplug.app/guides/meta-ads](https://adplug.app/guides/meta-ads)
- Setup guide: [adplug.app/guides/meta-ads](https://adplug.app/guides/meta-ads)
- Every ad platform in one connector: [adplug-app/adplug-cursor-plugin](https://github.com/adplug-app/adplug-cursor-plugin)

## Licence

MIT, see [LICENSE](LICENSE). Published by AdPlug, the trading name of MEANDATA IT SRL.
