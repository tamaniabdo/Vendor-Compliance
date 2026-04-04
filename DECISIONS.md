# DECISIONS.md — Key Architecture Decisions

## Stack choice
- Chosen stack for this learning path: **MERN** (MongoDB, Express, React, Node).
- Reason: you asked for MERN; it is common in industry and allows full-stack JS.

## Backend framework
- Option A: FastAPI (Python) — faster to iterate for parsing tasks.
- Option B: Node.js + Express — chosen to keep MERN consistency.
- Decision: **Express** (Node) to keep stack consistent and maximize full-stack JS learning.

## Database
- Dev: start with **MongoDB (local)** for flexible document model.
- Prod: MongoDB Atlas or Postgres (if relational data becomes required).
- Migration plan: design simple schema and prepare migration docs (if move from Mongo → Postgres).

## File storage
- Dev: local `./uploads` directory.
- Prod: **S3** (or equivalent) with server-side encryption.
- Rationale: S3 is standard and scalable.

## Parsing & background processing
- Phase 1 (MVP): parse synchronously for small scale.
- Later: push parsing to background worker via **BullMQ / Redis** for scale and robustness.

## Idempotency
- Use SHA-256 file hash to deduplicate and identify uploads.

## Queue choice
- Node ecosystem: **BullMQ** (Redis-backed) recommended.
- Alternatives: RabbitMQ, Kue.

## Observability
- Start with request logging and basic metrics (Prometheus-compatible counters).
- Later: add OpenTelemetry and a managed tracing/observability platform.

## Security
- Dev: simple dev-token auth.
- Prod: JWT/OAuth + RBAC + secrets manager for DB and S3 credentials.