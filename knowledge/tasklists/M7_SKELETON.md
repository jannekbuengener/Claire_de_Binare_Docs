# M7_SKELETON

Milestone: M7
Goal: Issue-ready cluster breakdown for implementation

## Cluster: Data/Feed
Subtasks:
1. Market data ingestion pipeline baseline
2. Data validation and schema checks
3. Backfill and replay support
Dependencies: Redis, Postgres
Acceptance:
- Data feed runs in docker-compose
- Basic validation errors surfaced

## Cluster: Signal
Subtasks:
1. Signal generation service baseline
2. Signal quality metrics
3. Publish signals to Redis
Dependencies: Data/Feed
Acceptance:
- Signals produced from live feed
- Metrics endpoint available

## Cluster: Risk
Subtasks:
1. Risk gate enforcement (paper-only)
2. Position limit checks
3. Drawdown and circuit breaker wiring
Dependencies: Signal
Acceptance:
- Risk blocks invalid orders
- Circuit breakers trigger deterministically

## Cluster: Execution
Subtasks:
1. Mock execution path stable
2. Order persistence (orders/trades)
3. Execution metrics and health checks
Dependencies: Risk, Postgres
Acceptance:
- Orders flow end-to-end in paper mode
- DB persistence verified

## Cluster: PSM
Subtasks:
1. Portfolio state model baseline
2. PnL tracking per symbol
3. Export summary snapshots
Dependencies: Execution, Postgres
Acceptance:
- Snapshot export available
- PnL metrics stable

## Cluster: Observability
Subtasks:
1. Prometheus scraping for core services
2. Grafana dashboards wired
3. Alert rules for downtime
Dependencies: All services
Acceptance:
- Dashboards render without errors
- Alerts fire in test scenario

## Cluster: Reporting
Subtasks:
1. Daily report generation
2. Weekly status template usage
3. Compliance summary export
Dependencies: Observability, PSM
Acceptance:
- Reports generated from live data
- Stored in Docs Hub

## Cluster: Ops
Subtasks:
1. Paper trading runbook
2. Docker hardening checklist
3. Smoke test checklist
Dependencies: Execution, Observability
Acceptance:
- Runbook is actionable
- Smoke tests documented

