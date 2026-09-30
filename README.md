# Zebu Data plugins for Claude

These plugins let Claude collect structured web data. They work through scrapers ("Actors") that Zebu Data publishes on the Apify platform.

| Plugin | What it does |
| --- | --- |
| [Local Business Leads](plugins/zebu-local-leads) (`zebu-local-leads`) | Finds local businesses in any city on Google Maps, Yellow Pages and Yelp, removes duplicates, and adds emails, phone numbers and social links from each business's website. |

## Install in Claude Code

```
/plugin marketplace add zebudata/claude-plugins
/plugin install zebu-local-leads@zebu-data
```

The first time a tool runs, Claude asks you to sign in to Apify. Usage is billed to your own Apify account, and a free account is enough to get started. Each plugin's README explains what it runs, what it costs and where data goes.

## Privacy and license

- Privacy: [PRIVACY.md](PRIVACY.md)
- License: [MIT](LICENSE)

More Zebu Data scrapers are listed at https://apify.com/delicious_zebu?utm_source=github&utm_medium=claude-plugin&utm_campaign=repo
