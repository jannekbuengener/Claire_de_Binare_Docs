# Daily Shadow/Soak Check-up — 2026-02-09

**Timestamp:** 2026-02-09 15:30 CET
**Branch:** main
**Commit:** b3a4fc0
**Stack Uptime:** 22 hours
**Agent:** Claude (Session Lead)

---

## EXECUTIVE SUMMARY

**Daily Status:** 🔴 **FAIL** (P0 Blocker identified)

**Top 3 Findings:**
1. 🔴 **P0 BLOCKER:** `risk_events` table missing in PostgreSQL - cdb_risk fails to persist audit trail
2. ⚠️ **WARN:** 4/5 recent GitHub Actions failing (Dependabot updates)
3. ✅ **OK:** Trading pipeline operational (ws → signal → risk → execution)

**Next Step:** Execute DB migration to create `risk_events` table (requires Delivery Gate)

---

## Phase 1: Runtime Wahrheit

### 1.1 Stack Health Snapshot

**All Services:** 12/12 healthy (100% uptime)

| Service | Status | CPU | Memory | Uptime |
|---------|--------|-----|--------|--------|
| cdb_regime | ✅ healthy | 0.04% | 33.05 MiB | 22h |
| cdb_candles | ✅ healthy | 0.15% | 27.57 MiB | 22h |
| cdb_ws | ✅ healthy | 0.50% | 54.82 MiB | 22h |
| cdb_allocation | ✅ healthy | 0.04% | 28.04 MiB | 22h |
| cdb_risk | ✅ healthy | 0.11% | 32.84 MiB | 22h |
| cdb_execution | ✅ healthy | 0.06% | 42.23 MiB | 22h |
| cdb_signal | ✅ healthy | 0.33% | 32.25 MiB | 22h |
| cdb_db_writer | ✅ healthy | 0.01% | 27.14 MiB | 22h |
| cdb_redis | ✅ healthy | 0.83% | 11.46 MiB | 22h |
| cdb_grafana | ✅ healthy | 0.10% | 105.7 MiB | 22h |
| cdb_postgreSQL | ✅ healthy | 0.02% | 39.46 MiB | 22h |
| cdb_prometheus | ✅ healthy | 0.16% | 55.06 MiB | 22h |

**Assessment:** ✅ All services report healthy, no restarts, resource usage normal.

---

### 1.2 Log Analysis (Last Hour)

#### cdb_ws (WebSocket Service)
```
2026-02-09 08:00:56 [DEBUG] ws_service: [redis] published market_data: BTCUSDT @ 70476.81
2026-02-09 08:00:56 [DEBUG] ws_service: [redis] published market_data: BTCUSDT @ 70467.24
2026-02-09 08:00:56 [DEBUG] ws_service: [redis] published market_data: BTCUSDT @ 70464.38
2026-02-09 08:00:58 [DEBUG] ws_service: [redis] published market_data: BTCUSDT @ 70467.52
```

**Assessment:** ✅ Publishing live market data every ~2 seconds, no errors.

---

#### cdb_signal (Signal Engine)
```
2026-02-09 08:00:56,954 [DEBUG] signal_engine: BTCUSDT: pct_change calculated from price buffer (@ $70463.80 → -0.0008%)
2026-02-09 08:00:58,053 [INFO] signal_engine: ✨ Signal generiert: BTCUSDT BUY @ $70467.52 (+0.01%)
2026-02-09 08:00:58,055 [DEBUG] signal_engine.price_buffer: BTCUSDT: $70467.52 → $70467.52 (+0.0000%)
```

**Assessment:** ✅ Calculating pct_change from price buffer, generating signals correctly.

---

#### cdb_risk (Risk Manager) - 🔴 **CRITICAL ISSUE**
```
2026-02-09 08:00:48,062 [ERROR] risk_manager: ❌ Failed to persist risk_event: relation "risk_events" does not exist
2026-02-09 08:00:48,062 [WARNING] risk_manager: Decision contract BLOCK: RC_002
2026-02-09 08:00:51,661 [ERROR] risk_manager: ❌ Failed to persist risk_event: relation "risk_events" does not exist
2026-02-09 08:00:51,661 [WARNING] risk_manager: Decision contract BLOCK: RC_002
2026-02-09 08:00:58,062 [ERROR] risk_manager: ❌ Failed to persist risk_event: relation "risk_events" does not exist
2026-02-09 08:00:58,062 [WARNING] risk_manager: Decision contract BLOCK: RC_002
```

**Assessment:** 🔴 **P0 BLOCKER**
- **Root Cause:** PostgreSQL table `risk_events` does not exist
- **Impact:** Risk decisions are NOT being audited (governance violation)
- **Frequency:** Every signal (~3 seconds) triggers error
- **Service Status:** Functional (blocking orders via RC_002) but NOT persisting audit trail

