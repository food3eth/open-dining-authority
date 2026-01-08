# Authority Weighting & Aggregation Logic v0.1

## 1. Purpose
Defines how eligible reviews and reviewer reputation combine into
explainable authority scores.

---

## 2. Inputs
- Reviews conforming to Review Schema v0.1
- Reviewer reputation tier (R0–R4)
- Review recency
- Verification signals

---

## 3. Weight Components

Final review weight is the product of:
- Tier weight
- Verification modifier
- Recency modifier
- Diversity safeguards

---

## 4. Tier Weights (Default)
- R0: 0.25
- R1: 0.60
- R2: 1.00
- R3: 1.40
- R4: 1.60

No tier may exceed 2.0.

---

## 5. Recency
- 0–3 months: full weight
- 4–12 months: reduced
- 13–24 months: reduced
- Older reviews excluded by default

---

## 6. Diversity Safeguards
- Only one review per reviewer per restaurant counts
- Soft caps applied if one tier dominates weighting

---

## 7. Dimension Aggregation
Scores are weighted means per dimension with:
- Outlier dampening at low counts
- Minimum evidence thresholds

---

## 8. Context Fit Scores
Context tags are aggregated as weighted proportions
indicating likelihood of fit.

---

## 9. Confidence Levels
Confidence is categorical:
- Low
- Medium
- High

Based on volume, diversity, tier mix, and freshness.

---

## 10. Composite Scores
Optional overall scores may be computed as averages of
available dimension scores.

---

## 11. Explainability Ledger
Every output must include:
- Review counts
- Reviewer counts
- Tier mix
- Caps applied
- Version identifiers

---

## 12. Versioning
This document is Authority Weighting & Aggregation Logic v0.1.

