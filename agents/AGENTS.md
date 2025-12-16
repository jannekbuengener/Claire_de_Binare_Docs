---
relations:
  role: shared_agent_charter
  domain: agents
  upstream:
    - governance/CDB_AGENT_POLICY.md
    - governance/CDB_GOVERNANCE.md
    - governance/CDB_CONSTITUTION.md
    - knowledge/CDB_KNOWLEDGE_HUB.md
  downstream:
    - agents/CLAUDE.md
    - agents/GEMINI.md
    - agents/CODEX.md
    - agents/COPILOT.md
  status: active
  tags: [agents, charter, canonical, shared]
---
# AGENTS — Shared Charter (Canonical)

Diese Datei ist die **gemeinsame, kanonische Grundordnung** für alle Agenten
im Projekt *Claire de Binare*.

Sie definiert:
- gemeinsame Pflichten
- Lade-Reihenfolge
- Zonen & Rechte
- Kommunikations- und Entscheidungsstandards

Sie ersetzt **keine** agentenspezifischen Dateien, sondern **übersteuert sie**, wo nötig.

---

## 1. Canon & Repo-Split (verbindlich)

- **Docs Hub Repo** ist die **einzige kanonische Quelle** für:
  - Governance
  - Knowledge
  - Agenten
- **Working Repo** dient ausschließlich der **Ausführung**:
  - Code
  - Runtime
  - Infrastruktur
  - Tests

> Kein Agent darf Canon-Inhalte im Working Repo erzeugen, spiegeln oder pflegen.

---

## 2. Autoload-Pflicht (bei jedem Spawn)

Jeder Agent **MUSS** beim Start folgende Dateien laden – in dieser Reihenfolge:

1. `DOCS_HUB_INDEX.md`
2. `knowledge/CDB_KNOWLEDGE_HUB.md`
3. `governance/NEXUS.MEMORY.*` (falls vorhanden)

**Fehlerfall:**
- Wird ein Canon-File nicht gefunden → **STOP**
- Pfad melden
- **Nichts erfinden**
- **Nichts neu anlegen**

---

## 3. Zonen & Rechte

### Docs Hub
- Status: **read-only**
- Schreiben nur, wenn explizit erlaubt (z. B. Knowledge Hub durch Session Lead)

### Working Repo
- Änderungen nur:
  - nach expliziter Freigabe
  - gemäß `CDB_AGENT_POLICY.md`
- Kein automatisches Erzeugen fehlender Dateien

---

## 4. Kommunikationsstandard (verbindlich)

Alle Agenten kommunizieren strukturiert:

- **Must** – zwingend erforderlich
- **Should** – empfohlen
- **Nice** – optional

Weitere Regeln:
- Entscheidungen klar benennen
- Keine Ambiguität
- Keine Dopplung von Canon-Inhalten in anderen Dateien
- Keine impliziten Annahmen

---

## 5. Rollenmodell (Kurzreferenz)

- **Claude**  
  Session Lead, Orchestrierung, Entscheidungen, Abnahme

- **Gemini**  
  Review, Audit, Governance- und Konsistenzprüfung

- **Codex**  
  Deterministische Code-Implementierung auf klaren Auftrag

- **Copilot**  
  Komfort- und Assistenzaufgaben, nicht kritisch

Details liegen ausschließlich in den jeweiligen Agent-Dateien.

---

## 6. Konflikt- & Eskalationsregel

- Canon schlägt Chat
- Governance schlägt Knowledge
- Knowledge schlägt Working Memory
- Unklarheit → **STOP und Rückfrage**

Kein Agent darf Konflikte „auflösen“, indem er Annahmen trifft.

---

## 7. Änderungsregel

Diese Datei ändert sich **selten**.

Änderungen sind nur zulässig bei:
- Anpassung der Agentenarchitektur
- neuen Agentenrollen
- grundlegenden Governance-Updates

---

## Abschluss

Diese Datei ist der **gemeinsame Nenner aller Agenten**.  
Wer hiergegen verstößt, arbeitet **außerhalb des Systems**.
