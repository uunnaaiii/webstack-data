# Find broken and redirected URLs in your sitemap

Your sitemap tells Google which pages to crawl. If it lists pages that return 404 or redirect somewhere else, you waste crawl budget and send mixed signals. This check takes about a minute.

## What we found on a real site

We ran the check on the first 600 URLs of shopify.com's sitemap on 8 November 2026. 571 returned 200, 11 returned 404, 2 returned 410, 1 redirected (301), and 15 did not answer in time. Even large, well-run sites have a few dead URLs in their sitemaps.

## 1. Run the check

Open the [Sitemap URL Extractor](https://apify.com/uianalize/sitemap-url-extractor) and use:

```json
{
  "startUrls": ["yoursite.com"],
  "checkStatusCodes": true
}
```

The Actor finds your sitemaps on its own: it reads `robots.txt`, then tries `/sitemap.xml`, `/sitemap_index.xml` and `/wp-sitemap.xml`. It follows sitemap indexes and reads `.xml.gz` files.

## 2. Read the result

Each URL gets a `statusCode`, a `redirectTo` (when it redirects) and a `responseTimeMs`. In the dataset view, sort by `statusCode`:

- **404 / 410:** remove the URL from the sitemap, or restore the page.
- **301 / 302:** replace the URL with its final destination (`redirectTo`).
- **No status (timeout):** run the check again. If it keeps failing, the page is slow or blocks bots.

The `site-summary` row shows how many sitemaps were read and lists any sitemap file that failed to load.

## 3. Cost

$0.0006 per URL with the status check, so a 1,000-page site costs $0.60. Without the status check (URL list only) it is $0.0003 per URL.

## 4. Bonus: watch a competitor's new pages

Set `modifiedSince` to a date and the Actor only returns pages added or changed since then. The n8n template [competitor-new-pages-weekly-email.json](../templates/n8n/competitor-new-pages-weekly-email.json) does this every Monday and emails you the list.
