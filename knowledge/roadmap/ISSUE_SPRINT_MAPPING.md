# Issue → Sprint Mapping (Master Roadmap)

**Roadmap:** `D:\Dev\Workspaces\Prompts\CLAUDE CODE\CLAUDE_MASTER_ROADMAP.md`
**Date:** 2026-01-23
**Status:** 🚧 Initial Mapping

---

## Sprint 0 — Enforcement & Hygiene (✅ DONE)

**Goal:** CI/CD durchsetzbar, Merges kontrolliert

**Status:**
- ✅ GitHub Pro aktiv
- ✅ CI kann laufen
- ⚠️ Required Checks stabilisieren (open)

**Mapped Issues:**
- #524: Repo-Hygiene, CI/CD Hygiene und Security Fixes (CLOSED)
- #501: Repo scan: Branch protection, secrets path, test failures (CLOSED)
- #432: Codex MCP Alignment: remove MCP_DOCKER (OPEN - parking)

**Missing Issues:**
- [ ] Required Checks Definition
- [ ] Secrets Scan Activation
- [ ] Branch Protection Final Setup

---

## Sprint 1 — Signale + frühe Observability (🚧 RE-OPEN)

**Goal:** Signale unter Last sichtbar messen, kein Blindflug

**Bereits erledigt:**
- ✅ Stateful pct_change / PriceBuffer (#345 - nicht als Issue gefunden, aber implementiert)
- ✅ Unit Tests (tests/unit/signal/test_price_buffer.py)
- ✅ Produktionsverifikation (5 Tage, 209 signals)

**Pflicht-Scope (Roadmap):**
- Signal-Metriken:
  - signals_generated_total ✅ (existiert)
  - signal_processing_latency_ms (TODO)
  - signal_errors_total (TODO)
- Prometheus Target grün (TODO)
- 1 Grafana Dashboard (Signals) (TODO)
- Burst-Replay / Stress-Input (TODO)

**Mapped Issues:**
- #595: [PAPER][HARDENING] Add contract test for signal -> db_writer -> DB (OPEN)
- #593: [PAPER][HARDENING] Prove allocation loop activity (OPEN)
- #591: [PAPER][BLOCKER] Define and fix 'stuck approvals/quotas' metric (OPEN)
- #590: [PAPER][BLOCKER] Verify order_results consumer + retention (OPEN)

**Sprint 1 Core Issues:**
- **#622:** 🎯 Sprint 1: Minimal Observability (Signals) ← START HERE
  - Metriken: latency_ms, errors_total
  - Prometheus Scrape grün
  - 1 Grafana Dashboard (Signals)
  - https://github.com/jannekbuengener/Claire_de_Binare/issues/622

- **#623:** 🎯 Sprint 1: Burst / Load / Race Conditions ← THEN THIS
  - Burst-Replay Runner
  - Signal-Engine unter Last (100+ signals/sec)
  - State-Korruption Proof (keine)
  - https://github.com/jannekbuengener/Claire_de_Binare/issues/623

**DoD (hart):**
- [ ] Signale unter Last stabil
- [ ] Latenz + Fehler sichtbar
- [ ] Keine State-Korruption
- [ ] Issues #622 + #623 geschlossen

---

## Sprint 2 — Deterministic E2E + Crash Proof (🚧 IN PROGRESS - Part 1 Done)

**Goal:** Reproduzierbarer Wahrheitsbeweis des Gesamtsystems

**Scope:**
- Deterministischer Replay Runner (Fixture) ✅ DONE
- E2E Harness mit Assertions (TODO)
- Happy Path (TODO)
- Mindestens 1 Crash-Fall (Redis down ODER DB down) (TODO)

**Mapped Issues:**
- **#620:** Sprint 2 Part 2: E2E Harness with Hard Assertions (OPEN) ✅
- **#621:** Sprint 2 Part 2: Verify order_results Truth (OPEN) ✅
- #589: [PAPER][BLOCKER] Verify auto-unwind E2E (OPEN)
- #427: 🧪 MUST: E2E Smoke Test ≥90% Pass Rate (OPEN)

**Deliverables (Part 1 DONE):**
- ✅ Fixture: tests/e2e/fixtures/mexc_btcusdt_replay.json (40 ticks, 8 signals)
- ✅ Replay Runner: tests/e2e/replay_runner.py (200 LOC, 43ms)
- ✅ Test Run Evidence: signals_generated +90 delta

**Deliverables (Part 2 TODO):**
- [ ] E2E Harness: tests/e2e/test_happy_path.py
- [ ] 5 Hard Assertions (signals, orders, results, DB)
- [ ] 1 Crash-Fall (Redis down oder DB down)
- [ ] 3× identische Runs (Determinismus-Proof)

**DoD:**
- [ ] 3 identische Runs ✅
- [ ] 1 Crash-Run dokumentiert
- [ ] Evidence Log vorhanden

**Related Issues (alt/referenziert):**
- #224: order_results Truth (nicht gefunden - ersetzt durch #621)
- #229: Harness Problem (nicht gefunden - evtl. gelöst)
- #354: Determinismus-Proof (nicht gefunden - in #620 enthalten)

---

## Sprint 3 — Observability vertiefen + Alerts (🔜 NOT STARTED)

**Goal:** Probleme sofort sichtbar und erklärbar

**Scope:**
- Metrik-Contract vollständig
- Prometheus Scrapes stabil
- Grafana Dashboards: Overview, Pipeline, Infra
- 3–5 Alerts + Runbooks

**Mapped Issues:**
- #529: Grafana Dashboards: Fehlende Metriken (CLOSED - reopen needed?)
- #338: Devil's Advocate Mode (OPEN - alignment?)

**Missing Issues:**
- [ ] Metrik-Contract Definition
- [ ] Prometheus Scrape Stability
- [ ] 3 Dashboards (Overview, Pipeline, Infra)
- [ ] Alerts + Runbooks (3–5)

**DoD:**
- [ ] Kein "No data"
- [ ] Alerts getestet (1×)
- [ ] Operator versteht Ursache in <5 Min

---

## Sprint 4 — Governance as Code (🔜 NOT STARTED)

**Goal:** Governance technisch erzwungen, nicht sozial

**Scope:**
- Forbidden Paths / Write-Zone Guard
- Secrets Scan Guard
- Policy-Check Workflow
- Merge Gates Doc
- Branch Protection final

**Mapped Issues:**
- #337: Issue Lifecycle State Machine (OPEN)
- #336: Pipeline-to-Review Bridge (OPEN)
- #335: Discussion Pipeline Output Clarity (OPEN)

**Missing Issues:**
- [ ] Forbidden Paths Guard
- [ ] Secrets Scan Guard (automated)
- [ ] Policy-Check Workflow
- [ ] Merge Gates Documentation
- [ ] Branch Protection Final

**DoD:**
- [ ] Drift technisch unmöglich
- [ ] Kein Direkt-Push
- [ ] Jeder Merge prüfbar

---

## Gate Phase — Echtgeld-Readiness (🔒 BLOCKED)

**Voraussetzungen:**
- [ ] Alle Sprints DONE
- [ ] Keine offenen P0/P1 Issues

**Prüfungen:**
- [ ] 72h Soak Test
- [ ] Chaos Drill
- [ ] Operator Drill
- [ ] Go / No-Go Review

**Mapped Issues:**
- #427: E2E Smoke Test ≥90% Pass Rate (Pre-Soak Gate)

---

## Parked / Out-of-Scope

**Issues nicht in Roadmap:**
- #562: Emoji Detection Alert (parked)
- #520: DB driver modernisieren (parked)
- #500: Isolated cdb_autoclaude stack (parked)
- #498: Review Gordon Docker setup (parked)
- #431: Agent PowerShell Toolchain (parked)
- #414: Raise coverage threshold (parked)
- #334: BSDE/HJB Framework (Deferred M10+)
- #333: Minimum Viable Decision Engine (M8/M9)
- #332: Advanced control theory decision (M8/M9)
- #328: Governance Audit Q1 2026 (in-progress, separate track)
- #215: E1–E4 Integration (roter_faden005, separate track)
- #211: Multi-Asset Portfolio Management (GEMINI, M3-M7)
- #207: Backtesting Framework (GEMINI, M5-M9)
- #206: Database Schema Migrations (CODEX, M5-M9)

---

## Actions Required (Next Steps)

### Immediate (Sprint 1 Completion):
1. ✅ Create Issue #622: Minimal Observability (Signals)
2. ✅ Create Issue #623: Burst / Load / Race Conditions
3. 🚧 Begin Sprint 1 work: #622 → #623

### Sprint 2 Part 2 (After Sprint 1):
4. Work on #620: E2E Harness with Assertions
5. Work on #621: order_results Truth Verification
6. Add Crash-Fall (Redis down OR DB down)
7. Prove 3× determinism

### Future Sprints:
8. Define Sprint 3 Epic + Sub-Issues
9. Define Sprint 4 Epic + Sub-Issues
10. Gate Phase preparation

---

**Status:** ✅ Mapping Complete
**Next:** Create missing Sprint 1 issues (#NEW-1, #NEW-2)
