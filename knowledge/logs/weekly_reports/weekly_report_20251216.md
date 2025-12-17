---
relations:
  role: log
  domain: knowledge
  upstream: []
  downstream: []
status: active
tags: [log, weekly_report]
generated: 2025-12-16
---
# Weekly Report – 2025-12-16

## 1. Summary
- Docs Hub prompt migration `.txt → .md` completed; originals kept with deprecation notice.
- Bureau files scan delivered (Issue #119) – canonical decisions about agent-role duplicates pending.
- Repo topology and agents confirmed as canon; GitLab CI guard rails active.

## 2. Highlights
- `PROMPT_MIGRATION_REPORT.md` documents the completed migration of agent prompts.
- `BUERO_FILES_REVIEW.md` lists new bureau files and flags conflict potentials (especially agent roles).
- Stable infrastructure baseline per CDB_KNOWLEDGE_HUB snapshot (compose services with healthchecks).

## 3. Risks / Issues
- Governance review from Gemini still open; potential divergence on agent role files.
- Open handoffs: Claude → Services (`get_secret()` migration, P2).
- Operational risk: disk-space warning from daily check (86% used, 29 GB free).

## 4. Next Actions
| Owner | Action | Due | Status |
| --- | --- | --- | --- |
| Claude | Canonical Location für Agenten-Rollen definieren (Konfliktpotenziale schließen) | 2025-12-20 | Open |
| Services | `get_secret()`-Migration abschließen (P2) | 2025-12-22 | Open |
| Gemini | Governance-Review Feedback liefern | 2025-12-19 | Open |
