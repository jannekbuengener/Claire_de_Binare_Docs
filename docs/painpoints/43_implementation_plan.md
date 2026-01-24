# Painpoints #43 ? Implementation Plan (Soak-safe)

Source: D:\Dev\Workspaces\Prompts\PAINPOINTS

Scope: Docs-only

## Checklist
- [ ] Policy knowledge/governance/OPERATIONAL_STATE_VALIDITY_POLICY.md uebernehmen (CANON) + Links in agents/AGENTS.md und agents/CLAUDE.md (weitere Charters falls vorhanden)
- [ ] Verifier scripts/verify_operational_state_headers.ps1 uebernehmen und lokal ausfuehren
- [ ] Operational-State Header in Primary Targets setzen: knowledge/status/**, knowledge/logs/sessions/**, knowledge/logs/weekly_reports/**; closed set BUILD/STABILIZE/SHADOW/PAPER/LIVE/FREEZE; State-Intent Pflicht
- [ ] YAML-Frontmatter: cdb_doc.operational_state + state_intent in bestehendem Block; Plain-Header nur ohne Frontmatter
- [ ] Kurzreport (updated/skipped/ambiguous) + Verifier-Output fuer PR-Description
- [ ] Abhaengigkeit zu #42: Status-Header und Operational-State muessen im selben Headerblock koexistieren (keine doppelten Frontmatter)

## Acceptance Criteria
- Verifier scripts/verify_operational_state_headers.ps1 laeuft clean (0 missing, 0 invalid).
- Alle Primary Targets enthalten Operational-State + State-Intent im erlaubten Set.
- gents/AGENTS.md und gents/CLAUDE.md verlinken die Policy.
- Kein zusaetzlicher Frontmatter-Block wurde hinzugefuegt.

## Dependencies
- Issue #42 (Status-Header muss mit Operational-State koexistieren).

## Gate
MERGE AFTER SOAK (Soak-Test running)
