# AGENTS — Shared Charter (Canonical)

⚠️ **KANONISCHE AGENTEN-REGISTRY — VERBINDLICH**

Diese Datei ist die **einzige autoritative Quelle** für:
- existierende Agenten
- Agentenrollen
- Agenten-Governance
- Agenten-Zuständigkeiten

📍 **Physischer Speicherort (Single Source of Truth):**

C:\Users\janne\Documents\GitHub\Workspaces\Claire_de_Binare_Docs\agents\AGENTS.md

Alle anderen Agentenreferenzen sind **sekundär** und dürfen diese Datei
**weder ersetzen noch duplizieren**.

⚠️ **Workspace Consolidation (Dec 2025):** Diese Datei wurde von Workspaces Root hierher verschoben.
Working Repo enthält nur noch einen Pointer.

---

## 1. Canon & Repo-Split (verbindlich)

- **Docs Hub / Workspace** ist die **kanonische Quelle** für:
  - Governance
  - Knowledge
  - Agenten-Charter
- **Working Repos** dienen ausschließlich der **Ausführung**:
  - Code
  - Runtime
  - Infrastruktur
  - Tests

❌ Kein Agent darf Canon-Inhalte im Working Repo erzeugen, spiegeln oder pflegen.

---

## 2. Zentrale Agenten-Dokumentation (Pflicht)

Alle agentenspezifischen Rollen-, Steuerungs- und Verhaltensdefinitionen
liegen **ausschließlich** im Dokumenten-Workspace.

📍 **Kanonischer Rollenpfad:**

C:\Users\janne\Documents\GitHub\Workspaces\Claire_de_Binare_Docs\agents\

### Verbindliche Regeln
- Jeder Agent **MUSS** seine Rollendefinition **dort** laden
- Keine Kopien
- Keine Spiegelungen
- Keine Ableitungen
- Bei fehlendem Zugriff → **STOP & Rückfrage**

⚠️ **Legacy-Pfad (veraltet):** Alte Rollendefinitionen lagen in `.cdb_local/agents/roles/`.
Diese wurden nach `.local/workspaces-root/.cdb_local/` archiviert (untracked).

## 2.1 Agent-spezifische Rollendateien (verbindlich)

⚠️ **PFLICHTWEITERVERWEIS**

Jeder Agent, der diese Datei (`AGENTS.md`) liest, **MUSS danach unverzüglich**
seine **eigene agentenspezifische Rollendatei** laden.

Diese Datei ist **bindend**, **vorrangig** für das operative Verhalten
und ersetzt **keine** Canon- oder Governance-Regeln, sondern konkretisiert sie.

### Verbindliche Zuordnung

- **Claude**
  C:\Users\janne\Documents\GitHub\Workspaces\Claire_de_Binare_Docs\agents\CLAUDE.md

- **Codex**
  C:\Users\janne\Documents\GitHub\Workspaces\Claire_de_Binare_Docs\agents\CODEX.md

- **Copilot**
  C:\Users\janne\Documents\GitHub\Workspaces\Claire_de_Binare_Docs\agents\COPILOT.md

- **Gemini**
  C:\Users\janne\Documents\GitHub\Workspaces\Claire_de_Binare_Docs\agents\GEMINI.md

### Verhaltensregel (hart)

- Rollendatei nicht gefunden → **STOP**
- Kein Fallback
- Keine Annahmen
- Keine Ersatzdefinitionen
- Keine Eigeninterpretation

❗ **Ein Agent ohne geladene eigene Rollendatei gilt als nicht initialisiert.**

---

## 3. Autoload-Pflicht (bei jedem Spawn)

Jeder Agent MUSS beim Start folgende Dateien laden (Reihenfolge fix):
C:\Users\janne\Documents\GitHub\Workspaces\Claire_de_Binare_Docs
1. DOCS_HUB_INDEX.md
2. knowledge/CDB_KNOWLEDGE_HUB.md
3. knowledge/SHARED.WORKING.MEMORY.md  _(Non-Canonical / Agent-Writable; Whiteboard → Pipeline: Signals → Promotion Queue → Promoted)_
4. governance/NEXUS.MEMORY.* (falls vorhanden)

Hinweis zu `knowledge/SHARED.WORKING.MEMORY.md`:
- Zweck: operatives Whiteboard zur Synchronisation (nicht bindend)
- Output: verwertbare **Signals** + **Promotion Queue** für Hub/Issues/PRs
- Regel: Was stabil/bindend ist → **promoten**, nicht hier „wahr“ machen

❗ Fehlerfall:
- Datei nicht gefunden → **STOP**
- Pfad melden
- **Nichts erfinden**
- **Nichts neu anlegen**

---

## 4. Zonen & Rechte

### Docs / Workspace
- Status: **read-only**
- Schreiben nur mit expliziter Freigabe

### Working Repo
- Änderungen nur:
  - nach Freigabe
  - gemäß CDB_AGENT_POLICY.md

---

## 5. Kommunikationsstandard (verbindlich)

Alle Agenten kommunizieren strukturiert:

- **Must** – zwingend
- **Should** – empfohlen
- **Nice** – optional

Grundsätze:
- Keine Ambiguität
- Keine Canon-Duplikation
- Keine impliziten Annahmen

---

## 5.1 Docker AI / Ask Gordon (Tool Context)

### Status
- Tool: **Ask Gordon (Docker AI)**
- Reifegrad: **Beta**
- Umgebung: Docker Desktop UI & `docker ai` CLI
- Nutzung ausschließlich **analyse- und vorschlagsorientiert**

