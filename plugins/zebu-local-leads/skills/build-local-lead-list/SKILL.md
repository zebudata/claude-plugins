---
name: build-local-lead-list
description: Build a local B2B lead list end to end - find businesses by category and city on Google Maps, Yellow Pages and Yelp, remove duplicates, add emails from their websites, and deliver a CSV. Use when the user wants a complete prospect list.
---

# Build a local lead list

This skill runs the full workflow and delivers one CSV. It combines the `find-local-businesses` and `enrich-leads-with-contacts` skills.

## 1. Scope

Ask only for what is missing:

- **Category:** the category or keywords.
- **Place:** the cities and the country.
- **Size:** the target number of leads.
- **Must-have fields:** for example email, website or phone.
- **Sources:** Google Maps, Yellow Pages, Yelp, or a mix. By default, use Google Maps. In the US, Canada and Australia, add Yellow Pages when the user wants maximum coverage or more emails.

Then give a size and cost estimate before you start. Every run is billed to the user's own Apify account, so get a clear yes before any run that is expected to:

- return more than about 200 businesses, or
- crawl more than about 100 websites.

## 2. Find

Follow `find-local-businesses`:

- Use one run per source. Where a tool accepts lists, put all keywords and cities in that run.
- Map the results to these columns: `name`, `phone`, `website`, `email`, `address`, `city`, `rating`, `review_count`, `categories`, `source`, `listing_url`.

## 3. Deduplicate

- **Matching:** treat two rows as the same business if they match on phone number (digits only). If not, compare website domain, then name plus street address.
- **Keeping:** when rows match, keep the most complete one, and record all of its sources in `source`, for example `googlemaps+yellowpages`.

## 4. Enrich

1. Collect the unique website domains of rows that still have no email. If the user wants every channel, collect every row that has a website.
2. Run `enrich-leads-with-contacts` on those domains. If the list is large, start with a batch of 20.
3. Merge the results by domain:
   - fill `email` with the best deliverable address;
   - add `all_emails`, `linkedin`, `facebook` and `instagram`.

## 5. Deliver

**Columns:** `name`, `phone`, `email`, `all_emails`, `website`, `address`, `city`, `rating`, `review_count`, `categories`, `linkedin`, `facebook`, `instagram`, `source`, `listing_url`.

**Format:**

- Save the list as a CSV file if you can create files.
- Otherwise, put the CSV in a code block, and split it if it is long.

**Summary:**

- the total number of unique businesses;
- coverage: the percentage with a phone, a website and an email;
- the number of duplicates removed from each source.

**Useful segments:** point these out when they are relevant. Examples:

- "23 businesses have no website, so they are prospects for web design services."
- Businesses with high ratings but few reviews.

## Guardrails

- Never start a large or multi-city run without the user's go-ahead.
- Never invent contact details. Leave missing fields empty.
- Before the user contacts any leads, remind them once to follow the applicable outreach and privacy laws.
