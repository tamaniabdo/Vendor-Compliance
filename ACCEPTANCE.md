# Acceptance Criteria — MVP MUST-HAVEs

## Upload
- POST /upload accepts PDF file up to 10MB.
- The system returns parsed fields: vendor_name, document_type (if present), expiry_date (if present).
- The parsed values are returned in the API response within 3 seconds for typical PDFs (local dev).

## View
- The UI shows: document id, vendor name, document type, expiry date, and a link to download the original PDF.
- The UI shows clear status: parsed / duplicate / error.

## Idempotency
- Uploading the same file twice (same content) returns the existing document id, not a new duplicated record.

## Security
- Local dev: files encrypted-at-rest (if supported by platform); at minimum, files stored in `./uploads` with controlled filesystem permissions.