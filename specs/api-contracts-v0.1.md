# MVP API Contracts v0.1

## 1. Purpose
Defines the minimal REST API surface required to:
- Canonicalize restaurants
- Submit and validate reviews
- Compute and retrieve authority profiles
- Provide public read access

---

## 2. Conventions
- Base path: /api/v1
- Content-Type: application/json
- Authentication required for write operations
- Public read access unless noted

Errors use structured JSON:
{
  "error": {
    "code": "VALIDATION_ERROR",
    "message": "visit_date is required"
  }
}

---

## 3. Restaurant Endpoints

### 3.1 Canonicalize Restaurant
POST /restaurants/canonicalize

Creates or matches a restaurant.

Request:
- name
- address fields
- geo coordinates (optional)

Response:
- restaurant_id
- result (matched | created)
- match_confidence (if matched)

---

### 3.2 Search Restaurants
GET /restaurants?query=&city=&region=

Returns paginated restaurant summaries.

---

### 3.3 Get Restaurant (Public)
GET /restaurants/{restaurant_id}

Returns canonical restaurant details and external signals.

---

## 4. Review Endpoints

### 4.1 Validate Review (Dry Run)
POST /reviews/validate

Validates against Review Schema v0.1 without persistence.

Response:
- valid (true | false)
- warnings (optional)

---

### 4.2 Submit Review
POST /reviews

Requires:
- Authenticated reviewer
- Explicit license acceptance

Response:
- review_id
- moderation_status

---

### 4.3 Get Review (Public)
GET /reviews/{review_id}

Returns sanitized review data only if moderation_status = active.

---

### 4.4 List Reviews for Restaurant
GET /restaurants/{restaurant_id}/reviews

Returns paginated active reviews only.

---

## 5. Authority Profile Endpoints

### 5.1 Compute Authority Profile
POST /restaurants/{restaurant_id}/authority-profile/compute

Admin or system-triggered.

Response:
- status (queued | completed)

---

### 5.2 Get Authority Profile (Public)
GET /restaurants/{restaurant_id}/authority-profile

Returns:
- version identifiers
- dimension scores + confidence
- context fit scores
- coverage indicators
- explainability ledger

Explainability ledger is mandatory.

---

## 6. Reviewer Endpoints

### 6.1 List My Reviews
GET /me/reviews

Authenticated.

---

### 6.2 Delete Review
DELETE /reviews/{review_id}

Effects:
- Removes public display
- Excludes from future aggregation
- Does not retroactively recompute aggregates

---

### 6.3 Export Reviews
GET /me/reviews/export?format=json|csv

Returns only reviewer-owned data.

---

## 7. Moderation Endpoints (Admin)

### 7.1 Flag Review
POST /reviews/{review_id}/flags

Creates a moderation flag.

---

### 7.2 Moderate Review
POST /reviews/{review_id}/moderate

Actions:
- activate
- exclude
- remove

All actions must be logged.

---

## 8. Authorization Rules
- Public: read-only endpoints
- Authenticated: submit, delete, export own reviews
- Admin: moderation, authority computation

---

## 9. Non-Goals
- No scraping endpoints
- No bulk data export of others’ reviews
- No hidden ranking modifiers

---

## 10. Versioning
This document is MVP API Contracts v0.1.
Changes apply prospectively and require documentation.

