# Data Schema (Vendor Compliance System)

## User
- id (string)
- email (string)
- password_hash (string)

---

## SupplierDocument
- id (uuid)
- vendor_name (string)
- document_type (string)
- document_number (string)
- issue_date (date)
- expiry_date (date)
- approval_status (enum, e.g. pending/approved/rejected)
- parsed_fields (json)
- pdf_path (string)
- file_hash (string)
- status (enum: parsed, reviewed, flagged, approved)
- created_at (datetime)
- updated_at (datetime)

---

## ComplianceRequirement
- id (string)
- name (string)
- category
- required_fields (json)
- validity_rules (json)
- category (string)
timestamps

---

## ReviewTask
- id (string)
- supplier_document_id (string)
- reason (string)
- created_by (string)
- status (open, closed)
timestamps

---

## AuditLog
- id (string)
- supplier_document_id (string)
- event_type (string)
- payload (json)
- created_at (datetime)

---

## Constraints and Rules
1 - unique file_hash
.file_hash must be unique in supplier_documents.
.Reason: prevent duplicate uploads of same file.
.Enforcement: DB unique index + API duplicate check.

2 - enums for status fields
.status allowed values: parsed, duplicate, error, reviewed, flagged, approved
.approval_status allowed values: pending, approved, rejected
.Reason: avoid typo values and broken filters.
.Enforcement: backend validation + schema enum.

3 - references must be valid
.review_tasks.supplier_document_id must point to real supplier_documents._id
.audit_logs.supplier_document_id (if present) must point to real document
.Reason: prevent orphan records.
.Enforcement: validate existence before create/update.

4 - UTC timestamps only
.created_at and updated_at are stored in UTC only.
.Reason: avoid timezone bugs.
.Enforcement: backend sets UTC, UI only converts for display.

5 - ullable policy
.expiry_date: nullable (some PDFs don’t include it)
.vendor_name: not nullable (core field)
.approval_status: not nullable, default pending
.parsed_fields: not nullable, default {}

---

## Query and Index Intent
.unique index on file_hash
.index on vendor_name
.index on expiry_date
.index on status

