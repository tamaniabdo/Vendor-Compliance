# Database Indexing & Rules

## What
Rules for MongoDB structure.

## Why
Makes database fast and prevents bugs.

## Indexes
- file_hash → prevent duplicates
- vendor_name → search faster
- expiry_date → filter expired docs

## Important rule
Do NOT use decimals for money.

## Instead use:
- cents (integer)
Example:
$10.50 → 1050 cents


## Index Strategy
- file_hash — unique index
Why: same file content must not create duplicates.

- endor_name — index
Why: fast vendor filtering and search.

- expiry_date — index
Why: fast expired/expiring reports.

- status — index
Why: fast workflow lists (parsed, error, etc.).

- (vendor_name, document_type) — optional compound index
Why: common combined filtering.



## Idempotency Rule
- Same file bytes -> same file_hash -> return existing document ID -> do not insert a new row.

Also add behavior:
- API response for duplicate should clearly indicate duplicate status.
- Keep original record as source of truth.

## Design-Level Test Cases
1-New PDF upload -> new record created
2-Same PDF uploaded again -> existing ID returned
3-Same filename, different file content -> new hash -> new record
4-Two near-simultaneous uploads of same file -> only one record remains
5-Query by vendor_name + status remains fast at larger volume


## How This Can Fail
- unique index missing -> duplicates
- hash computed differently in two paths -> false non-duplicates
- race condition around duplicate check + insert
- inconsistent status values -> bad filtering/index value
- too many indexes -> slower write performance

## Duplicate Bug Debug Sequence
1-Reproduce with same file twice
2-Verify both hashes are identical
3-Confirm DB has unique index on file_hash
4-Confirm insert handles duplicate-key error correctly
5-Confirm API returns existing ID for duplicate path

## Step 4 Quality Gate (Done Checklist)
-file_hash is marked unique
-all 4 indexes listed (file_hash, vendor_name, expiry_date, status)
-optional compound index documented (vendor_name, document_type)
-idempotency rule is explicit
-duplicate API behavior documented (returns existing ID)
