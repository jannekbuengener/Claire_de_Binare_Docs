---
relations:
  role: doc
  domain: knowledge
  upstream: []
  downstream: []
  status: active
  tags: [knowledge, overview, rules, non_canonical]
---
# /knowledge — Working Knowledge & Session Context (NON-CANONICAL)

## Zweck

Der Ordner `/knowledge` ist der **zentrale Arbeits- und Denkraum**
für Mensch und KI-Agenten im Projekt *Claire de Binare*.

Er dient als:
- temporärer Denkraum
- Übergabe- und Koordinationsfläche
- Ablage für Reviews, Logs und Session-Kontext

**Wichtig:**  
Inhalte in `/knowledge` besitzen **keine kanonische Autorität** und
setzen **keine systemweiten Regeln**.

---

## Grundprinzip (verbindlich)

> `/knowledge` ist **Arbeitsgedächtnis**, nicht Gesetz.  
> Denken ist erlaubt. Autorität ist es nicht.

---

## Was gehört HIERHER

Der `/knowledge`-Ordner enthält **ausschließlich nicht-normative Inhalte**:

- Session-Zusammenfassungen und Handoffs
- laufende oder vorläufige Entscheidungen
- Denk- und Arbeitsnotizen
- Review- und Audit-Ergebnisse
- technische Logs und Reports
- System- und Runtime-Kontext (read-only)

### Zentrale Dateien

```text
/knowledge/
├── CDB_KNOWLEDGE_HUB.md        # Entscheidungs- & Übergabe-Hub (canonical, non-governance)
├── SHARED.WORKING.MEMORY.md    # Temporärer Denkraum (nicht bindend)
├── SYSTEM.CONTEXT.md           # Laufzeit- & Umweltkontext (read-only)
├── operating_rules/            # Betriebsregeln (nicht Governance)
├── reviews/                    # Review- & Audit-Berichte
├── tasklists/                  # Aufgabenlisten
└── logs/                       # Logs & Reports

Was gehört EXPLIZIT NICHT hierher

Folgende Inhalte dürfen niemals in /knowledge liegen:

Governance-Dokumente

Policies oder Regelwerke

Verfassungen oder Invarianten

kanonische Architektur- oder Repo-Definitionen

Langzeit-Memory (NEXUS.MEMORY.yaml)

Code, Konfigurationen oder Infrastruktur

Diese Inhalte gehören ausschließlich nach /governance.

Schreib- & Änderungsregeln
KI-Agenten

dürfen nur in /knowledge schreiben

dürfen Inhalte:

ändern

überschreiben

verwerfen

dürfen keine Regeln ableiten

dürfen Inhalte nicht als Wahrheit interpretieren

Mensch (User)

entscheidet explizit, ob Inhalte:

verworfen

archiviert

oder nach Governance / NEXUS überführt werden

Es gibt keinen automatischen Übergang aus /knowledge.

Beziehung zu Governance & Memory

/knowledge
→ Denken, Arbeiten, Übergeben

/governance
→ Regeln, Autorität, Invarianten

NEXUS.MEMORY.yaml
→ bestätigtes Langzeitwissen (stark reglementiert)

Der Übergang ist immer:

manuell

bewusst

explizit

Sicherheitsregel

Kein Dokument in /knowledge darf:

Ausführung triggern

Policies verändern

systemweite Effekte erzeugen

implizite Autorität besitzen

Leitsatz

Wenn ein Dokument Regeln setzt → gehört es nicht nach /knowledge.
Wenn ein Dokument denkt, prüft oder übergibt → gehört es nach /knowledge.

Chaos ist erlaubt.
Autorität ist es nicht.