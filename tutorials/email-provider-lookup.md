# Find which companies use Google Workspace or Microsoft 365

If you sell email security, deliverability services, Google Workspace or Microsoft 365 migrations, or a tool that only integrates with one of them, the first question about a lead is: which email provider do they use? That answer is public. It is in the domain's DNS (MX and SPF records), so you can check a whole list of domains in seconds without contacting anyone.

## 1. Run it on a list of domains

1. Open [Email Provider Checker](https://apify.com/uianalize/email-domain-checker) and click **Try for free**.
2. Paste domains, URLs or email addresses, one per line. `jane@acme.com` and `https://www.acme.com/about` are both reduced to `acme.com`.
3. Click **Start**.

Each row looks like this (example values):

```json
{
  "domain": "acme-example.com",
  "status": "ok",
  "canReceiveEmail": true,
  "emailProvider": "Microsoft 365",
  "emailProviderSource": "spf",
  "securityGateway": "Proofpoint",
  "spf": { "senders": ["Microsoft 365", "HubSpot", "SendGrid"], "allQualifier": "-all" },
  "dmarc": { "policy": "none" },
  "dkimSelectorsFound": ["selector1"],
  "mtaSts": false,
  "issues": ["DMARC_POLICY_NONE"],
  "securityScore": 65
}
```

- **emailProvider**: Google Workspace, Microsoft 365, Zoho Mail, Proton, iCloud, Fastmail, GoDaddy, IONOS, OVHcloud, Hostinger and more. When the MX points to a security gateway, the provider is inferred from SPF and `emailProviderSource` says `spf`.
- **securityGateway**: Mimecast, Proofpoint, Barracuda, Cisco, Sophos, Hornetsecurity and others.
- **spf.senders**: services allowed to send as the domain (HubSpot, Mailchimp, SendGrid, Salesforce, Zendesk...). A quick signal of their marketing and support stack.
- **dmarc.policy** and **issues**: missing SPF/DMARC, `p=none`, `+all`, more than 10 SPF lookups, no DKIM on common selectors.
- **securityScore**: a simple 0-100 score (SPF 30, DMARC 40 enforced or 15 with `p=none`, DKIM 20, MTA-STS 10).

## 2. Use cases

- **Segment leads** by provider before outreach: a Microsoft 365 migration pitch is wasted on a Google Workspace company.
- **Find deliverability prospects**: domains with `DMARC_MISSING` or `DMARC_POLICY_NONE` are exposed to spoofing and Gmail/Yahoo bulk-sender rules.
- **Clean a list**: `canReceiveEmail: false` (no MX or a null MX) means emails to that domain will bounce.
- **Audit your own domains** (or your clients') every month.

DKIM keys cannot be listed, so the Actor tries 19 common selectors; a domain can still have DKIM under an unusual selector. It only reads public DNS records and never sends email.

## 3. Automate it with n8n

Import [email-provider-enrich-google-sheet.json](../templates/n8n/email-provider-enrich-google-sheet.json) into n8n. It reads a Google Sheet with a `domain` column, calls the Actor and writes back provider, gateway, SPF senders, DMARC policy, score and issues.

## Cost

$1.50 per 1,000 domains checked (pay per result, no subscription). Domains that fail with a DNS error are not charged.
