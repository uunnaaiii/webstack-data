# Qualify leads by the technology their website uses

If you sell to Shopify stores, WordPress agencies' clients, HubSpot users or companies that already pay for Stripe, the website tells you whether a lead is a fit. This tutorial adds a technology column to any list of domains so you can filter before you reach out.

## 1. Run it on a list of domains

1. Open [Tech Stack Detector](https://apify.com/uianalize/tech-stack-detector) and click **Try for free**.
2. Paste your domains, one per line (up to thousands).
3. Click **Start**.

Each row contains the site, its HTTP status and the technologies grouped by category:

```json
{
  "input": "example-shop.com",
  "technologyCount": 7,
  "categories": {
    "E-commerce": ["Shopify"],
    "Analytics": ["Google Analytics"],
    "Advertising": ["Meta Pixel"],
    "CDN": ["Cloudflare"]
  }
}
```

It detects about 130 technologies in more than 30 categories: CMS, e-commerce, analytics, tag managers, ad pixels, marketing automation, live chat, payments, cookie consent, CDN, hosting and web servers. Sites that cannot be reached are reported but not charged.

## 2. Filter your leads

Typical filters:

- **E-commerce agencies:** `categories.E-commerce` contains `WooCommerce` or `Magento`, which are migration candidates.
- **Ad and tracking consultants:** sites with `Meta Pixel` but no `Cookie consent` tool.
- **Payments and fintech:** sites that already use `Stripe`, `PayPal` or `Klarna`.
- **Marketing automation:** sites without any `Email marketing` or `Marketing automation` technology.

Export the dataset to Excel or CSV and filter there, or call the API from your CRM.

## 3. Enrich a Google Sheet automatically with n8n

1. Import [tech-stack-enrich-google-sheet.json](../templates/n8n/tech-stack-enrich-google-sheet.json) into n8n.
2. Give the sheet the columns `domain, cms, ecommerce, analytics, advertising, technologies`.
3. Create an *HTTP Header Auth* credential with name `Authorization` and value `Bearer YOUR_APIFY_TOKEN`.
4. Pick the sheet in **Read domains** and **Update sheet**, then run it.

## What does it cost?

$0.01 per run plus $1.50 per 1,000 sites analysed. 1,000 leads cost about $1.51, and failed sites are free.

## Good to know

Detection uses public signals from the homepage only: HTML, script URLs, meta tags, response headers and cookie names. It does not log in, bypass protections or collect personal data. Results are indicative. Technologies that load only after user interaction may be missing.
