# Fraud Strategy – Detection Rules & Anomaly Hunting

This repository contains SQL‑based fraud detection strategies used to identify synthetic identity rings, account takeover attempts, and suspicious transaction patterns.

## Contents

### 1. `LEVENSHTEIN.sql`
**Purpose:** Find near‑duplicate user records (emails, phone numbers) that could indicate synthetic identities, mule accounts, or credential stuffing.

**Highlights:**
- Uses Levenshtein distance to match similar email addresses (e.g., `john.doe@gmail.com` vs `john.doe+1@gmail.com`)
- Identifies multiple accounts sharing the same phone number across different user profiles
- Flags recycled security answers or identical email domains with minor variations

**Example output:**  
A table listing clusters of user IDs with suspiciously similar contact information, ranked by similarity score.

### 2. `test_transactions.sql`
**Purpose:** Detect non‑live or test transactions that could be used to probe fraud rules or bypass controls.

**What it looks for:**
- Common test card numbers (e.g., `4111111111111111`)
- Transaction amounts = `$0.01`, `$0.00`, or round numbers like `$1.00`, `$100.00`
- Descriptors containing keywords: `TEST`, `QA`, `SAMPLE`, `SANDBOX`
- Unusual velocity from a single user in a short time window (e.g., 5+ transactions in 2 minutes)

**Example output:**  
A flagged list of transactions that should be escalated or blocked before they impact fraud metrics.

## How to Use

1. Clone this repository.
2. Modify the table/column names to match your environment.
3. Run these queries in your SQL editor (Databricks, Snowflake, PostgreSQL, etc.).
4. Review the results and integrate into your fraud detection pipeline or monitoring dashboard.
5. Or feel free to use the steps in your own environment.

## Business Impact

- **Reduced false positives** – Targeted detection lowers noise from legitimate users and reduces customer friction.
- **Prevented synthetic identity rings** – Caught 1,000+ fraudulent attempts with <1% false positive rate.
- **Stopped test transaction abuse** – Eliminated loss from low‑value probing attacks.

---

*These strategies were developed during my work at HealthEquity, EBTH, and Genpact. They have been anonymized and generalized for portfolio showcase.*
