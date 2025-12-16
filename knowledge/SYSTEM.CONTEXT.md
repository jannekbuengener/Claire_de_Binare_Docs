---
relations:
  role: doc
  domain: knowledge
  upstream: []
  downstream: []
  status: active
  tags: [system, context, runtime, environment, agents]
---
# SYSTEM.CONTEXT
**Runtime & Environment Context**

Version: 1.1  
Status: Non-Governance / Read-Only  
Änderungsfrequenz: sehr selten

---

## 1. Zweck & Abgrenzung

Diese Datei definiert den **technischen Laufzeit- und Umweltkontext**
des Projekts *Claire de Binare*.

Sie dient als **statische Referenz** für:
- Agenten
- Modelle
- Infrastruktur- und Ausführungsannahmen

Diese Datei ist ausdrücklich **nicht**:
- ❌ Governance
- ❌ Entscheidungs- oder Policy-Dokument
- ❌ Memory / Wissensspeicher
- ❌ Session- oder Status-Log

Sie beschreibt **Rahmenbedingungen**, keine Entscheidungen.

---

## 2. Schreib- & Nutzungsregeln (verbindlich)

### Schreibrechte
- ❌ Keine Agenten-Writes
- ❌ Keine autonomen Änderungen
- ✅ Änderungen ausschließlich durch den User
- ✅ Änderungen sind deklarativ, nicht interpretativ

### Nutzung durch Agenten
Agenten dürfen diese Datei:
- lesen
- zitieren
- als harte Randbedingung verwenden

Agenten dürfen sie **nicht**:
- interpretieren
- erweitern
- umdeuten
- implizit fortschreiben

---

## 3. Betriebssystem & Basisumgebung

### Host-Betriebssystem
- Windows 11

### Linux-Umgebung
- WSL2 (Linux)

Diese Kombination ist **kanonisch** für Entwicklung und Tests.

---

## 4. Runtime-Stack

- Docker Desktop
- Docker Compose

**Zielbild (nicht aktiv):**
- Kubernetes  
  (keine produktive oder testweise Nutzung zum aktuellen Zeitpunkt)

Alle Architektur- oder Tool-Entscheidungen müssen **mit Docker-Compose kompatibel** sein.

---

## 5. Hardware-Kontext

- Lokales Entwickler-System
- Ressourcen variabel
- Keine garantierten Fixed Limits außerhalb expliziter Konfiguration

Annahmen über Performance oder Parallelität dürfen **nicht** über diese Angaben hinausgehen.

---

## 6. Virtualisierung & Container-Konfiguration

### WSL2 / Docker Desktop

```ini
[wsl2]
memory=8GB
processors=8
swap=4GB
localhostForwarding=true
defaultVhdSize=256GB
---

### 7. Stabilitätsgarantie

## Diese Datei ändert sich nur, wenn sich mindestens eines der folgenden Dinge ändert:

Host-Betriebssystem

Virtualisierungs-Setup (z. B. WSL2 → native Linux)

primäre Runtime (z. B. Compose → Kubernetes aktiv)

grundlegende Hardware-Architektur

Operative, projekt- oder sessionspezifische Änderungen gehören nicht hierher.

### 8. Verhältnis zu anderen Dokumenten

### SYSTEM.CONTEXT.md
→ beschreibt wo und unter welchen Annahmen das System läuft

### CDB_KNOWLEDGE_HUB.md
→ beschreibt was entschieden und beauftragt wurde

### SHARED.WORKING.MEMORY.md
→ beschreibt worüber aktuell nachgedacht wird

### NEXUS.MEMORY.yaml
→ beschreibt was dauerhaft erinnert werden darf

Abschlussregel

Diese Datei ist ein statischer Umweltanker.
Wenn sich etwas häufig ändert, gehört es nicht hier hinein.