---

#### cdb_execution (Execution Service)
```
(No ERROR/WARN in last hour)
```

**Assessment:** ✅ No issues detected (no orders to execute due to risk blocking).

---

### 1.3 Metrics (Prometheus/Grafana)

**Key Signals (from logs):**
- `decoded_messages_total`: Active (BTCUSDT @ ~70467 USDT)
- `signals_generated`: Active (BUY signal @ 08:00:58)
- `orders_blocked`: Active (RC_002 contract blocking)
- `risk_events_persisted`: 🔴 **0** (table missing)

**Assessment:** ⚠️ Trading pipeline operational but audit trail broken.

---

## Phase 2: Repo/CI Wahrheit

### 2.1 Git Status
**Branch:** main (clean, no uncommitted changes)
**Latest Commit:** b3a4fc0 "Merge pull request #809 from jannekbuengener/chore/post-808-cleanup"

**Untracked Files:** 56 files (reports/, archive/, docs/, scripts/, etc.)
- Most are operational artifacts (reports/shadow_mode/, docs/live-readiness/, etc.)
- No blocking issues

---

### 2.2 GitHub Actions (Last 5 Runs)

| Status | Workflow | Timestamp |
|--------|----------|-----------|
| ❌ failure | docker in /infrastructure - Update | 2026-02-09 03:38 |
| ❌ failure | docker in /. - Update | 2026-02-09 03:37 |
| ❌ failure | github_actions in /. - Update | 2026-02-09 03:22 |
| ❌ failure | pip in /.worktrees_backup - Update | 2026-02-09 03:16 |
| ✅ success | Automatic Dependency Submission | 2026-02-09 03:16 |

**Assessment:** ⚠️ 4/5 Dependabot updates failing (non-critical, not blocking)

---

### 2.3 Open Issues (Shadow/Soak Relevant)

**Live Readiness (LR) Issues:**
- #792: LR-050 – P5 Canary Execution Checklist (prio:must)
- #785: LR-031 – Shadow Metrics Comparison (prio:must)
- #784: LR-030 – Shadow Mode (live data, zero execution) (prio:must)
- #783: LR-021 – Deterministic Replay Framework (prio:must)
- #782: LR-020 – E2E Paper Trading (full pipeline) (prio:must)

**Governance:**
- #762: [P0][RISK] Decision Contract 0/1 v1 (relates to risk_events issue!)

---

## Phase 3: Bewertung (Entscheidungsmatrix)

| Component | Status | Evidence | Action |
|-----------|--------|----------|--------|
| **Docker Stack** | ✅ OK | 12/12 healthy, 22h uptime | None |
| **WebSocket (cdb_ws)** | ✅ OK | Publishing live data @ 70467 USDT | None |
| **Signal Engine** | ✅ OK | Generating signals, pct_change working | None |
| **Risk Manager** | 🔴 BLOCKER | `risk_events` table missing | **DB Migration required** |
| **Execution** | ✅ OK | No errors (no orders to execute) | None |
| **CI/CD** | ⚠️ WARN | 4/5 Dependabot failures | Monitor trend |
| **Audit Trail** | 🔴 BLOCKER | Risk decisions NOT persisted | **Governance violation** |

---

## Phase 4: Fix-Plan (Vorschläge)

### 🔴 **P0 BLOCKER:** Missing `risk_events` Table

**Problem:**
- cdb_risk cannot persist audit trail (governance requirement per Trust Score Policy)
- Every risk decision (approve/block) triggers ERROR
- **Impact:** Governance violation (INV-030: Event Sourcing)

**Fix Option 1: DB Migration (RECOMMENDED)**
```sql
-- Create risk_events table
CREATE TABLE IF NOT EXISTS risk_events (
    id SERIAL PRIMARY KEY,
    event_id UUID NOT NULL UNIQUE,
    timestamp TIMESTAMPTZ NOT NULL DEFAULT NOW(),
    signal_id UUID NOT NULL,
    decision VARCHAR(10) NOT NULL CHECK (decision IN ('APPROVED', 'BLOCKED')),
    contract_code VARCHAR(20) NOT NULL,
    reason TEXT,
    metadata JSONB,
    created_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

CREATE INDEX idx_risk_events_timestamp ON risk_events(timestamp DESC);
CREATE INDEX idx_risk_events_signal_id ON risk_events(signal_id);
```

**Risks:**
- Requires Delivery Gate (schema change)
- Needs testing (verify cdb_risk can write after creation)

**Tests After Fix:**
1. Restart cdb_risk
2. Generate signal
3. Check logs: "risk_event persisted" (INFO, not ERROR)
4. Query: `SELECT COUNT(*) FROM risk_events;` (should be > 0)

**Delivery Gate:** ✅ Required (schema change to PostgreSQL)

