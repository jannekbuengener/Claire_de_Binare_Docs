# Session Log: Docker Secrets Blueprint Implementation

**Datum:** 2025-12-29 02:00 - 03:25 CET
**Session Lead:** Claude Opus 4.5
**Teilnehmer:** Jannek

---

## Ziel

Implementierung des Docker Secrets Management Blueprints für produktionsreife Secret-Handhabung. Upgrade von Environment-Variablen zu `/run/secrets/` file-basiertem Ansatz.

---

## Kontext

Nach einem Secret-Leak in Git-History war eine permanente Lösung erforderlich. Das Compass-Blueprint-Dokument definierte die Best Practices:
- Docker Compose `secrets:` Direktive
- `_FILE` Pattern für offizielle Images
- Gitleaks Pre-commit Hooks
- Single Source of Truth: `~/Documents/.secrets/.cdb/`

---

## Durchgeführte Arbeiten

### 1. Docker Compose Secrets Architecture

**base.yml:**
```yaml
secrets:
  redis_password:
    file: ${SECRETS_PATH}/REDIS_PASSWORD
  postgres_password:
    file: ${SECRETS_PATH}/POSTGRES_PASSWORD
  grafana_password:
    file: ${SECRETS_PATH}/GRAFANA_PASSWORD
```

**Pattern nach Image-Typ:**
| Service | Pattern | Beispiel |
|---------|---------|----------|
| PostgreSQL | Native `_FILE` | `POSTGRES_PASSWORD_FILE: /run/secrets/postgres_password` |
| Grafana | Native `__FILE` | `GF_SECURITY_ADMIN_PASSWORD__FILE: /run/secrets/grafana_password` |
| Redis | Command substitution | `--requirepass $(cat /run/secrets/redis_password)` |
| Python Services | Entrypoint export | `export POSTGRES_PASSWORD=$(cat /run/secrets/...)` |

### 2. Entrypoint Pattern für Python Services

```yaml
entrypoint: ["sh", "-c", "export REDIS_PASSWORD=$(cat /run/secrets/redis_password) && export POSTGRES_PASSWORD=$(cat /run/secrets/postgres_password) && exec python -u service.py"]
```

### 3. Security Hardening

- `.gitignore` erweitert mit Secrets-Patterns
- `.dockerignore` mit Secrets-Patterns
- Gitleaks Pre-commit Hook in `.pre-commit-config.yaml`
- `.secrets.example/` für Developer Onboarding

### 4. Init-Scripts

- `stack_up.ps1`: `Set-SecretsPath` Funktion für `SECRETS_PATH` Environment Variable
- `init-secrets.ps1`: Generiert sichere Secrets mit `WriteAllBytes` (CRLF-safe)

---

## Probleme & Lösungen

### Problem 1: Windows Symlink Permissions
**Symptom:** `FATAL: Cannot create symlink!`
**Ursache:** Windows benötigt Developer Mode für Symlinks
**Lösung:** Ersetzt durch `SECRETS_PATH` Environment Variable Interpolation

### Problem 2: YAML Multiline Command Syntax
**Symptom:** Redis startete ohne Passwort
**Ursache:** YAML `>` Multiline-Syntax brach Shell-Commands
**Lösung:** Array-Format `["sh", "-c", "..."]` statt Multiline

### Problem 3: CRLF in Secret-Dateien (ROOT CAUSE)
**Symptom:** `FATAL: password authentication failed for user "claire_user"`
**Ursache:** Windows schreibt Dateien mit `\r\n`. PostgreSQL initialisierte mit `Passwort\r\n`, Services lasen `Passwort` → Mismatch
**Diagnose:** `od -c` zeigte `\r\n` am Ende der Secret-Datei
**Lösung:**
1. Secret-Dateien ohne Trailing Newline neu geschrieben
2. `init-secrets.ps1` auf `WriteAllBytes` umgestellt

### Problem 4: db_writer Wrong Filename
**Symptom:** `ModuleNotFoundError: No module named 'service'`
**Ursache:** Entrypoint nutzte `service.py` statt `db_writer.py`
**Lösung:** Korrekter Dateiname in Entrypoint

---

## Ergebnis

**Alle 10 Container Healthy:**
```
cdb_redis           Up (healthy)
cdb_postgres        Up (healthy)
cdb_prometheus      Up (healthy)
cdb_grafana         Up (healthy)
cdb_ws              Up (healthy)
cdb_signal          Up (healthy)
cdb_risk            Up (healthy)
cdb_execution       Up (healthy)
cdb_db_writer       Up (healthy)
cdb_paper_runner    Up (healthy)
```

---

## Commits

| SHA | Message |
|-----|---------|
| `ce729cb` | feat(security): implement Docker Secrets Blueprint |
| `f5e86c4` | fix(security): upgrade vulnerable dependencies |

---

## Geänderte Dateien

```
 .dockerignore                            |  16 +++
 .gitignore                               |  28 ++++-
 .pre-commit-config.yaml                  |  20 +++-
 .secrets.example/GRAFANA_PASSWORD        |   1 +
 .secrets.example/POSTGRES_PASSWORD       |   1 +
 .secrets.example/REDIS_PASSWORD          |   1 +
 infrastructure/compose/base.yml          |  37 ++++--
 infrastructure/compose/dev.yml           | 118 +++++++------------
 infrastructure/scripts/init-secrets.ps1  |  82 +++++++++++++
 infrastructure/scripts/stack_up.ps1      | 189 ++++++++++++++++++++-----------
 requirements-dev.txt                     |   2 +-
```

---

## Dependabot Fixes

| Package | Old | New | CVE |
|---------|-----|-----|-----|
| black | 23.12.1 | 25.12.0 | ReDoS |
| werkzeug | (unpinned) | >=3.1.4 | Debugger RCE, safe_join bypass |

---

## Learnings

1. **CRLF ist Gift für Docker Secrets** - Windows-Zeilenenden brechen Authentifizierung
2. **YAML Array-Format ist robuster** - Multiline `>` Syntax ist fehleranfällig für Shell-Commands
3. **`_FILE` Pattern ist Standard** - Offizielle Images (Postgres, Grafana) unterstützen es nativ
4. **Volumes speichern Passwörter** - Bei Passwort-Änderung: `docker compose down -v`

---

## Nächste Schritte

- [ ] Dependabot-Alerts nach Rescan prüfen
- [ ] SOPS + age für verschlüsselte Secrets in Git evaluieren (optional)
- [ ] TLS-Overlay für Redis/Postgres testen

---

## Evidence

**Docker Health Snapshot:** 2025-12-29T02:13:40 CET
**Git Branch:** main
**Commit:** f5e86c4
