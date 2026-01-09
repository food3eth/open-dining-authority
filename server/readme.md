# Server (Reference Implementation)

This folder contains a reference backend implementation for the Open Dining Authority specifications.

The source of truth for methodology is:
- `/governance` (authority rules)
- `/specs` (data model + API contracts)

The server must implement those documents as written. If implementation and governance disagree, governance wins.

---

## Goals (v0.1)

- Restaurant canonicalization (`POST /restaurants/canonicalize`)
- Review submission + validation (`POST /reviews/validate`, `POST /reviews`)
- Consent enforcement (license version recorded per review)
- Authority profile computation and retrieval
  - `POST /restaurants/{id}/authority-profile/compute`
  - `GET /restaurants/{id}/authority-profile` (with explainability ledger)
- Public read views (restaurants, active reviews, authority profile)

---

## Non-Goals (v0.1)

- Scraping third-party review text
- Bulk exporting other users’ reviews
- Black-box ranking modifiers
- Production-scale deployment concerns

---

## Data Safety

Do not commit:
- `.env` files
- local databases (sqlite, dumps)
- secrets, tokens, or API keys
- any real user-generated review data

Use only synthetic fixtures under `/examples` for tests.

---

## Version Compatibility

This reference server targets:
- Review Schema: v0.1 (`/governance/review-schema-v0.1.md`)
- Reputation Rules: v0.1 (`/governance/reviewer-reputation-rules-v0.1.md`)
- Aggregation Logic: v0.1 (`/governance/authority-weighting-logic-v0.1.md`)
- API Contracts: v0.1 (`/specs/api-contracts-v0.1.md`)
- Data Model: v0.1 (`/specs/data-model-v0.1.md`)

Authority profile outputs must include these versions and an explainability ledger.

---

## Development Status

Not yet implemented.

Recommended next steps:
1. Choose stack (language, framework, DB)
2. Implement review schema validation and consent recording
3. Implement authority aggregation engine with deterministic tests
4. Add minimal endpoints per `/specs/api-contracts-v0.1.md`

