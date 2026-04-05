# Redis + Worker System

## What
We use Redis + BullMQ to handle background jobs.

## Why
Heavy tasks (like PDF parsing) should NOT run inside API requests.

## Flow
1. User uploads file
2. API sends job to Redis queue
3. Worker picks job
4. Worker processes file
5. Worker saves result to database

## Tools
- Redis → stores jobs
- BullMQ → manages queue
- Worker → processes jobs

## Example job
- documentId
- filePath
- fileHash

## Result
- parsed text saved
- status updated in database