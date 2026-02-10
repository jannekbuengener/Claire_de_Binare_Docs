# Painpoints #42 ? Implementation Plan (Soak-safe)

Source: D:\Dev\Workspaces\Prompts\PAINPOINTS

Scope: Docs-only, no runtime impact

## Checklist
- [ ] Policy knowledge/governance/STATUS_HEADER_POLICY.md uebernehmen (git mv falls vorhanden) und als CANON bestaetigen
- [ ] Verifier scripts/verify_status_headers.ps1 uebernehmen und lokal ausfuehren
- [ ] Status-Header in allen In-Scope-Dateien setzen: knowledge/** (ohne logs/archive/agent_trust), agents/**, README.md; YAML-Frontmatter bevorzugt; kein zweiter Frontmatter-Block
- [ ] Policy-Link in agents/AGENTS.md und agents/CLAUDE.md (weitere Agent-Charters falls vorhanden)
- [ ] Kurzreport (updated/skipped/ambiguous) + Verifier-Output fuer PR-Description
- [ ] Koordination mit #43: knowledge/status/** spaeter um Operational-State erweitern; Header koexistieren, keine doppelten Bloecke

## Acceptance Criteria
- Verifier scripts/verify_status_headers.ps1 laeuft clean (0 missing, 0 invalid).
- Alle In-Scope-Dateien haben genau einen gueltigen Status-Header (Frontmatter oder Plain).
- gents/AGENTS.md und gents/CLAUDE.md verlinken die Policy.
- Kein zweiter Frontmatter-Block wurde hinzugefuegt.

## Dependencies
- Issue #43 (Operational-State Header muss mit Status-Header koexistieren).

## Gate
MERGE AFTER SOAK (Soak-Test running)
