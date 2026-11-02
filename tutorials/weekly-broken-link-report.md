# Find broken links on your website every week, automatically

Broken links hurt visitors, conversions and SEO, and they appear on their own: a partner moves a page, a product is discontinued, a blog post links to a source that disappears. This tutorial sets up a weekly check that finds them for you and drops them into a Google Sheet.

**You need:** an [Apify](https://apify.com) account (the free plan is enough to start) and, for the automated version, n8n or another automation tool.

## 1. Try it once in the browser

1. Open [Broken Link Checker](https://apify.com/uianalize/broken-link-checker) and click **Try for free**.
2. In **Websites**, enter your domain, for example `example.com`.
3. Leave **Max pages per site** at 50 for a first run, then click **Start**.

When it finishes, the **Broken links** tab shows one row per broken link:

| Broken URL | HTTP | Found on page | Anchor text |
|---|---|---|---|
| https://example.com/old-pricing | 404 | https://example.com/blog/launch | see our pricing |

Each site also gets a summary row with pages crawled, links checked and broken links found. Links whose server refuses automated checks (403, 429, LinkedIn's 999) are counted separately as *blocked* instead of being reported as broken. Turn on **Include links that block bots** if you want to review them as well.

Export the table as CSV, Excel or JSON from the **Export** button.

## 2. Run it every week

The simplest option is Apify's own scheduler. In Apify Console, open **Schedules → Create new**, choose the Actor and your input, and set it to weekly.

## 3. Send the results to Google Sheets with n8n

1. Download the template [broken-links-weekly-to-google-sheets.json](../templates/n8n/broken-links-weekly-to-google-sheets.json).
2. In n8n, go to **Workflows → Import from file**.
3. In the **Run Broken Link Checker** node, create an *HTTP Header Auth* credential with name `Authorization` and value `Bearer YOUR_APIFY_TOKEN`. Get your token in Apify Console under **Settings → API & Integrations**.
4. Put your domain in `startUrls` in the request body.
5. In **Append to Google Sheets**, choose your spreadsheet. The first row should contain: `site, brokenUrl, statusCode, error, isExternal, foundOnPage, anchorText, checkedAt`.
6. Activate the workflow.

Every Monday at 8:00 you get a fresh list of broken links in the sheet, with the page to fix next to each one.

## What does it cost?

The Actor charges $0.01 per run plus $1.50 per 1,000 pages crawled. Checking the links found on those pages is included. A weekly check of a 100-page site is about $0.16, or roughly $0.70 a month. The template caps every run at $2 with `maxTotalChargeUsd`.

## Tips

- Agencies can put many client sites in `startUrls`. Results are grouped by `site`.
- Set **Check external links** to off if you only care about your own pages.
- Run it after every deploy by calling the API from CI. See [examples](../examples/).
