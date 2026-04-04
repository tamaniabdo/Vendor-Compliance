# Architecture Overview (Vendor Compliance System)

## Flow

React (Frontend)
→ FastAPI (Backend)
→ SQLite (Dev DB) / Postgres (Prod DB)
→ Local Storage (Dev) / S3 (Prod)
→ Redis Queue (Background Workers)
→ Rules Engine
→ Response back to React UI

---

## Why this design exists

- Frontend is separated from backend for scalability
- Backend handles all business logic
- Database stores structured compliance data
- File storage avoids bloating database
- Queue handles slow processing (PDF parsing)
- Rules engine ensures compliance logic is centralized

---

## Key Principle

Never block user requests for heavy processing.
Use background workers for all slow tasks.