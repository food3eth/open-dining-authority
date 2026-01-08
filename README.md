# Open Dining Authority

An open-source, community-governed restaurant review authority built on
transparent methodology, structured reviews, and explainable aggregation.

This project answers:

> How do we build a restaurant review system people trust because they can see how it works?

---

## Why This Exists

Many restaurant review platforms suffer from:
- Opaque ranking algorithms
- Incentive misalignment (ads, promotions, pay-to-play)
- Low-signal unstructured reviews
- No clear definition of “authority”

Open Dining Authority takes a different approach:
authority is earned through methodology, transparency, and repeatability.

---

## Core Principles

- **Transparency over precision** — every score is explainable
- **Methodology over popularity** — no engagement-driven ranking
- **Structured signal over rants** — constrained reviews improve quality
- **Open governance** — rules are public, versioned, auditable

See: `governance/authority-principles.md`

---

## What This Project Is (and Is Not)

### This project is
- An open specification for review authority
- A reference implementation of structured reviews + aggregation
- A platform for first-party, experience-based reviews
- A community-governed alternative to opaque review platforms

### This project is not
- A scraping engine
- A Yelp / Google Maps replacement
- A marketing platform for restaurants
- A black-box AI ranking system

---

## Repository Structure
├── governance/ # Authority rules and principles
├── specs/ # Data models and API contracts
├── config/ # Public constants used in aggregation logic
├── examples/ # Sample fixtures (no real user data)
└── docs/ # Additional project documentat

The governance documents are the source of truth.

---

## Current Status

- ✅ Authority Principles v0.1
- ✅ Review Schema v0.1
- ✅ Reviewer Reputation Rules v0.1
- ✅ Authority Weighting & Aggregation Logic v0.1
- ✅ Community Review Data License v0.1 (Draft)
- ✅ MVP Data Model & API Contracts v0.1
- ⏳ Reference implementation (not started)
- ⏳ Single-city pilot

---

## How Authority Works (High Level)

1. Reviewers submit structured, experience-based reviews
2. Reviews are weighted by reputation, recency, and verification signals
3. Scores are aggregated using documented deterministic logic
4. Outputs include an explainability ledger

No hidden boosts. No silent changes.

---

# Licensing

This repository uses multiple licenses by design:

- **Code**: Apache 2.0 (`LICENSE`)
- **Governance and specification documents**: CC BY 4.0 (`LICENSE-docs`)
- **Example and fixture data**: CC0 1.0 (`LICENSE-examples`)

Live user-generated review data is not stored in this repository and is governed separately.

