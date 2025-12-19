# RUNBOOK_PAPERTRADING

Date: 2025-12-19
Scope: Paper trading operations runbook (Docs Hub)
Goal: Safe defaults, no live trading, no secrets in repo

## Safe defaults
- MODE=paper
- EXECUTION=dry-run

Location of defaults:
- C:\Users\janne\Documents\GitHub\Workspaces\.cdb_local\.secrets\.env.example

## Preconditions
- Secrets are stored outside the Working Repo.
- Working Repo contains execution-only files.

## Startup
1. Ensure secrets exist in workspace secrets path (.cdb_local/.secrets).
2. From Working Repo root:
   - make docker-up
3. Verify containers are healthy:
   - make docker-health

## Smoke checks
- Confirm services respond on expected ports:
  - 8000 (cdb_ws)
  - 8001 (cdb_core)
  - 8002 (cdb_risk)
  - 8003 (cdb_execution)
  - 8004 (cdb_paper_runner)

## Safety checks
- MODE remains paper
- EXECUTION remains dry-run
- No live trading keys present

## Rollback
- make docker-down
- Remove local containers and volumes if needed

## Notes
- This runbook lives in Docs Hub only.
- No changes are made to Working Repo by this document.
