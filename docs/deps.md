# deps.md — Dependencies and setup (MERN)

## Overview
This project uses MERN stack:
- Frontend: React (Vite)
- Backend: Node.js + Express
- Database: MongoDB (dev: local) -> Prod: MongoDB Atlas or Postgres if needed
- Queue / Workers: Redis + BullMQ
- File storage: local uploads (dev) -> S3 (prod)

## Backend (Node/Express) - core packages
- express — web framework
- multer — file uploads
- mongoose — MongoDB ODM
- bullmq — job queue (Redis-backed)
- ioredis — Redis client for BullMQ
- pdf-parse — PDF text extraction
- crypto — node builtin (for hashing)
- dotenv — environment variables
- joi or zod — input validation
- winston / pino — structured logging
- helmet — HTTP security middleware
- cors — CORS handling
- morgan — request logging (dev)
- jest / supertest — testing

### Dev / infra tools
- nodemon — restart server in dev
- eslint / prettier — linting & code style
- pm2 / systemd (prod) — process manager (if not using container)
- Docker — for containerizing services

