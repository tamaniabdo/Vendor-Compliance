# SLOs-and-metrics.md

## SLIs / SLOs (initial)
- SLI: document parse latency (time from upload accepted → parsed fields returned or enqueued)
- SLO: 95% of document parses < 5 seconds (MVP target)
- SLI: parse success rate (no parser exception)
- SLO: parse_success_rate >= 99%

## Metrics to collect (minimal for MVP)
- uploads_total (counter)
- parse_latency_seconds (histogram)
- parse_errors_total (counter)
- duplicate_uploads_total (counter)
- worker_queue_backlog (gauge) — when worker queue active

## Alerts (initial)
- Alert if parse_errors_total rate > 1% in 5m window
- Alert if parse latency p95 > 10s
- Alert if queue backlog > threshold (e.g., 100 items)