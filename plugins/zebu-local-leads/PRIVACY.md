# Privacy Policy: Zebu Data Claude plugins

Last updated: 2026-09-30

This policy covers the Claude plugins in the repository https://github.com/zebudata/claude-plugins, including "Local Business Leads" (`zebu-local-leads`).

## What a plugin contains

Each plugin contains two things:

- text instructions (skills) for Claude;
- a reference to Apify's hosted MCP server (`https://mcp.apify.com`).

It contains no code that runs on your device.

## Where data goes

- **Between you and Claude.** Anthropic handles your requests and conversations under its own terms and privacy policy. Zebu Data does not receive them.
- **Between Claude and Apify.** When Claude uses a tool, it sends the tool's inputs to Apify's MCP server. Inputs are things like search keywords, locations or website URLs. Apify runs the requested Actor in your Apify account and returns the results to Claude. Apify's [privacy policy](https://apify.com/privacy-policy) and terms apply to this part.
- **Between the Actors and websites.** The Actors request publicly available pages from the source websites, such as Google Maps, Yellow Pages, Yelp or the websites you provide, and extract business information from them.

## What Zebu Data collects

The plugins do not collect or store any data, and they do not send any data to Zebu Data.

Zebu Data develops the Actors on Apify, so it may see aggregated usage statistics that Apify provides to developers, such as run counts and error rates. This is governed by Apify's terms.

## Retention

Run inputs and results are stored in your own Apify account. They are kept according to your Apify plan's data retention, and you can delete them at any time in the Apify Console.

## Age

These plugins are not intended for people under 18.

## Contact

If you have questions about this policy, open an issue at https://github.com/zebudata/claude-plugins/issues.
