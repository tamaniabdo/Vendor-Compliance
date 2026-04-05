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