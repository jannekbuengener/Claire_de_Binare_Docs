# CI_PIPELINE_GUIDE

Date: 2025-12-19
Scope: CI/CD pipeline overview for contributors
Repo: Claire_de_Binare (Working Repo)

## Overview
Primary CI runs in GitLab via `.gitlab-ci.yml`. GitHub Actions workflows are present for automation/guardrails.

## GitLab CI Pipeline (8 stages)
Stages (from `.gitlab-ci.yml`):
1. governance
2. quality
3. test
4. security
5. docs
6. summary

### Governance
- write-zone-validation (blocking unless DELIVERY_APPROVED via token)

### Quality
- lint (ruff)
- format-check (black)
- type-check (mypy, non-blocking)

### Test
- test-py311 (pytest, coverage)
- test-py312 (pytest, coverage)

### Security
- secrets-scan (gitleaks, blocking)
- security-audit (bandit)
- dependency-audit (pip-audit)

### Docs
- docs-check (markdownlint, non-blocking)

### Summary
- build-summary (always)

## GitHub Actions (selected)
Workflows in `.github/workflows/` include:
- ci.yaml
- branch-policy.yml
- docs-hub-guard.yml
- claude.yml / claude-code-review.yml
- copilot-housekeeping.yml
- stale.yml
- auto-label.yml
- label-bootstrap.yml

## Local equivalents
- Lint: `ruff check .`
- Format: `black --check --diff .`
- Type: `mypy services/ --ignore-missing-imports --no-strict-optional`
- Tests: `pytest -v -m "not e2e and not local_only"`

## Notes
- Some jobs are allow_failure (type-check, bandit, pip-audit, markdownlint).
- Secrets scan is blocking.
