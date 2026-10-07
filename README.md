# Zebu Data plugins and MCP servers

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

## MCP servers for any AI client

The same scrapers are also available as ready-made MCP server bundles. They are listed in the [official MCP Registry](https://registry.modelcontextprotocol.io/) under `io.github.zebudata`.

Add a bundle URL to any MCP client that supports remote (streamable HTTP) servers, such as Claude, Cursor or VS Code. The first time a tool runs, you sign in to Apify. Usage is billed to your own Apify account.

### Local Business Leads

`io.github.zebudata/local-business-leads`: Find local businesses on Google Maps, Yellow Pages and Yelp, then pull emails and phones from sites.

```
https://mcp.apify.com/?tools=delicious_zebu/google-maps-data-scraper,delicious_zebu/yellowpages-usa-business-lead-scraper,delicious_zebu/yellowpages-ca-business-data-scraper,delicious_zebu/yellowpages-australia-lead-generator,delicious_zebu/yelp-advanced-business-scraper-pay-per-result,delicious_zebu/contact-info-scraper,delicious_zebu/contact-info-scraper-pay-per-result
```

### Customer Reviews

`io.github.zebudata/customer-reviews`: Reviews from Google Maps, Yelp, TripAdvisor, eBay, Naver and Coupang, with ratings and dates.

```
https://mcp.apify.com/?tools=delicious_zebu/google-maps-store-review-scraper,delicious_zebu/yelp-reviews-scraper,delicious_zebu/tripadvisor-review-collector,delicious_zebu/ebay-product-reviews-scraper-with-advanced-filters,delicious_zebu/naver-shopping-reviews-scraper,delicious_zebu/coupang-reviews-scraper
```

### Amazon & eBay Product Data

`io.github.zebudata/ecommerce-product-data`: Amazon and eBay search results, product details, prices, variants and seller reviews.

```
https://mcp.apify.com/?tools=delicious_zebu/amazon-product-data-scraper,delicious_zebu/amazon-product-details-scraper,delicious_zebu/ebay-product-listing-scraper,delicious_zebu/ebay-product-details-scraper,delicious_zebu/ebay-product-reviews-scraper-with-advanced-filters
```

### Naver & Coupang Korea Data

`io.github.zebudata/korea-commerce-data`: Korean data from Naver Search, Shopping and Map plus Coupang: products, prices, reviews, places.

```
https://mcp.apify.com/?tools=delicious_zebu/naver-shopping-product-scraper,delicious_zebu/naver-product-detail-scraper,delicious_zebu/naver-shopping-reviews-scraper,delicious_zebu/naver-map-search-results-scraper,delicious_zebu/naver-search-scraper,delicious_zebu/coupang-category-products-scraper,delicious_zebu/coupang-reviews-scraper
```

### YouTube Data & Transcripts

`io.github.zebudata/youtube-data`: YouTube search, whole channels, video stats, comments and full transcripts with timestamps.

```
https://mcp.apify.com/?tools=delicious_zebu/youtube-video-scraper-by-keyword,delicious_zebu/youtube-channel-video-scraper,delicious_zebu/youtube-video-data-scraper,delicious_zebu/youtube-comments-replies-scraper,delicious_zebu/youtube-transcript-scraper
```

### X (Twitter), YouTube & TikTok Data

`io.github.zebudata/social-video-data`: X (Twitter) search, profiles and trends, YouTube search, video stats and comments, TikTok comments.

```
https://mcp.apify.com/?tools=delicious_zebu/ultimate-x-twitter-advanced-search-scraper,delicious_zebu/advanced-x-twitter-profile-scraper,delicious_zebu/x-global-trending-scraper,delicious_zebu/youtube-video-scraper-by-keyword,delicious_zebu/youtube-video-data-scraper,delicious_zebu/youtube-comments-replies-scraper,delicious_zebu/tiktok-video-comment-scraper
```

### Zillow Real Estate Data

`io.github.zebudata/real-estate-data`: Zillow listings and property details: price, Zestimate, rent estimate, history, schools, agents.

```
https://mcp.apify.com/?tools=delicious_zebu/zillow-property-data-scraper,delicious_zebu/zillow-property-details-scraper
```

Example for Claude Code:

```
claude mcp add --transport http zebu-local-leads "https://mcp.apify.com/?tools=delicious_zebu/google-maps-data-scraper,delicious_zebu/yellowpages-usa-business-lead-scraper,delicious_zebu/yellowpages-ca-business-data-scraper,delicious_zebu/yellowpages-australia-lead-generator,delicious_zebu/yelp-advanced-business-scraper-pay-per-result,delicious_zebu/contact-info-scraper,delicious_zebu/contact-info-scraper-pay-per-result"
```

## Privacy and license

- Privacy: [PRIVACY.md](PRIVACY.md)
- License: [MIT](LICENSE)

More Zebu Data scrapers are listed at https://apify.com/delicious_zebu?utm_source=github&utm_medium=claude-plugin&utm_campaign=repo
