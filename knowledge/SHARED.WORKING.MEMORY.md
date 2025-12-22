✅ FINALER TEXT – SHARED.WORKING.MEMORY.md

(1:1 ersetzen)

---
relations:
  role: working_memory
  domain: knowledge
  upstream:
    - knowledge/governance/CDB_CONSTITUTION.md
    - knowledge/governance/CDB_GOVERNANCE.md
    - knowledge/governance/CDB_AGENT_POLICY.md
  downstream: []
  status: active
  tags: [working_memory, agent_collaboration, temporary]
---
# SHARED.WORKING.MEMORY
**CDB – Shared Working Memory Layer**

Version: 1.1  
Status: Non-Canonical / Agent-Writable  
Charakter: Flüchtig, explorativ, nicht bindend

---

## 0. Rangordnung & Systemeinordnung

Diese Datei unterliegt strikt:

1. `CDB_CONSTITUTION.md`  
2. `CDB_GOVERNANCE.md`  
3. `CDB_AGENT_POLICY.md`

Sie ist ausdrücklich:
- ❌ keine Governance
- ❌ kein kanonisches Wissen
- ❌ kein Entscheidungsartefakt
- ❌ kein Audit- oder Logbuch

Sie besitzt **keine Autorität** im System.

---

## 1. Zweck

`SHARED.WORKING.MEMORY.md` ist der **gemeinsame Denk- und Arbeitsraum**
aller beteiligten Agenten und Modelle.

Sie existiert, um:
- paralleles Denken zu ermöglichen
- Hypothesen, Skizzen und Zwischenstände zu sammeln
- Abhängigkeiten sichtbar zu machen
- kognitive Kohärenz zwischen Agenten herzustellen

> Dies ist der Ort, an dem Agenten **denken dürfen**, ohne Recht zu behalten.

---

## 2. Was diese Datei IST

Diese Datei ist:
- ein temporärer **kognitiver Synchronisationsraum**
- ein **Arbeitskontext**, kein Wissensspeicher
- ein Ort für unfertige Gedanken

Stabilität ist **nicht** das Ziel.

---

## 3. Was diese Datei NICHT ist

Diese Datei ist **nicht**:
- System- oder Langzeitgedächtnis → `NEXUS.MEMORY.yaml`
- Entscheidungslog → `CDB_KNOWLEDGE_HUB.md`
- Dokumentation
- Statusübersicht
- Taskliste
- Governance

Alles, was bestätigt, stabil oder bindend ist, gehört **nicht** hierher.

---

## 4. Zugriffsrechte

### 4.1 Lesen
- Alle Agenten
- Alle Modelle
- Session Lead
- User

### 4.2 Schreiben
- ✅ Alle Agenten
- ✅ Parallel
- ✅ Ohne Vorab-Freigabe
- ✅ Auch im Analysis Mode

### 4.3 Einschränkungen
- ❌ Kein automatischer Transfer nach `NEXUS.MEMORY`
- ❌ Kein Persistenz-Upgrade
- ❌ Keine implizite Autorität

Eintrag ≠ Wahrheit.

---

## 5. Semantische Regeln (verbindlich)

Einträge dürfen:
- widersprüchlich sein
- unfertig sein
- verworfen werden
- überschrieben werden

**Wahrheit ist optional.**  
**Nützlichkeit ist Pflicht.**

---

## 6. Empfohlene Beitragsstruktur (nicht zwingend)

Agenten *sollten* Beiträge so kennzeichnen:

```md
### [Agent / Modell | Datum-Zeit]
- Kontext:
- Gedanke / Hypothese:
- Abhängigkeiten:
- Risiken / Unsicherheiten:
- Offene Fragen:

## 7. Beziehung zu anderen Ebenen
Ebene	Zweck	Schreibrechte
SHARED.WORKING.MEMORY	Denken	Agenten
CDB_KNOWLEDGE_HUB	Entscheiden	Session Lead
NEXUS.MEMORY	Erinnern	User + Lead

Kein Übergang erfolgt automatisch.
Jeder Transfer ist bewusst und manuell.

## 8. Löschung & Vergessen

Vergessen ist erwünscht.

### Einträge dürfen jederzeit:

gelöscht

zusammengefasst

ersetzt

verworfen werden

## 9. Sicherheitsprinzip

Diese Datei darf das System klüger, aber niemals mächtiger machen.

### Kein Eintrag darf:

Execution auslösen

Policies verändern

Limits umgehen

implizite Autorität erzeugen

## 10. Abschlussregel

### Wenn etwas:

stabil ist

bewiesen ist

systemweit gelten soll

→ raus aus dieser Datei.

Dies ist ein Denkraum.
Kein Gedächtnis.
Kein Gesetz.