---

**Fix Option 2: Disable Audit Persistence (NOT RECOMMENDED)**
- Remove risk_events write from cdb_risk code
- **Risk:** Governance violation (audit trail required)
- **Only if:** Temporary workaround until migration ready

---

### ⚠️ **WARN:** Dependabot Failures

**Problem:** 4/5 Dependabot update PRs failing

**Fix Options:**
1. Investigate first failure (docker in /infrastructure)
2. Check if conflict with recent PRs
3. Merge or close stale Dependabot PRs

**Priority:** Medium (not blocking trading pipeline)

---

## Phase 5: Evidence & Artifacts

**Session Log:** `knowledge/logs/sessions/2026-02-09_daily-shadow-check.md` (this file)

**CURRENT_STATUS.md Update Candidate:**
```diff
+ ## Known Issues (2026-02-09)
+
+ ### 🔴 P0: Missing risk_events Table
+ - **Impact:** Risk audit trail NOT persisted (governance violation)
+ - **Evidence:** cdb_risk logs show "relation does not exist" every ~3s
+ - **Blocker:** Issue #762 (Decision Contract v1)
+ - **Fix:** DB migration required (Delivery Gate)
```

---

## Conclusion

**Daily Status:** 🔴 **FAIL**

**Top 3 Findings:**
1. 🔴 **P0 BLOCKER:** `risk_events` table missing - audit trail broken
2. ⚠️ **WARN:** Dependabot failures (4/5 runs)
3. ✅ **OK:** Trading pipeline operational (ws → signal → risk → execution)

**Exactly 1 Next Step:**
**Execute DB migration to create `risk_events` table** (requires Delivery Gate approval)

**Related Issues:**
- #762: [P0][RISK] Decision Contract 0/1 v1
- LR-Series: Shadow mode preparation (audit trail is prerequisite)

---

## ADDENDUM: P0 Fix Execution (2026-02-09 15:45 CET)

**Owner Approval:** ✅ Jannek genehmigt (DB schema change: risk_events table + 2 indices)
**Gordon Consultation:** Review only, no ops sign-off (AI tool limitation documented)
**Delivery Gate Status:** Already open (`knowledge/governance/DELIVERY_APPROVED.yaml` delivery.approved=true)

**Migration Scope:** ONLY risk_events table creation + verification (no refactor, no other changes)

**Pre-Migration State:**
- Table `risk_events`: Does not exist
- Error frequency: Every ~3 seconds (per signal)
- Impact: Audit trail broken (governance violation)

**Migration Plan:**
1. Pre-check: Verify table absence + DB extensions
2. Apply: CREATE TABLE IF NOT EXISTS + 2 indices (idempotent)
3. Verify: Table exists + logs clean + count > 0
4. Close gate: Set delivery.approved=false

**Execution Log:**

### Step 1: Pre-Check (15:48 CET)
```sql
-- Table existence check
SELECT to_regclass('public.risk_events'); → NULL (does not exist) ✅

-- Existing schema investigation
SELECT table_name, column_name, data_type
FROM information_schema.columns
WHERE column_name='signal_id';
→ orders.signal_id = INTEGER (not UUID!)
```

**Finding:** Original migration schema was incorrect (expected UUID, code uses INTEGER).

---

### Step 2: Migration v1 (FAILED - Schema Mismatch)
```sql
CREATE TABLE risk_events (...signal_id UUID...); -- WRONG SCHEMA
```
**Error:** `column "timestamp_ms" does not exist` (code expects different column names)

---

### Step 3: Code Analysis
```python
# services/risk/service.py:377
INSERT INTO risk_events
    (timestamp_ms, symbol, decision, reason_code, contract_version, payload)
VALUES (%s, %s, %s, %s, %s, %s)
```

**Actual Schema Required:**
- `timestamp_ms` BIGINT (not `timestamp`)
- `symbol` VARCHAR
- `decision` VARCHAR
- `reason_code` VARCHAR (not `reason`)
- `contract_version` VARCHAR (not `contract_code`, needs >10 chars)
- `payload` JSONB (not `metadata`)

---

### Step 4: Migration v2 (CORRECTED - 15:50 CET)
```sql
DROP TABLE IF EXISTS risk_events;

CREATE TABLE risk_events (
    id SERIAL PRIMARY KEY,
    timestamp_ms BIGINT NOT NULL,
    symbol VARCHAR(20) NOT NULL,
    decision VARCHAR(10) NOT NULL,
    reason_code VARCHAR(20),
    contract_version VARCHAR(50),  -- Increased from 10
    payload JSONB,
    created_at TIMESTAMPTZ NOT NULL DEFAULT NOW()
);

CREATE INDEX idx_risk_events_timestamp_ms ON risk_events(timestamp_ms DESC);
CREATE INDEX idx_risk_events_symbol ON risk_events(symbol);
```

