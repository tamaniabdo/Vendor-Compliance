# RISKS.md — Major Risks & Mitigations

1. PDF parsing failures
   - Risk: PDFs are scanned images or inconsistent formats → parser fails.
   - Mitigation: Add Tesseract OCR fallback; confidence scoring; manual override UI.

2. Duplicate documents / idempotency failure
   - Risk: duplicates inflate records and cause inconsistent state.
   - Mitigation: use file hash (SHA-256) uniqueness, return existing id for duplicates.

3. PII / legal exposure
   - Risk: supplier docs contain sensitive info.
   - Mitigation: encrypt at rest, restrict access, retention policy, logs for access.

4. Audit evidence missing
   - Risk: no immutable audit trail.
   - Mitigation: store audit events for uploads, parsing events, changes; keep original PDF.

5. Unauthorized access
   - Risk: users access sensitive docs.
   - Mitigation: RBAC, TLS, secure storage.

6. Operational cost
   - Risk: cloud costs for storage, workers, DB.
   - Mitigation: cost model in Phase P8; cleanup policy for old files; use tiered storage.

7. Over-engineering / scope creep
   - Risk: building huge product before core works.
   - Mitigation: strict MVP definition, one-commit-per-small-feature discipline.

8. Data quality & false positives
   - Risk: parser returns incorrect fields leading to wrong decisions.
   - Mitigation: confidence score, manual review flag, logs of parsing method.