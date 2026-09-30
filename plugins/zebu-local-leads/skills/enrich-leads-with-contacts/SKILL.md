---
name: enrich-leads-with-contacts
description: Find emails, phone numbers and social media links on company websites, with free email deliverability checks. Use to enrich a lead list, CRM export or spreadsheet of website URLs, with one clean row per company.
---

# Enrich leads with contacts

This skill crawls each company's own website, including its contact, about and team pages. It returns one row per company with emails, phone numbers, social links and address.

It runs the `contact-info-scraper` Apify Actor through this plugin's MCP server. Usage is billed to the user's own Apify account, and cost grows with the number of pages crawled.

## Prepare the URLs

- Use one homepage URL per company, for example `https://example-plumbing.com`. Remove duplicates by domain.
- Skip URLs that are not the company's own site. Examples: facebook.com, instagram.com, yelp.com, yellowpages.com, Google Maps links and link-in-bio pages.
- Tell the user how many websites will be crawled.
- For more than about 100 sites, confirm with the user before running, and offer a first batch of 20.

## Input

```json
{
  "Urls": ["https://example-plumbing.com", "https://another-company.com"],
  "Depth": 1,
  "Total_num": 10,
  "output_mode": "summary_only",
  "verify_emails": true,
  "url_include_patterns": ["contact", "about", "team", "impressum"],
  "enrich_social_profiles": []
}
```

- **`output_mode`:** `"summary_only"` returns one deduplicated row per website, which is the format lead lists need.
- **`Total_num`:** caps the number of pages crawled in the whole run. Allow about 5 pages per website, so 5 × the number of URLs, up to 10,000.
- **`Depth`:** `1` crawls the homepage plus the linked pages that match `url_include_patterns`. That reaches most contact pages at low cost. If some sites return no email, run just those again with `Depth: 2`.
- **`enrich_social_profiles`:** leave it empty unless the user explicitly asks for follower counts or bios. That option runs additional scrapers, which are billed separately to the user's account.
- **`render_mode`:** keep the default, `auto`. It opens a browser only for pages that need JavaScript.

## Read the results

Each summary row includes:

- **Company:** `domain`, `company_name`
- **Email:** `primary_email`, `emails`, `email_count`
- **Phone:** `primary_phone`, `phone_numbers`
- **Address:** `address`, `city`, `region`, `postal_code`, `country`
- **Social profile links:** `linkedin`, `facebook`, `instagram`, `twitter`, `youtube`, `tiktok` and others
- **Email checks:**
  - `email_status` gives these flags for each email: `has_mx` (the domain accepts mail), `role` (a role mailbox such as info@), `free` (a free email provider) and `disposable`.
  - `deliverable_email_count`
- **Crawl size:** `pages_crawled`

Choosing an email:

- Prefer addresses with `has_mx: true` that are not disposable.
- Role mailboxes such as info@ or sales@ are normal for B2B outreach.
- Flag addresses on free email providers, because they may belong to an individual.

## Merge back

1. Join the results to the user's list by website domain. Add these columns: `email`, `all_emails`, `phone_from_site`, `linkedin`, `facebook` and `instagram`.
2. Report coverage, for example: "Found at least one deliverable email for 34 of 50 companies."
3. List the domains that failed or had no contacts, so the user can decide whether to retry them with `Depth: 2`.

## Notes

- Emails of named people are personal data.
  - Collect only what the user needs.
  - Before any outreach, remind the user to follow the applicable rules, such as GDPR, CAN-SPAM or CASL.
- Some sites block automated visits or show contact details only as images. Empty rows for those sites are expected.
