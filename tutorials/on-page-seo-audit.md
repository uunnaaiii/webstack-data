# Run a full on-page SEO audit of a website in 5 minutes

Most SEO problems that cost clicks are boring and fixable: missing meta descriptions, titles that get cut off in Google, pages with two H1s, images without alt text, pages accidentally set to noindex, duplicate titles across a whole section. This tutorial finds all of them on every page of a site and gives you a list to work through.

## 1. Audit a site from the browser

1. Open [SEO Audit Crawler](https://apify.com/uianalize/seo-audit-crawler) and click **Try for free**.
2. Enter your domain in **Websites**, for example `example.com`.
3. Set **Max pages per site** (50 is a good first run). Turn on **Only output pages with issues** if you only want the to-do list.
4. Click **Start**.

You get two views:

- **Pages**: one row per page with its issues (`TITLE_TOO_LONG`, `META_DESCRIPTION_MISSING`, `H1_MULTIPLE`, `IMAGES_WITHOUT_ALT`, `NOINDEX`, `DUPLICATE_TITLE`…), plus the title, lengths, word count and response time.
- **Site summary**: a score out of 100 and the most common issues, with how many pages each one affects.

As an example, a 20-page test run scored apify.com 96/100 and wordpress.org 87/100. The most common issue on wordpress.org was missing structured data.

## 2. Fix in the right order

1. `NOINDEX` and `HTTP_ERROR` first. These pages are invisible to Google or broken.
2. `CANONICAL_POINTS_ELSEWHERE` and `DUPLICATE_TITLE`. Google may pick the wrong page.
3. `TITLE_*` and `META_DESCRIPTION_*`. They are what people see in search results, so they drive clicks.
4. `H1_*`, `IMAGES_WITHOUT_ALT` and `THIN_CONTENT`. They are content quality and accessibility issues.
5. `OPEN_GRAPH_MISSING` and `NO_STRUCTURED_DATA`. They affect social previews and rich results.

## 3. Track it every month with n8n

Import [seo-audit-monthly-to-google-sheets.json](../templates/n8n/seo-audit-monthly-to-google-sheets.json) into n8n, add your Apify token as an *HTTP Header Auth* credential (`Authorization: Bearer YOUR_APIFY_TOKEN`), set your domain and pick a Google Sheet. On the 1st of each month you get a fresh list of pages with issues, so you can see the site improving.

For a complete technical check, run [Broken Link Checker](https://apify.com/uianalize/broken-link-checker) on the same site.

## What does it cost?

$1.50 per 1,000 pages audited, plus a near-zero start fee. A 200-page site costs about $0.30 per audit, and unreachable sites are free.

## Limits

It analyses the HTML the server returns. Content rendered only by JavaScript in the browser is not executed, so heavily client-rendered sites may show as thin content.
