# Disaster Recovery - Docker Reinstallation

**Location:** `Claire_de_Binare_Docs/knowledge/operations/disaster_recovery/`  
**Last Updated:** 2025-12-31  
**Status:** Production-Ready

---

## 📚 Dokumentation

| File | Beschreibung | Verwendung |
|------|--------------|------------|
| **QUICK_START.md** | 🚀 3-Schritte Schnellanleitung | Nach Docker Neuinstallation |
| **RESTORE_GUIDE.md** | 📖 Ausführliche Schritt-für-Schritt Anleitung | Detaillierte Restore-Prozedur |
| **restore_volumes.ps1** | ⚡ Automatisches Restore-Script | PowerShell ausführen |
| **verify_restore.ps1** | ✅ Verifications-Script | Nach Restore zur Validierung |

---

## 🎯 Verwendungszweck

Diese Dokumentation beschreibt den **Docker Volume Backup und Restore Prozess** für CDB (Claire de Binare).

**Anwendungsfälle:**
- Docker Desktop Neuinstallation
- Migration auf neuen Rechner
- Disaster Recovery nach System-Crash
- Entwicklungsumgebung Reset

---

## 💾 Was wird gesichert

### Kritische Daten:
- ✅ **Grafana Dashboards** (8 Dashboards, ~109MB)
  - System Performance, Signal Engine, Risk Manager
  - Paper Trading, Execution, Database, HITL Control
  - Dark Mode Theme
- ✅ **Redis Datenbank** (~85KB)
  - Session State, Cache, Pub/Sub Messages
- ✅ **Prometheus Metriken** (~2MB)
  - Zeitreihen-Daten, Performance Metrics
- ✅ **Loki Logs** (~671B)
  - Aggregierte Log-Daten
- ✅ **Claude Memory** (~3KB)
  - MCP Server Memory State

### Konfiguration:
- ✅ `.env` File
- ✅ `.secrets.example/` Templates
- ✅ Container/Volume/Network Listen

### PostgreSQL:
- ⚠️ **Volume bleibt normalerweise erhalten** bei Docker Neuinstallation
- Bei Migration: Manueller Export/Import empfohlen
- Bei Datenverlust: Fresh Init mit Schema

### Secrets (außerhalb Docker):
- ✅ Bleiben erhalten: `C:\Users\janne\Documents\.secrets\.cdb\`
- Enthalten: MEXC API Keys, Grafana/Postgres/Redis Passwords

---

## 🚀 Quick Start (TL;DR)

**Nach Docker Neuinstallation:**

```powershell
# 1. Restore (2-3 Min)
cd D:\Dev\Backups\docker_reinstall_YYYYMMDD_HHMMSS
.\restore_volumes.ps1

# 2. Stack starten (30-60 Sek)
cd D:\Dev\Workspaces\Repos\Claire_de_Binare
make docker-up

# 3. Verifizieren
.\verify_restore.ps1
```

**Details:** Siehe [QUICK_START.md](./QUICK_START.md)

---

## 📋 Backup-Prozess

### Manuelles Backup erstellen:

```powershell
# 1. Backup-Verzeichnis erstellen
$BACKUP_DIR = "D:\Dev\Backups\docker_backup_$(Get-Date -Format 'yyyyMMdd_HHmmss')"
mkdir $BACKUP_DIR

# 2. Volumes sichern
docker run --rm -v claire_de_binare_redis_data:/data -v ${BACKUP_DIR}:/backup alpine tar czf /backup/redis_data.tar.gz -C /data .
docker run --rm -v claire_de_binare_grafana_data:/data -v ${BACKUP_DIR}:/backup alpine tar czf /backup/grafana_data.tar.gz -C /data .
docker run --rm -v claire_de_binare_prom_data:/data -v ${BACKUP_DIR}:/backup alpine tar czf /backup/prometheus_data.tar.gz -C /data .
docker run --rm -v claire_de_binare_loki_data:/data -v ${BACKUP_DIR}:/backup alpine tar czf /backup/loki_data.tar.gz -C /data .
docker run --rm -v claude-memory:/data -v ${BACKUP_DIR}:/backup alpine tar czf /backup/claude_memory.tar.gz -C /data .

