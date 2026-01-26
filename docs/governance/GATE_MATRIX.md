# GATE_MATRIX (Phase 0)

Context
- Repo: Claire_de_Binare_Docs
- Issue: #670 (Execution Dashboard)
- Scope: Phase 0 gate/control-plane mapping (read-only)

Legend
- OPEN: gate allows progression
- PARTIAL: policy defined but enforcement or metadata incomplete
- CLOSED: gate blocks progression

Sources
- knowledge/governance/DELIVERY_APPROVED.yaml
- knowledge/CURRENT_STATUS.md
- knowledge/operating_rules/ci_cd/CI_PIPELINE_GUIDE.md
- knowledge/governance/ISSUE_AND_BRANCH_LIFECYCLE.md
- knowledge/governance/CDB_GOVERNANCE.md
- knowledge/governance/CDB_AGENT_POLICY.md
- knowledge/SYSTEM_INVARIANTS.md
- knowledge/governance/CDB_RL_SAFETY_POLICY.md
- Issue #656, #657, #661, #670 (GitHub)

Gate Matrix
| Gate | Purpose | Input | Output/Check | Opens | Blocks | Owner | Status | Evidence |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Delivery Gate (DELIVERY_APPROVED.yaml) | Allow code/infra mutation + Delivery Mode | delivery.approved flag | CI delivery-gate check | Delivery Mode + merge eligibility | Code/infra mutation when false/missing | Human (User) | PARTIAL | knowledge/governance/DELIVERY_APPROVED.yaml |
| CI Required Checks | Quality/security gates for PRs | GitHub Actions workflows | Required checks: delivery-gate, gitleaks, e2e | PR merge when green | PR merge when failing | CI/System | CLOSED | knowledge/CURRENT_STATUS.md; knowledge/operating_rules/ci_cd/CI_PIPELINE_GUIDE.md |
| Branch Protection | Enforce PR-only + required checks | GitHub branch protection settings | PR required; checks required | Enforced PR flow | Direct pushes to main | Human (User) | CLOSED | knowledge/CURRENT_STATUS.md |
| Review Gate | Require review + lifecycle compliance | PR review + issue/branch lifecycle | Review before merge | Merge after review | Unreviewed changes | Human (User)/Reviewers | PARTIAL | knowledge/governance/ISSUE_AND_BRANCH_LIFECYCLE.md; knowledge/governance/CDB_GOVERNANCE.md; knowledge/CURRENT_STATUS.md |
| Metrics Baseline (#656) | Observability baseline (No Data resolved) | Grafana/Prometheus metrics | Baseline ready | Phase B safety/test tasks | Phase B tasks | Human (Team) | CLOSED | Issue #656; Issue #670 |
| Kill Switch (#657) | Verified kill switch | Kill switch metrics + verification | Verifiable stop of order flow | Operator drills | Drills until verified | Human (Team) | CLOSED | Issue #657; knowledge/governance/CDB_RL_SAFETY_POLICY.md |
| Chaos/Drills Gate (#661) | Stress/chaos only after foundations | Phase A+B complete + kill switch verified | Allow drills/chaos | Phase C | Chaos/stress before A+B | Human (Team) | CLOSED | Issue #670 |

Notes
- Status reflects documented evidence only; no runtime verification performed.
- No gate changes executed in Phase 0.
