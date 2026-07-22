---
name: Look up a quote and price history
description: Resolve a ticker symbol, fetch its real-time quote, and pull historical end-of-day prices from Financial Modeling Prep.
api: openapi/financial-modeling-prep-quote-api-openapi.yml
operations: [searchSymbols, getQuote, getHistoricalPrice]
generated: '2026-07-22'
method: generated
---

# Look up a quote and price history

Base URL: `https://financialmodelingprep.com/stable`. Authenticate with `?apikey=` or the `apikey` header.

1. **Resolve the symbol** — `searchSymbols`: `GET /search-symbol?query=Apple&limit=10` (optional `exchange=NASDAQ`). Use the returned `symbol` for all subsequent calls. Skip this step when the user already gives a ticker.
2. **Quote** — `getQuote`: `GET /quote?symbol=AAPL` returns price, change, day/year ranges, volume, PE, and `timestamp` (epoch seconds — check freshness).
3. **History** — `getHistoricalPrice`: `GET /historical-price-eod/full?symbol=AAPL&from=2026-01-01&to=2026-06-30`. Returns one object per trading day (open/high/low/close, volume, vwap, changePercent).

Rules:
- Free-tier data timing is end-of-day, not real-time; historical range is plan-gated (5 vs 30+ years).
- For continuous prices prefer the WebSocket stream (see asyncapi/financial-modeling-prep-websocket-asyncapi.yml) instead of polling `getQuote`.
- `401` means invalid/missing API key; the error envelope is `{"Error Message": "..."}`.
