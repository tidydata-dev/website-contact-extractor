# Website Contact Extractor — Python, Node.js & cURL examples

Find **emails, phone numbers (E.164) and social profiles** on any website — homepage plus contact, imprint and about pages — or **enrich a Google Maps dataset** in place. **$2 per 1,000 websites, only when contacts are found.**

Hosted on Apify: **[Website Contact Extractor](https://apify.com/tidydata/website-contact-extractor)**. These examples show how to call it from your code; the Actor runs in the cloud, no API key for the source site, no proxies to manage.

## Python

```bash
pip install apify-client
export APIFY_TOKEN=...   # free account at apify.com → Settings → API & Integrations
```

```python
import os
from apify_client import ApifyClient

client = ApifyClient(os.environ["APIFY_TOKEN"])
run = client.actor("tidydata/website-contact-extractor").call(run_input={
    "websites": [
        "https://www.louvre.fr",
        "apify.com"
    ],
    "maxPagesPerSite": 5
})
for item in client.dataset(run["defaultDatasetId"]).iterate_items():
    print({k: item.get(k) for k in ['domain', 'emails', 'phones', 'instagram']})
```

## Node.js

```javascript
import { ApifyClient } from 'apify-client';

const client = new ApifyClient({ token: process.env.APIFY_TOKEN });
const run = await client.actor('tidydata/website-contact-extractor').call({"websites": ["https://www.casalucio.es"]});
const { items } = await client.dataset(run.defaultDatasetId).listItems();
console.log(items.length, items[0]);
```

## cURL (one call, results as JSON)

```bash
curl -s -X POST "https://api.apify.com/v2/acts/tidydata~website-contact-extractor/run-sync-get-dataset-items?token=$APIFY_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"websites": ["https://www.casalucio.es"]}'
```

## Enrich Google Maps results

Pass your Google Maps run's dataset: `{"datasetIds": ["<DATASET_ID>"]}`. Every place keeps its fields and gets `contactEmails`, `contactPhones`, `facebook`, `instagram`, `linkedin`… — the same website is scanned once.

## More TidyData Actors

[YouTube Transcript](https://apify.com/tidydata/youtube-transcript-scraper) · [YouTube Comments](https://apify.com/tidydata/youtube-comments-scraper) · [YouTube Scraper](https://apify.com/tidydata/youtube-channel-scraper) · [Website Contacts](https://apify.com/tidydata/website-contact-extractor) · [Google News](https://apify.com/tidydata/google-news-scraper) · [App Reviews](https://apify.com/tidydata/app-reviews-scraper) · [Merge & Dedupe](https://apify.com/tidydata/merge-dedupe-datasets) · [all of them](https://github.com/tidydata-dev)

Examples are MIT-licensed.
