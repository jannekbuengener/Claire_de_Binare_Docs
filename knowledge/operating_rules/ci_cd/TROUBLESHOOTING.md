# CI_TROUBLESHOOTING

Date: 2025-12-19
Scope: Common CI failures and fixes

## Lint failures (ruff)
- Run locally: `ruff check .`
- Fix reported files or use `ruff check . --fix` where safe.

## Formatting failures (black)
- Run locally: `black .`
- Re-run `black --check --diff .` to verify.

## Type-check warnings (mypy)
- Job is non-blocking but should be addressed.
- Common fixes: add type hints, fix import paths, adjust mypy config.

## Test failures (pytest)
- Run: `pytest -v -m "not e2e and not local_only"`
- Check missing dependencies in requirements-dev.txt.

## Secrets scan (gitleaks) failures
- Remove secrets from repo history if committed.
- Use `.gitignore` for local secrets.

## Bandit / pip-audit findings
- Review report artifacts (bandit-report.json, pip-audit.json).
- Patch or pin vulnerable dependencies.

## Docs lint failures (markdownlint)
- Run: `markdownlint '**/*.md' --ignore node_modules --ignore .venv`
- Fix line length, header order, or list formatting.
