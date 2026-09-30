---
name: find-local-businesses
description: Find local businesses in any city with phones, websites, addresses and ratings from Google Maps, Yellow Pages (US, Canada, Australia) and Yelp. Use for B2B lead lists, sales prospecting and local market research.
---

# Find local businesses

This skill searches business directories for a category in one or more cities and returns a clean table of businesses.

The searches run as Apify Actors through this plugin's MCP server. Every run is billed to the user's own Apify account, so keep each run to a sensible size.

## Pick the tool

| Market | Directory | Tool name ends with |
| --- | --- | --- |
| Any country | Google Maps | `google-maps-data-scraper` |
| United States | YellowPages.com | `yellowpages-usa-business-lead-scraper` |
| Canada | YellowPages.ca | `yellowpages-ca-business-data-scraper` |
| Australia | YellowPages.com.au | `yellowpages-australia-lead-generator` |
| US, Canada, Australia, UK and many other countries | Yelp | `yelp-advanced-business-scraper-pay-per-result` |

- **Google Maps:** the default for "businesses of type X in city Y". It works in any country and usually has the widest coverage.
- **Yellow Pages:** use it in the US, Canada and Australia, especially for trades and services. In the US and Australia it can also return email addresses.
- **Yelp:** use it when the user cares about reviews, price level or opening hours, especially for restaurants and consumer services.
- **Combined:** Google Maps plus Yellow Pages, merged, gives the most complete list in the US, Canada and Australia. Suggest this when the user wants maximum coverage.

## Before running

1. Confirm three things:
   - the category, for example "plumbers";
   - the city or cities;
   - the country.
2. Estimate the size: keywords × locations × results per search.
   - Tell the user the estimate.
   - For more than about 200 results, or for several cities, ask the user to confirm before you run.
3. If the user gave no size:
   - start with one or two result pages (20–40 results) for each keyword and city;
   - show the results;
   - offer to fetch more.

## Inputs

Send every field shown below. If you leave a field out, some of these Actors fall back to example values, which adds unrelated results and cost.

**Google Maps.** One result page holds about 20 places:

```json
{"keywords": ["plumbers"], "location": "Austin, TX", "maxCrawlPages": 2, "language": "English (United States)", "urls": []}
```

- `maxCrawlPages` applies to each keyword separately. For example, 3 keywords × 10 pages is up to about 600 places.
- Put the area in `location` only, not in the keyword. A specific city works better than a broad region, and results stay inside that location's real boundary.
- `language` sets the language of the returned names, categories and addresses. Examples: `Deutsch (Deutschland)`, `Français (France)`, `Español (España)`, `日本語`.
- The user may already have a Google Maps search or place open in a browser. To scrape it, put its URL in `urls` and keep `keywords` empty:

  ```json
  {"keywords": [], "urls": ["https://www.google.com/maps/search/..."], "maxCrawlPages": 2}
  ```

**YellowPages USA.** One page holds about 30 businesses, and `maxPages` applies to each keyword. Keep `urls` empty when you search by keyword:

```json
{"searchKeyword": ["plumbers"], "location": "Austin, TX", "sort": "Default", "maxPages": 1, "urls": []}
```

- `sort` accepts `Default`, `Distance`, `Rating` or `Name`.
- The user may have already filtered YellowPages.com results in a browser. To scrape those result pages, put their URLs in `urls` and keep `searchKeyword` empty:

  ```json
  {"searchKeyword": [], "urls": ["https://www.yellowpages.com/..."], "maxPages": 1}
  ```

**YellowPages Canada.** All four fields are required:

```json
{"searchKeyword": ["dentists"], "location": "Toronto ON", "sortBy": "Relevance", "maxPages": 1}
```

`sortBy` accepts `Relevance`, `Closest`, `Highest Rated`, `Most Reviewed`, `Alphabetical` or `Recently Reviewed`.

**YellowPages Australia.** `max_items` is the number of businesses returned for each keyword:

```json
{"searchKeyword": ["electricians"], "location": "Brisbane City, QLD 4000", "sortBy": "Default", "openNow": false, "localBusiness": false, "popular": false, "max_items": 50}
```

`sortBy` accepts `Default`, `Distance`, `Rating` or `Name`.

**Yelp.**

```json
{"keywords": ["coffee"], "locations": ["Seattle, WA"], "maxResults": 50, "sort": "Recommended", "languages": "English (United States)", "include_ads": true, "urls": []}
```

- `maxResults` applies to each keyword and location pair. Yelp shows at most 240 results per search.
- `sort` accepts `Recommended`, `Highest Rated` or `Most Reviewed`.
- `languages` selects which country's Yelp site to search. Examples: `English (Canada)`, `English (Australia)`, `English (United Kingdom)`, `Français (France)`.
- Set `include_ads` to `false` to leave out sponsored listings.

## Get the results

- Each tool starts a run and waits for it.
- If the run is still going when the call returns, check on it with `get-actor-run`. Once it has finished, read the output with `get-dataset-items`.
- In `get-dataset-items`, use `fields` to request only the columns you need. Use `limit` and `offset` to page through large results.
- Don't paste raw JSON into the chat.

## Normalize

Field names differ by source. Map them into one table, and check the keys of the first item, because sources can add fields over time.

| Column | Google Maps | YellowPages USA | YellowPages Canada | YellowPages Australia | Yelp |
| --- | --- | --- | --- | --- | --- |
| name | `title` | `title` | `name` | `name` | `name` |
| phone | `phone` | `phone` | `phones` | `phone_number` | `phone_number` |
| website | `website` | `website` | `website` | `website_url` | `website` |
| email | — | `email` | — | `email` | — |
| address | `full_address` | `address` | `address` | `address` | `full_address` |
| rating | `rating` | `star_rating` | `average` | `rating` | `rating` |
| review count | `review_count` | `rating_count` | `total_ratings` | `review_count` | `review_count` |
| categories | `categories` | `categories` | — | `categories` | `categories` |
| listing URL | `url` | `source_url` | `source_url` | `url` | `url` |

Google Maps also returns `city`, `state`, `country`, `latitude`, `longitude`, `place_id`, `claimed`, `price_range` and `permanently_closed`. Leave out places that are marked permanently closed.

- **Duplicates:** remove them by phone number (digits only), then by website domain.
- **Source:** keep a `source` column so the user knows where each row came from.
- **Presenting:**
  1. Start with a short summary: how many businesses were found, and how many have a phone, a website and an email.
  2. Then show the table.
  3. Offer a CSV file.

## Notes

- These are public business listings. If the user plans outreach, remind them once to follow the local rules for commercial email and calls, such as CAN-SPAM (US), CASL (Canada) or the Spam Act (Australia).
- To add emails and social profiles from the businesses' own websites, use the `enrich-leads-with-contacts` skill.
