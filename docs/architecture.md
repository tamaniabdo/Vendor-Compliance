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
## Componenets
Frontend (React): file upload form, result rendering
Backend (Express): validation, hashing, parsing orchestration, response
Database (Mongo): supplier docs + audit events + requirements
Storage: local uploads now, S3 later
Queue (later): Redis/BullMQ for async parse




---


## Key Principle

Never block user requests for heavy processing.
Use background workers for all slow tasks.