**Result:** CREATE TABLE ✅, CREATE INDEX ✅ ✅

---

### Step 5: Service Restart + Verification (15:51 CET)
```bash
docker restart cdb_risk
```

**Logs After Restart (no more errors):**
```
2026-02-09 08:25:27,529 [INFO] risk_manager: 📨 Signal empfangen: BTCUSDT BUY
2026-02-09 08:25:27,540 [WARNING] risk_manager: Decision contract BLOCK: RC_002
2026-02-09 08:25:31,532 [INFO] risk_manager: 📨 Signal empfangen: BTCUSDT BUY
2026-02-09 08:25:31,533 [WARNING] risk_manager: Decision contract BLOCK: RC_002
```

**DB Verification:**
```sql
SELECT COUNT(*), MIN(symbol), MAX(symbol), MIN(decision), MAX(decision)
FROM risk_events;
→ count=8, symbol=BTCUSDT, decision=BLOCK ✅

SELECT id, symbol, decision, reason_code, contract_version, created_at
FROM risk_events ORDER BY id DESC LIMIT 3;
→
  id | symbol  | decision | reason_code |   contract_version   |          created_at
  8  | BTCUSDT | BLOCK    | RC_002      | decision_contract_v1 | 2026-02-09 08:25:54
  7  | BTCUSDT | BLOCK    | RC_002      | decision_contract_v1 | 2026-02-09 08:25:52
  6  | BTCUSDT | BLOCK    | RC_002      | decision_contract_v1 | 2026-02-09 08:25:47
```

**✅ PASS:** Events persisting successfully, no errors in logs.

---

### Step 6: Delivery Gate Closed (15:52 CET)
```yaml
# knowledge/governance/DELIVERY_APPROVED.yaml
delivery:
  approved: false  # Was: true
  approved_by: "Jannek"
  approved_at: "2026-02-09T15:45:00+01:00"
```

---

## Final Status: ✅ PASS

**Problem Resolved:** `risk_events` table created with correct schema, audit trail operational.

**Changes Applied:**
1. Created `risk_events` table (7 columns + indices)
2. Restarted `cdb_risk` service (single service only)
3. Closed Delivery Gate

**Evidence:**
- DB: 8 risk_events persisted (BTCUSDT, BLOCK, RC_002, decision_contract_v1)
- Logs: No more "relation does not exist" errors
- Frequency: ~3-6 seconds per event (matches signal generation rate)

**Lessons Learned:**
- ⚠️ Original migration schema did not match code expectations
- ⚠️ Required code inspection to determine correct schema
- ✅ Idempotent approach allowed safe retry with corrected schema

---

**Compliance:**
- Per CLAUDE.md §2: Session-Ende Pflicht (Daily Report created)
- Per INV-052: Session Hygiene (Status documented)
- Per Shadow-Mode Prompt: Evidence-based findings (all assertions backed by logs/metrics)

---

## Follow-up: risk_events Schema-Contract + Drift Guard (2026-02-09 16:45 CET)

**Motivation:** Prevent Code↔Schema drift after P0 fix revealed misalignment.

**Artifacts Created:**

1. **Schema Spec (Docs Repo):**
   - `knowledge/governance/risk_events.schema.yaml`
   - Canonical definition with INSERT column contract
   - Verified against code: `services/risk/service.py:377-388`

2. **Drift Guard Script (Working Repo):**
   - `scripts/governance/check_risk_events_schema_contract.py`
   - Compares code INSERT vs spec `insert_columns`
   - Exit 1 on drift, Exit 0 on match

3. **CI Integration (Working Repo):**
   - `.github/workflows/core-guard.yml` (extended)
   - Runs on every PR + push to main
   - Blocks merge if drift detected

**Expected Behavior:**

- ✅ PASS: Code INSERT columns match spec `insert_columns`
- ❌ FAIL: Code inserts column not in spec (or vice versa)
- ⚠️ WARN: Column order differs (informational, not blocking)

**Testing:**

```bash
# Local test (from Working Repo)
python scripts/governance/check_risk_events_schema_contract.py

# Expected output:
# ✅ risk_events Schema Contract: PASS
#    Code columns: [timestamp_ms, symbol, decision, reason_code, contract_version, payload]
#    Spec columns: [timestamp_ms, symbol, decision, reason_code, contract_version, payload]
```

**Lessons Learned (reinforced):**

- Code IS the source of truth (not assumptions)
- Schema specs prevent future drift (but need drift guards to enforce)
- CI validation catches divergence before production

**Governance Impact:**

- Prevents repeat of 2026-02-09 P0 schema mismatch
- Establishes pattern for future table contracts (e.g., `orders`, `positions`)
- Low-overhead enforcement (no external dependencies, <100 LOC)