# 3. Config sichern
Copy-Item D:\Dev\Workspaces\Repos\Claire_de_Binare\.env ${BACKUP_DIR}\.env_backup

# 4. Dokumentieren
docker ps -a --format "{{.Names}}\t{{.Image}}\t{{.Status}}" > ${BACKUP_DIR}\container_list.txt
docker volume ls > ${BACKUP_DIR}\volume_list.txt
docker network ls > ${BACKUP_DIR}\network_list.txt
```

### Automatisches Backup (TODO):
- Cronjob/Task Scheduler für tägliche Backups
- Retention Policy (z.B. 7 Tage behalten)
- Backup-Validierung

---

## 🔧 Restore-Prozess

### Automatisch (empfohlen):
```powershell
.\restore_volumes.ps1
```

### Manuell:
Siehe [RESTORE_GUIDE.md](./RESTORE_GUIDE.md) für alle Commands

---

## ✅ Verifikation

### Nach Restore ausführen:
```powershell
.\verify_restore.ps1
```

### Manuelle Checks:
```powershell
# Docker Version
docker --version
docker compose version

# Volumes existieren
docker volume ls

# Container laufen
docker ps

# Grafana Dashboards
# → http://localhost:3000

# Redis Daten
docker exec cdb_redis redis-cli DBSIZE
```

---

## 🚨 Bekannte Probleme & Lösungen

### Problem: PostgreSQL Mount-Fehler
**Symptom:**
```
error mounting "...schema.sql": not a directory
```

**Ursache:** Alte absolute Pfade in Compose Files (C:\Users\... statt D:\Dev\...)

**Lösung:**
1. Prüfe `infrastructure/compose/base.yml`
2. Entferne oder update absolute Pfade
3. Volume-Namen sollten ausreichen

### Problem: Container crashen nach Restore
**Check:**
```powershell
docker compose logs <container_name>
```

**Häufige Ursachen:**
- Falsche Pfade in .env
- Fehlende Secrets
- Inkompatible Volume-Daten

### Problem: Grafana zeigt keine Dashboards
**Lösung:**
```powershell
docker volume rm claire_de_binare_grafana_data
docker volume create claire_de_binare_grafana_data
docker run --rm -v claire_de_binare_grafana_data:/var/lib/grafana -v D:\Dev\Backups\...\grafana_data:/backup alpine cp -r /backup/. /var/lib/grafana/
docker compose restart cdb_grafana
```

---

## 📊 Backup-Historie

| Datum | Event | Backup Location | Size | Status |
|-------|-------|----------------|------|--------|
| 2025-12-31 | Docker Neuinstallation | `docker_reinstall_20251231_075507` | 112MB | ✅ Erfolgreich |

---

## 🔗 Related Documentation

- [WORKSPACE_LAYOUT.md](../WORKSPACE_LAYOUT.md) - Workspace-Struktur
- [Stack Lifecycle](../../../docs/STACK_LIFECYCLE.md) - Docker Stack Management
- [Setup Guide](../../../docs/SETUP_GUIDE.md) - Initial Setup

---

## 📝 Maintenance

**Empfohlene Backup-Frequenz:**
- **Täglich:** Automatisches Volume Backup (TODO)
- **Vor Major Updates:** Manuelles Backup
- **Vor Docker Neuinstallation:** Manuelles Backup (wie hier dokumentiert)

**Retention:**
- Lokale Backups: 7 Tage
- Kritische Backups: 30 Tage
- Vor Major Releases: Permanent archivieren

---

**Erstellt:** 2025-12-31  
**Autor:** Claude (Disaster Recovery Documentation)  
**Basierend auf:** Docker Reinstall 2025-12-31 07:55
