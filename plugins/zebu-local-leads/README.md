# Local Business Leads

Build local B2B lead lists inside Claude. Ask for a type of business in a city. Claude will:

1. Find matching businesses on Google Maps (any country), Yellow Pages (US, Canada and Australia) and Yelp.
2. Remove duplicates.
3. Visit each company's website to collect emails, phone numbers and social media links.
4. Deliver the results as a clean CSV.

Example requests:

- "Find 100 plumbers in Austin, TX with phone numbers and websites."
- "Build a lead list of dentists in Toronto and Vancouver, with emails."
- "List 200 cafés in Berlin with their websites and ratings."
- "Which electricians in Brisbane don't have a website?"
- "Here are 40 company websites. Find their contact emails and LinkedIn pages."

## What's included

| Skill | What it does |
| --- | --- |
| `find-local-businesses` | Searches Google Maps, Yellow Pages and Yelp by category and city, and puts the results into one table with the same columns. |
| `enrich-leads-with-contacts` | Crawls company websites for emails (with deliverability checks), phone numbers and social profile links. |
| `build-local-lead-list` | Runs the whole workflow: find, deduplicate and enrich. Delivers a CSV with a coverage summary. |

The skills use six scrapers ("Actors") that Zebu Data publishes on the Apify platform:

- [Google Maps Data Scraper](https://apify.com/delicious_zebu/google-maps-data-scraper?utm_source=github&utm_medium=claude-plugin&utm_campaign=local-leads)
- [YellowPages Scraper - USA Business Leads](https://apify.com/delicious_zebu/yellowpages-usa-business-lead-scraper?utm_source=github&utm_medium=claude-plugin&utm_campaign=local-leads)
- [YellowPages.ca Business Data Scraper](https://apify.com/delicious_zebu/yellowpages-ca-business-data-scraper?utm_source=github&utm_medium=claude-plugin&utm_campaign=local-leads)
- [YellowPages Australia Lead Generator](https://apify.com/delicious_zebu/yellowpages-australia-lead-generator?utm_source=github&utm_medium=claude-plugin&utm_campaign=local-leads)
- [Yelp Scraper - Business Leads, Phones & Websites](https://apify.com/delicious_zebu/yelp-advanced-business-scraper-pay-per-result?utm_source=github&utm_medium=claude-plugin&utm_campaign=local-leads)
- [Contact Info Scraper](https://apify.com/delicious_zebu/contact-info-scraper?utm_source=github&utm_medium=claude-plugin&utm_campaign=local-leads)

## How it works

The plugin contains two things:

- **Skills:** written instructions that tell Claude how to use the tools.
- **An MCP server entry:** it points to Apify's hosted MCP server at `https://mcp.apify.com` and is limited to the six Actors listed above.

It works like this:

- **First use:** the first time Claude uses one of the tools, you sign in to Apify. A free Apify account is enough to get started.
- **Each tool call:** Apify runs the Actor in your Apify account. The Actor loads public web pages from the directory sites, or from the websites you give it, and returns the extracted data to Claude.
- **What the plugin itself does:** it does not run code on your computer, and it sends data only to Apify's MCP server.

## Costs

The plugin is free. The Actors charge per result:

- **Who bills you:** Apify, which charges your own Apify account at the prices shown on each Actor's page.
- **Free credit:** Apify's free plan includes a monthly usage credit.
- **Staying in control:** the skills estimate the size of every run and ask you before large ones.

## Privacy and responsible use

See [PRIVACY.md](PRIVACY.md) for how data flows between Claude, Apify and the source websites.

The data comes from publicly available business listings and websites. You are responsible for how you use it. That includes following the terms of the source websites, and privacy and anti-spam laws such as GDPR, CAN-SPAM, CASL and Australia's Spam Act.

## Support

To report a problem or request a feature, open an issue at https://github.com/zebudata/claude-plugins/issues.

Zebu Data is an independent developer. This plugin is not affiliated with or endorsed by Google, Yelp, Yellow Pages, Apify or Anthropic. Their names appear only to describe the data sources and platforms the plugin works with.