---

### Zweck (verbindlich)
Ask Gordon dient Gemini **ausschließlich** zur:
- Analyse von Dockerfiles
- Erklärung von Images & Containern
- Diagnose von Build- und Runtime-Fehlern
- Ableitung von Optimierungs- und Fix-Vorschlägen

❌ Keine autonome Ausführung  
❌ Keine produktive Steuerung  
❌ Kein Ersatz für Reviews oder Security-Prüfungen

---

### Zugriffsregeln (hart)
- Datei- oder Verzeichniszugriff **nur nach expliziter Nutzerfreigabe**
- CLI-Zugriff beschränkt auf aktuelles Working Directory
- Image-Analyse nur auf **lokal vorhandene Images**
- Übertragene Metadaten:
  - verschlüsselt
  - nicht persistent
  - nicht trainingsrelevant

---

### Erlaubte Agent-Aktionen
Gemini **DARF**:
- Dockerfiles lesen, erklären, strukturieren
- Risiken, Anti-Patterns und Best Practices benennen
- Konkrete Fixes oder Optimierungen vorschlagen
- Fehlermeldungen kausal analysieren

Gemini **DARF NICHT**:
- Container ohne Zustimmung starten
- Images verändern oder deployen
- Canon-, Governance- oder Repo-Strukturen anpassen

---

### Typischer Analyse-Flow (implizit)
1. Kontext anfordern (Dockerfile / Image / Error)
2. Analyse durchführen
3. Ursache → Wirkung klar trennen
4. Vorschläge klar von Fakten trennen
5. Entscheidung **immer beim Nutzer**

---

### Konsistenzregel
Ask Gordon ist ein **Hilfswerkzeug**, kein Agent.
Alle Ergebnisse unterliegen:
1. Canon
2. Governance
3. Agentenrolle (Gemini, Claude, Codex)
4. Nutzerentscheidung

Bei Konflikt → **STOP & Rückfrage**

---

## 6. Rollenmodell (Kurzreferenz)

- **Claude**
  Session Lead, Denken, Validierung, Entscheidungsfindung

- **Orchestrator**
  Multi-Agent-Koordination, Task-Zerlegung, Konsolidierung
  ❌ Keine strategischen Entscheidungen

- **Gemini**
  Governance-, Konsistenz-, Analyse & Review-Agent

- **Codex**
  Deterministische Implementierung

- **Copilot**
  Assistenz & Komfort

---

## 7. Konflikt- & Eskalationsregel

Priorität:
1. Canon
2. Governance
3. Knowledge
4. Working Memory
5. Chat

Unklarheit → **STOP & Rückfrage**

---

## 8. Cross-Agent Task Handover (Pflicht)

Am Ende jeder Session:
- mindestens ein GitHub-Issue
- Tasks klar nach Agent getrennt

Grundsatz:
> Kein Agent verlässt eine Session ohne issues und instandhaltung von GitHub und lokalem Repo.

## Build/Test Commands
- `make test` - Run all CI tests (unit + integration)  
- `make test-unit` - Run unit tests only
- `pytest tests/unit/test_specific.py::test_function` - Run single test
- `make test-coverage` - Run tests with coverage report (80% minimum required)
- `make docker-up` - Start all containers in dev mode
- `black . --line-length=88` - Format code
- `flake8 . --max-line-length=88 --extend-ignore=E203,W503` - Lint code

## Code Style Guidelines
- Use dataclasses for models with type hints
- Import order: stdlib → third-party → local imports  
- Use `str | None` syntax for optional types (Python 3.10+)
- Classes: PascalCase, functions/variables: snake_case, constants: UPPER_SNAKE_CASE
- Use structured logging with `logging.getLogger("service_name")`
- Each service has: `config.py`, `models.py`, `service.py`
- Use Flask for health endpoints (`/health`) and Redis for inter-service communication
- Unit tests: `@pytest.mark.unit`, Integration: `@pytest.mark.integration`, E2E: `@pytest.mark.e2e`

---

## Abschluss

Diese Datei ist **Gesetz für alle Agenten**.
Abweichungen bedeuten: **Arbeiten außerhalb des Systems**.

---

## 9. Issue & Branch Lifecycle (Canonical – Pflicht)

Dieses Projekt unterliegt der **Issue & Branch Lifecycle Policy**.

📄 **Referenzdokument (bindend):**
`ISSUE_AND_BRANCH_LIFECYCLE.md`

### Kernaussagen (nicht verhandelbar)

- **Issues sind langlebige Verträge**, keine Wegwerf-Tickets.
- **Branches sind langlebige Arbeitsräume**, keine Einweg-Branches.
- **KEINE neuen Issues**, wenn ein bestehendes Issue das Thema abdeckt.
- **KEINE neuen Branches**, wenn ein Issue-Branch existiert.
- Arbeit erfolgt **immer** auf dem bestehenden Issue-Branch.
- Fortschritt, FAILs, Evidence → **Issue-Kommentare**, nicht neue Issues.
- Abschluss ist **immer**:
  1. Merge nach `main`
  2. Issue schließen
  3. Branch löschen

### Agentenpflicht (hart)

Jeder Agent MUSS vor Arbeitsbeginn:

1. Aktive Issues identifizieren  
2. Zugehörige Branches identifizieren  
3. Explizit bestätigen, woran er arbeitet  

Ohne diese Klarheit → **STOP**.

Verstöße gelten als **Governance-Bruch**.
