# Webstack Data

Ready-to-use web data tools, templates and tutorials built on [Apify](https://apify.com/uianalize).

Our Actors run in the cloud, scale from one website to thousands, export to CSV/Excel/JSON, and plug into n8n, Make, Zapier, Google Sheets or your own code. You pay per result. Failed sites are free.

## Actors

| Actor | What it does | Price |
|---|---|---|
| [Broken Link Checker](https://apify.com/uianalize/broken-link-checker) | Crawls a website and lists every broken link (404, 5xx, timeouts, DNS/SSL errors) with the page where it appears and its anchor text. | $0.01 per run + $1.50 per 1,000 pages crawled |
| [SEO Audit Crawler](https://apify.com/uianalize/seo-audit-crawler) | Audits every page of a website for on-page SEO: titles, meta descriptions, H1, canonical, noindex, alt text, thin content, Open Graph, structured data and duplicates, with a site score out of 100. | $1.50 per 1,000 pages audited |
| [Tech Stack Detector](https://apify.com/uianalize/tech-stack-detector) | Detects the CMS, e-commerce platform, analytics, ad pixels, chat, payments, CDN and hosting of any list of websites. | $0.01 per run + $1.50 per 1,000 sites analysed |

## Templates

- [n8n: weekly broken-link report to Google Sheets](templates/n8n/broken-links-weekly-to-google-sheets.json)
- [n8n: enrich a Google Sheet of domains with their tech stack](templates/n8n/tech-stack-enrich-google-sheet.json)

## Tutorials

- [Find broken links on your website every week, automatically](tutorials/weekly-broken-link-report.md)
- [Qualify leads by the technology their website uses](tutorials/qualify-leads-by-tech-stack.md)

## Call the Actors from code

See [examples/](examples/) for cURL, Python and JavaScript snippets.

## Support

Open an issue on the Actor page in Apify Store or in this repository.
