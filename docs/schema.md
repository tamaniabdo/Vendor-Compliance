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
- required_fields (json)
- validity_rules (json)
- category (string)

---

## ReviewTask
- id (string)
- supplier_document_id (string)
- reason (string)
- created_by (string)
- status (open, closed)

---

## AuditLog
- id (string)
- supplier_document_id (string)
- event_type (string)
- payload (json)
- created_at (datetime)