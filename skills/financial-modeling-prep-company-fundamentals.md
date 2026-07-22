---
name: Review a company's fundamentals
description: Pull a company's profile, financial statements, and ratios from Financial Modeling Prep to build a fundamentals picture.
api: openapi/financial-modeling-prep-profile-api-openapi.yml
operations: [getCompanyProfile, getIncomeStatement, getBalanceSheet, getCashFlowStatement, getFinancialRatios]
generated: '2026-07-22'
method: generated
---

# Review a company's fundamentals

Base URL: `https://financialmodelingprep.com/stable`. Authenticate every request with `?apikey=YOUR_API_KEY` (use `&apikey=` when other query parameters exist) or an `apikey` header. All operations are read-only GETs.

1. **Profile** — `getCompanyProfile`: `GET /profile?symbol=AAPL`. Confirms the company exists and returns price, marketCap, beta, sector, and identifiers (symbol, cik).
2. **Income statement** — `getIncomeStatement`: `GET /income-statement?symbol=AAPL&limit=5&period=FY`. `period` accepts Q1–Q4, FY, annual, quarter.
3. **Balance sheet** — `getBalanceSheet`: `GET /balance-sheet-statement?symbol=AAPL&limit=5&period=FY`.
4. **Cash flow** — `getCashFlowStatement`: `GET /cash-flow-statement?symbol=AAPL&limit=5&period=FY`.
5. **Ratios** — `getFinancialRatios`: `GET /ratios?symbol=AAPL&limit=5&period=FY` for margins, liquidity, and valuation ratios.

Rules:
- A `401` returns `{"Error Message": "Invalid API KEY. ..."}` — fix the key, do not retry.
- Do not assume undocumented parameters exist (FMP docs are explicit about this).
- Endpoint availability, symbol coverage, and historical range are plan-gated (free tier: 250 calls/day, 5 years history, some endpoints limited to US or a fixed symbol set) — see plans/financial-modeling-prep-plans-pricing.yml.
- Legacy `/api/v3` and `/api/v4` URLs are discontinued; only use `/stable`.
