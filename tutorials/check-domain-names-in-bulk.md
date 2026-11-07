# Check 100 domain name ideas in one minute (and watch your own domains expire)

Naming a product or a client project usually means typing names into a registrar one by one. The [Domain Availability Checker](https://apify.com/uianalize/domain-availability-checker) does the whole list at once and tells you, for each domain, whether it is **available** or **registered**. For registered domains it also gives the **registrar, creation date and expiry date**.

The data comes from the official registries: RDAP (the modern WHOIS) where it exists, the registry WHOIS server for extensions such as .io, .de, .co, .it or .me, and a live DNS cross-check.

## 1. Brainstorm: names × extensions

Open the Actor, fill in **Name ideas** and **TLDs**, and turn on **Only output available domains**:

```json
{
  "names": ["brightmeadow", "quietharbor", "tinyorbit", "northlane"],
  "tlds": ["com", "io", "ai", "co", "app"],
  "onlyAvailable": true
}
```

That is 20 combinations. Each one costs $0.0015, so the run costs about $0.03. You get a table you can export to CSV or Excel.

## 2. Due diligence on a list of domains

Paste full domains or URLs into **Domains to check**. For each registered domain you get:

| Field | Example |
|---|---|
| `registrar` | MarkMonitor Inc. |
| `createdAt` | 1997-09-15T04:00:00Z |
| `expiresAt` | 2028-09-14T04:00:00Z |
| `daysUntilExpiry` | 678 |
| `nameservers` | ns1.google.com, ns2.google.com |

This helps you see how old a domain is, where it is registered and whether it is about to expire.

## 3. Get an email before your own domains expire

Import the n8n template [domain-expiry-watch-email.json](../templates/n8n/domain-expiry-watch-email.json). Every Monday it checks your domains and emails you any domain that expires within 45 days, or that is no longer registered. With 20 domains it costs about $0.13 a month.

## Status values, honestly

- `available`: the registry has no record and the name has no DNS delegation.
- `registered`: the registry or live DNS shows the domain is taken (subdomains such as `maps.google.com` also show as taken).
- `likely-available`: the registry does not answer public lookups (for example .es and .ch). No DNS delegation was found, so confirm at your registrar.
- `unknown`: the registry did not answer after retries. These are not charged.

Registries do not publish premium or reserved names, so a few "available" domains may carry a premium price. Always confirm at your registrar before you rely on the result.
