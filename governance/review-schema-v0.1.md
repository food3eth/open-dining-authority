# Review Schema v0.1

## 1. Purpose
This schema defines the minimum structured data required for a restaurant review
to be eligible for inclusion in authority calculations.

Reviews that do not conform to this schema may exist in the system but do not
contribute to authority scores.

---

## 2. Eligibility Requirements
A review is eligible if and only if:
- It represents a first-hand dining experience
- It is tied to a specific visit
- It is submitted by a persistent reviewer identity
- All required fields are present and valid

---

## 3. Required Metadata

### Review Identification
- review_id (system-generated)
- reviewer_id (persistent identity)
- restaurant_id (canonical)

---

### Visit Context
- visit_date (YYYY-MM-DD)
- visit_time_block: breakfast | lunch | dinner | late_night
- party_size (1–12)
- service_mode: dine_in | bar_seating | counter | takeout | delivery

---

### Order Information
- items_ordered: list of menu-linked items
- At least one item is required

---

## 4. Evaluation Dimensions (1–5 Scale)

### Food Execution
Quality of preparation and technical execution.

### Consistency
Reliability across ordering and delivery.

### Hospitality
Service quality, professionalism, and warmth.

### Atmosphere
Comfort, noise, pacing, and environment.

### Value
Value relative to price point and category.

---

## 5. Context Fit Tags (Required, multi-select)
At least one:
- quick_meal
- date_night
- business_meeting
- group_dining
- family_friendly
- solo_dining
- special_occasion

---

## 6. Experience Commentary (Constrained)
- 50–300 characters
- Prompt:
  “What would someone with similar expectations appreciate or dislike here?”

Prohibited:
- Profanity
- Personal attacks
- Promotional language
- Comparisons to other platforms

---

## 7. Optional Context (Non-authoritative)
- noise_level
- wait_time_minutes
- reservation_used
- outdoor_seating

---

## 8. Verification Signals (Optional)
- receipt_hash
- reservation_reference
- geo_presence_confirmed

Verification affects weight, not validity.

---

## 9. Explicit Exclusions
- Overall star ratings
- Hearsay
- Incentivized or compensated reviews
- Speculation about operations

---

## 10. Versioning
This document is Review Schema v0.1.
Changes require versioned updates and documentation.

