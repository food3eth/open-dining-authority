# MVP Data Model v0.1

## 1. Purpose
This document defines the minimal canonical data model required to support
structured reviews, reviewer reputation, and authority aggregation.

This model prioritizes auditability, determinism, and legal safety over flexibility.

---

## 2. Core Entities

### 2.1 Restaurant (Canonical)
Represents a single real-world dining venue.

Fields:
- restaurant_id (UUID, primary key)
- name
- address_line1
- address_line2 (optional)
- city
- region (state/province)
- postal_code (optional)
- country (ISO code)
- latitude (optional)
- longitude (optional)
- phone (optional)
- website_url (optional)
- cuisine_tags (array)
- price_tier (unknown | $ | $$ | $$$ | $$$$)
- created_at
- updated_at

A restaurant_id is stable and never reused.

---

### 2.2 Restaurant Alias
Tracks alternate names or spellings.

Fields:
- alias_id (UUID)
- restaurant_id (FK)
- alias_name
- source (user | admin | import)
- created_at

Aliases do not create new canonical restaurants.

---

### 2.3 External Reference (Signals Only)
Links to legally accessible third-party identifiers.

Fields:
- ref_id (UUID)
- restaurant_id (FK)
- provider (yelp | google | michelin | opentable | other)
- external_id
- external_url
- signals_json (aggregate ratings, counts, badges only)
- last_fetched_at (optional)
- created_at

Third-party review text is explicitly excluded.

---

## 3. Reviewer

### 3.1 Reviewer Identity
Represents a persistent reviewer.

Fields:
- reviewer_id (UUID)
- handle (unique)
- display_name (optional)
- status (active | suspended | banned)
- created_at

---

### 3.2 Reviewer Reputation Snapshot
Stores current reputation tier.

Fields:
- reviewer_id (FK)
- tier (R0 | R1 | R2 | R3 | R4)
- effective_from
- reason (optional)
- updated_at

Reputation history may be stored separately but is not required for MVP.

---

## 4. Review

### 4.1 Review Record
Structured review eligible for authority calculations.

Fields:
- review_id (UUID)
- restaurant_id (FK)
- reviewer_id (FK)
- schema_version ("0.1")
- visit_date
- visit_time_block
- party_size
- service_mode
- items_ordered (JSON array)
- food_execution (1–5)
- consistency (1–5)
- hospitality (1–5)
- atmosphere (1–5)
- value (1–5)
- context_fit_tags (array)
- experience_note (50–300 chars)
- optional_context (noise_level, wait_time, etc.)
- verification (JSON, optional)
- moderation_status (pending | active | excluded | removed)
- exclusion_reason (optional)
- created_at
- updated_at

Constraint:
- Only the most recent eligible review per reviewer per restaurant is used
  in aggregation.

---

## 5. Moderation Inputs

### 5.1 Review Flags
Used for moderation and abuse detection.

Fields:
- flag_id (UUID)
- review_id (FK)
- flagger_reviewer_id (FK)
- reason (spam | harassment | conflict_interest | other)
- details (optional)
- created_at

---

## 6. Authority Profile (Computed)

### 6.1 Authority Profile Snapshot
Cached, recomputable output.

Fields:
- restaurant_id (FK)
- review_schema_version
- reputation_rules_version
- aggregation_logic_version
- computed_at
- dimension_scores_json
- context_fit_json
- composite_json (optional)
- freshness_json
- coverage_json
- explainability_ledger_json

Authority profiles must be fully reproducible from source data.

---

## 7. Design Constraints
- No raw third-party review text
- No unstructured global ratings
- No irreversible aggregation
- No hidden or mutable logic

---

## 8. Versioning
This document is MVP Data Model v0.1.
Changes require versioned updates.

