# Non-Functional Requirements (NFRs)

- Encryption:
  - Development: local filesystem; mark as "encrypt at rest required in prod".
  - Production: data and files encrypted at rest (S3 server-side encryption + DB encryption).

- Performance:
  - Single-document parse ≤ 3s (target for 95th percentile on small PDFs).
  - API should respond to upload request with initial acknowledgement quickly; heavy parsing may be moved to background worker.

- Security:
  - Basic auth for UI in dev (dev token); in prod use role-based auth (JWT/OAuth).
  - Role separation: admin, reviewer, analyst.

- Resilience:
  - Idempotent uploads (file hashing).
  - Worker retry policy for background tasks (when introduced).

- Storage:
  - Dev: SQLite or Mongo local file depending on stack choice (we will start with Mongo for MERN).
  - Prod: Postgres or Mongo Atlas (document storage) + S3 for files.

- Observability:
  - Basic logs in dev (request id).
  - Metrics and alerts in later phases.

- Maintainability:
  - Tests for parser logic (unit tests).
  - Linting and pre-commit hooks (black/ruff for Python or prettier/eslint for JS depending on stack).