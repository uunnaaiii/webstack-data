# Calling Webstack Data Actors from code

Get an API token in Apify Console → Settings → API & Integrations. Keep it secret; the examples read it from the `APIFY_TOKEN` environment variable.

## cURL: check a site for broken links and get the results

```bash
curl -s -X POST "https://api.apify.com/v2/acts/uianalize~broken-link-checker/run-sync-get-dataset-items" \
  -H "Authorization: Bearer $APIFY_TOKEN" -H "Content-Type: application/json" \
  -d '{"startUrls":["example.com"],"maxPagesPerSite":50}'
```

## Python: tech stack of a list of domains

```python
import os
from apify_client import ApifyClient  # pip install apify-client

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("uianalize/tech-stack-detector").call(run_input={"urls": ["shopify.com", "wordpress.org"]})
for site in client.dataset(run["defaultDatasetId"]).iterate_items():
    print(site["input"], site["categories"])
```

## JavaScript (Node.js)

```js
import { ApifyClient } from 'apify-client'; // npm i apify-client

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor('uianalize/broken-link-checker').call({ startUrls: ['example.com'], maxPagesPerSite: 100 });
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.table(items.filter((i) => i.type === 'broken-link').map(({ brokenUrl, statusCode, foundOnPage }) => ({ brokenUrl, statusCode, foundOnPage })));
```

## Limit the cost of a run

Both Actors are pay-per-event. Pass `maxTotalChargeUsd` as a query parameter (for example `?maxTotalChargeUsd=1`) and the run stops when that amount is reached.
