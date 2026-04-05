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

## Example backend package.json (minimal)
Use this to bootstrap backend quickly.

```json
{
  "name": "vendor-guard-backend",
  "version": "0.1.0",
  "main": "src/index.js",
  "scripts": {
    "start": "node src/index.js",
    "dev": "nodemon src/index.js",
    "test": "jest"
  },
  "dependencies": {
    "express": "^4.18.2",
    "mongoose": "^7.0.0",
    "multer": "^1.4.5",
    "pdf-parse": "^1.1.1",
    "dotenv": "^16.0.0",
    "bullmq": "^1.87.0",
    "ioredis": "^5.0.0",
    "helmet": "^6.0.0",
    "cors": "^2.8.5",
    "joi": "^17.9.0",
    "winston": "^3.8.0"
  },
  "devDependencies": {
    "nodemon": "^2.0.22",
    "jest": "^29.0.0",
    "eslint": "^8.0.0",
    "prettier": "^2.0.0"
  }
}