# Alibaba.com Product & Supplier Scraper [Just 💰$0.63]

Extract structured data from [alibaba.com](https://alibaba.com) — alibaba.com — product listings by keyword or supplier country with price range, minimum order and sold count. Review scores per product, supplier trade assurance and response rate, plus incremental mode that returns only new or changed products.

**[Alibaba.com Product & Supplier Scraper [Just 💰$0.63] on Apify →](https://apify.com/blackfalcondata/alibaba-com-scraper?fpr=1h3gvi)**

---

## 🚀 How to use this actor

> ### 💚 $5 free Apify credits — every month
> No credit card required. No commitment. Cancel anytime.

### 👉 [Sign up free on Apify →](https://console.apify.com/sign-up?fpr=1h3gvi)

1. **Click sign up** — pick GitHub, Google, or email; takes ~30 seconds
2. **Open this actor** — input is pre-filled with a working example
3. **Click Start** — export results as JSON, CSV, or Excel

Your **$5 monthly platform credit** is enough to run this actor right away — and again every month — scraping typically several hundred to several thousand results per run, depending on your input.

## Key features

**Search with filters** — Search by keyword and location. Filter by description format, and more.

**Incremental mode** — Only get new or changed products since your last run. Content hash per product — no duplicates, no re-processing.

**Change classification** — Track unchanged, expired, cross-run duplicate detection across runs. Build audit trails of how products evolve over time.

**Compact output** — Emit core fields only (AI-agent / MCP-friendly). Keeps response size small for LLM workflows.

**Result cap** — Stop after N products (up to 1.000). Set to 0 for the full catalog.

**Export anywhere** — Download as JSON, CSV, or Excel. Stream via Apify API, webhooks, or integrations with Make, Zapier, Airbyte, Keboola.

**Structured data** — Every product returns the same schema with consistent field naming. All fields always present — `null` when unavailable, never omitted.

---

## Use cases

**Data pipeline automation**
Integrate with your ETL pipeline to collect structured products from alibaba.com on a schedule. Export to CSV, JSON, or directly to your database. Use compact mode to control output size.

**Market research**
Monitor products, track trends, and analyze market dynamics with structured, deduplicated data from alibaba.com.

**Change monitoring**
Run daily or hourly in incremental mode to capture only new, updated, or expired ${NOUNS}. Perfect for price-tracking, churn analysis, and alerting pipelines.

**AI / LLM training data**
Structured JSON per product is ready for RAG pipelines, embeddings, and agent workflows. Compact mode trims tokens for LLM context windows.

---

## Quick start

```json
{
  "query": "led lights",
  "location": "CN",
  "maxResults": 100,
  "compact": false,
  "descriptionFormat": "all",
  "excludeEmptyFields": false,
  "incrementalMode": false,
  "skipReposts": false,
  "emitUnchanged": false,
  "emitExpired": false,
  "notifyOnlyChanges": false,
  "notificationLimit": 5
}
```

---

## Input parameters

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | — | Product search keyword, e.g. "led lights". For several keywords write a JSON list, e.g. ["led lights", "solar panel"]; each keyword is searched separately. Required if no startUrls provided. |
| `location` | string | — | Leave empty to search suppliers in every country (global search). Enter a 2-letter country code (e.g. CN, US, VN, IN) to search only suppliers from that country. |
| `maxResults` | integer | `100` | Maximum total results (0 = unlimited). |
| `maxPagesPerQuery` | integer | `0` | How many result pages (40-48 products each) to read for each keyword or start URL, 1-100. 0 = every page alibaba.com serves (up to 100). Max Results still caps the total delivered. |
| `startUrls` | array | `[]` | Paste raw search URLs from the target site. Each URL becomes its own search task; results are merged and deduped by listing ID across all URLs. When provided, startUrls REPLACE the query/location fields (each supported URL becomes one task; unsupported URLs are skipped, and if none is supported the run stops with an input error). |
| `minPrice` | number | — | Only products whose unit price reaches this value (in the Currency below, USD when empty). 0 = no limit. |
| `maxPrice` | number | — | Only products whose unit price starts at or below this value (in the Currency below, USD when empty). 0 = no limit. |
| `currency` | string | — | 3-letter currency code (e.g. EUR, GBP, CNY) for Min/Max price. Each product also gets convertedPriceMin/convertedPriceMax in this currency (ECB rates). Empty = USD, no conversion. |
| `maxMoq` | integer | — | Only products you can order in this quantity or less. 0 = no limit. |
| `minRating` | number | — | Only products rated at least this (0-5). 0 = no limit. |
| `minReviewCount` | integer | — | Only products with at least this many buyer reviews. 0 = no limit. |
| `minSupplierYears` | integer | — | Only suppliers with at least this many years on alibaba.com. 0 = no limit. |
| `compact` | boolean | `false` | Core fields only (for AI-agent/MCP workflows). |
| `descriptionFormat` | enum | `"all"` | Pick a single description representation. `all` keeps every variant; `text` / `html` / `markdown` drop the others. |
| `excludeEmptyFields` | boolean | `false` | Drop null, empty-string, and empty-array fields from each record before push. Smaller payloads for AI agents and dashboards. |
| `incrementalMode` | boolean | `false` | Compare against previous run state. stateKey is optional — defaults to a value derived from search inputs (queries, locations, startUrls, country) so different filter sets never share state. |
| `stateKey` | string | — | Optional. Stable identifier for the tracked search universe. Leave empty to auto-generate from search inputs. |
| `skipReposts` | boolean | `false` | When incremental, skip listings whose content matches an expired listing from a prior run (cross-run duplicate detection). |
| `emitUnchanged` | boolean | `false` | When incremental mode is on, also emit listings whose content has not changed since the last run. |
| `emitExpired` | boolean | `false` | When incremental mode is on, also emit listings that were seen before but are no longer found. |
| `notifyOnlyChanges` | boolean | `false` | When Incremental Mode is on, only send notifications for NEW and UPDATED listings. Has no effect outside incremental mode. |
| `notificationLimit` | integer | `5` | Maximum number of listings included in each notification message (1–20). |
| `telegramToken` | string | — | Telegram bot token (from @BotFather). Required for Telegram notifications. |
| `telegramChatId` | string | — | Telegram chat or channel ID (e.g. "-100123456789"). Required when telegramToken is set. |
| `discordWebhookUrl` | string | — | Discord incoming webhook URL. Server Settings → Integrations → Webhooks → New Webhook. |
| `slackWebhookUrl` | string | — | Slack incoming webhook URL. api.slack.com/messaging/webhooks. |
| `whatsappPhoneNumberId` | string | — | Your WhatsApp Business phone-number ID (numeric, from Meta dashboard). Required when whatsappAccessToken is set. |
| `whatsappAccessToken` | string | — | WhatsApp Cloud API permanent access token (System User token from Meta Business). Recipient must have messaged the business number within the last 24h (service-conversation window — free since Nov 2024). |
| `whatsappTo` | string | — | Recipient phone in E.164 format without + (e.g. "436641234567"). Recipient must have messaged your business number within last 24h. |
| `webhookUrl` | string | — | Receives a JSON POST with {metadata, items} after each run. Universal escape hatch for n8n / Make / Zapier / custom backends. |
| `webhookHeaders` | object | — | Optional JSON object of custom headers (e.g. {"Authorization":"Bearer ..."}). |
| `appConnector` | string | — | Optional. Pick a connected app under Settings → API & Integrations to receive your results (including any contact details). Best-effort across MCP connectors as Apify expands its catalog. |
| `mcpIssueTeam` | string | — | Only when the connected app is an issue tracker: the team (name or ID) the summary issue is created under, if that app requires one. |

---

## Output fields

Every product returns the same 85-field schema. Missing values are `null` — never omitted.

- `id`
- `title`
- `productId`
- `productUrl`
- `priceMin`
- `priceMax`
- `priceText`
- `currency`
- `quantityPrices`
- `minOrderQuantity`
- `minOrderUnit`
- `moqText`
- `soldCount`
- `soldText`
- `leadTimeDays`
- `categoryId`
- `certifications`
- `attributes`
- `imageUrl`
- `images`
- `hasVideo`
- `isSponsored`
- `rating`
- `reviewCount`
- `productScore`
- `productReviewScore`
- `supplierServiceScore`
- `shippingScore`
- `reviewTags`
- `supplierId`
- `supplierName`
- `supplierUrl`
- `supplierProductsUrl`
- `supplierLogo`
- `supplierCountry`
- `supplierCountryName`
- `supplierYears`
- `supplierMainProducts`
- `isGoldSupplier`
- `isVerifiedSupplier`
- `verifiedBy`
- `tradeAssurance`
- `supplierResponseRate`
- `supplierOrderCount`
- `supplierTransactionVolume`
- `supplierStarLevel`
- `supplierExportCountries`
- `companyId`
- `companyName`
- `companyLogo`
- `contactSupplier`
- `countryCode`
- `displayStarLevel`
- `goldSupplierYears`
- `supplierHref`
- `supplierHomeHref`
- `eurl`
- `tmlid`
- `trackInfo`
- `lyb`
- `isShowAd`
- `mainImage`
- `multiImage`
- `price`
- `moq`
- `moqV2`
- `reviewScore`
- `supplierService`
- `customGroup`
- `koreaAgeRestricted`
- `showAddToCart`
- `showCrown`
- `goldSupplierIcon`
- `selling_points`
- `selling_points_pc`
- `position`
- `searchQuery`
- `scrapedAt`
- `portalUrl`
- `listingId`
- `contentQuality`
- `detailFetched`
- `source`
- `contentHash`
- `changeType`

---

## Sample output

One object per product. Here is a real example from a production run:

```json
{
  "id": 1601516930193,
  "title": "COXO Ultra Slim Flexible Bendable LED Panel 24v Dimmable 4000k 6000k Surface Diffuser Backlit Backlighting Sheet Panel LED Light",
  "productId": "1601516930193",
  "productUrl": "https://www.alibaba.com/product-detail/Ultra-Slim-Flexible-Bendable-LED-Panel_1601516930193.html",
  "priceMin": 7.6,
  "priceMax": 10.2,
  "priceText": "US $7.60-$10.20",
  "currency": "USD",
  "quantityPrices": [
    {
      "price": 10.2,
      "quantityMin": 30,
      "quantityMax": 99,
      "unit": "pieces"
    },
    {
      "price": 9.3,
      "quantityMin": 100,
      "quantityMax": 499,
      "unit": "pieces"
    },
    {
      "price": 8.35,
      "quantityMin": 500,
      "quantityMax": 999,
      "unit": "pieces"
    },
    {
      "price": 7.6,
      "quantityMin": 1000,
      "quantityMax": null,
      "unit": "pieces"
    }
  ],
  "minOrderQuantity": 30,
  "minOrderUnit": "pieces",
  "moqText": "30 pieces"
}
```

*Truncated — full records contain 85 fields. See Output fields for the complete schema.*

**[Try Alibaba.com Product & Supplier Scraper [Just 💰$0.63] now — $5 free credit, no credit card →](https://apify.com/blackfalcondata/alibaba-com-scraper?fpr=1h3gvi)**

---

## Pricing

Pay only for what you extract. No subscription required — Apify's free $5 credit covers thousands of results.

| Event | Price (USD) |
| --- | --- |
| Actor Start | $0.01 |
| Result | $0.00063 |

See the [actor on Apify](https://apify.com/blackfalcondata/alibaba-com-scraper?fpr=1h3gvi) for current pricing.

---

## FAQ

**How do I scrape alibaba.com?**
Use this actor on Apify to extract structured data from alibaba.com. Configure your search query and filters in the input, then click Start — no coding required.

**How do I get alibaba.com data as JSON, CSV, or Excel?**
The actor writes each product to Apify's dataset. Download as JSON, CSV, or Excel from the Console, stream via the API, or push to Make, Zapier, Airbyte, or Keboola.

**Is it legal to scrape alibaba.com?**
Web scraping of publicly available data is generally legal. This actor only accesses publicly visible information. Always check alibaba.com's terms of service for your specific use case.

**How much does it cost?**
Pay-per-event pricing — you only pay for ${NOUNS} extracted. Apify's free $5 credit is enough to run thousands of results before you pay anything.

**How does incremental mode work?**
Each product gets a content hash. On subsequent runs, only new or changed products are emitted — saving time, compute, and storage. Expired products can be tracked separately.

**Do I need an API key or credentials?**
No. Just sign up for Apify, paste your input, and click Start. No credit card required.

---

## Related products by Black Falcon Data

- [Djinni Scraper](https://apify.com/blackfalcondata/djinni-scraper?fpr=1h3gvi) — Ukraine & CEE tech jobs with salary and English level
- [Work.ua Scraper](https://apify.com/blackfalcondata/work-ua-scraper?fpr=1h3gvi) — Ukraine's work.ua job listings
- [NoFluffJobs Scraper](https://apify.com/blackfalcondata/nofluffjobs-scraper?fpr=1h3gvi) — Poland & CEE IT jobs with transparent salary ranges
- [OLX Jobs Scraper](https://apify.com/blackfalcondata/olx-jobs-scraper?fpr=1h3gvi) — OLX job listings across 7 CEE countries
- [Prace.cz Scraper](https://apify.com/blackfalcondata/prace-scraper?fpr=1h3gvi) — Czech Republic's prace.cz job board
- [Profession.hu Scraper](https://apify.com/blackfalcondata/profession-scraper?fpr=1h3gvi) — Hungary's profession.hu job board

[Browse all Black Falcon Data actors →](https://apify.com/blackfalcondata?fpr=1h3gvi)

---

## Getting started with Apify

New to Apify? [Create a free account with $5 credit](https://console.apify.com/sign-up?fpr=1h3gvi) — no credit card required.

1. Sign up — $5 platform credit included
2. Open [Alibaba.com Product & Supplier Scraper [Just 💰$0.63]](https://apify.com/blackfalcondata/alibaba-com-scraper?fpr=1h3gvi) and configure your input
3. Click **Start** — export results as JSON, CSV, or Excel

Need more later? [See Apify pricing](https://apify.com/pricing?fpr=1h3gvi).

---

## About Black Falcon Data

Black Falcon Data builds production-grade web scrapers for job boards and marketplace data. Browse our full actor catalog at [www.blackfalcondata.com](https://www.blackfalcondata.com).

---

*Last updated: 2026 10*
