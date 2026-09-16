---
name: nexscope-amazon-keyword-opportunity
description: >-
  Research Amazon keyword opportunity for a seed term or ASIN using Nexscope's
  data skills — expand keywords, pull search-volume/overview metrics, and check
  share-of-voice — grounded in real Nexscope skill operations.
api: Nexscope Ecommerce Data and Creative APIs
generated: '2026-09-16'
method: generated
source: openapi/nexscope-openapi.json
operations:
  - runAmazonKeywordExpansion
  - runAmazonKeywordOverview
  - runAmazonKeywordSummary
  - runAmazonKeywordShareOfVoice
  - runAmazonAsinKeywords
---

# Amazon keyword opportunity workflow

All calls are `POST https://api.nexscope.ai/api/skill-api/v1/skills/{skill}/run`
with header `Authorization: Bearer <NEXSCOPE_API_KEY>` and a JSON body. Inspect
the response `code` (0 = success); a non-zero `code` is an error even on HTTP
200 (see errors/nexscope-problem-types.yml). Calls consume credits.

1. **Expand the seed** — `runAmazonKeywordExpansion`
   (`skills/amazon-keyword-expansion/run`) to turn a seed keyword into a related
   term set.
2. **Score demand** — `runAmazonKeywordOverview`
   (`skills/amazon-keyword-overview/run`) and `runAmazonKeywordSummary`
   (`skills/amazon-keyword-summary/run`) for search volume, trend, competition
   and PPC bid signals per term.
3. **Check competitive position** — `runAmazonKeywordShareOfVoice`
   (`skills/amazon-keyword-share-of-voice/run`) to see who owns the term.
4. **Reverse from a competitor ASIN** — `runAmazonAsinKeywords`
   (`skills/amazon-asin-keywords/run`) to pull the keywords a competing ASIN
   ranks for and fold new opportunities back into step 2.

Notes: pace requests (~5s starting interval is provider guidance, not a
guarantee); honor `Retry-After` on 429. No idempotency key is supported, so
treat retries as fresh billable calls.
