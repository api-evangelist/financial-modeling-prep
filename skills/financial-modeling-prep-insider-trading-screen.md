---
name: Screen insider trading activity
description: Search SEC insider transactions for a company and cross-check against its market quote using Financial Modeling Prep.
api: openapi/financial-modeling-prep-insider-trading-api-openapi.yml
operations: [getInsiderTrading, getQuote]
generated: '2026-07-22'
method: generated
---

# Screen insider trading activity

Base URL: `https://financialmodelingprep.com/stable`. Authenticate with `?apikey=` or the `apikey` header.

1. **Search insider trades** — `getInsiderTrading`: `GET /insider-trading/search?symbol=AAPL&page=0&limit=100`. Filters: `reportingCik`, `companyCik`, `transactionType` (e.g. `S-Sale`, `P-Purchase`). Each row carries filingDate, transactionDate, reportingName, typeOfOwner, securitiesTransacted, price, and a `url` to the SEC filing.
2. **Paginate** — increase `page` until fewer than `limit` rows return. Page starts at 0.
3. **Cross-check the market** — `getQuote`: `GET /quote?symbol=AAPL` to compare insider transaction prices against the current price.

Rules:
- `acquisitionOrDisposition` is `A` (acquired) or `D` (disposed); `directOrIndirect` is `D`/`I` ownership.
- Always cite the SEC filing `url` when reporting a specific transaction.
- Plan gating applies (free tier limits pages/symbols on some endpoints); `401` returns the `{"Error Message": ...}` envelope.
