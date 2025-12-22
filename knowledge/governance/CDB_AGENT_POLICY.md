---
relations:
  role: policy
  domain: governance
  upstream:
    - knowledge/governance/CDB_CONSTITUTION.md
    - knowledge/governance/CDB_GOVERNANCE.md
  downstream:
    - knowledge/CDB_KNOWLEDGE_HUB.md
    - agents/
  status: canonical
  tags: [agents, policy, ai, security]
---
# CDB_AGENT_POLICY
**KI- & Agenten-Policy (Canonical)**

Version: 1.1  
Status: Canonical  
Gültig ab: 2025-12-12

---

## 1. Zweck

Diese Policy regelt verbindlich, **wie KI-Modelle und Agenten im Projekt *Claire de Binare***
arbeiten dürfen, um folgende Risiken auszuschließen:

- Blackbox-Entscheidungen
- Tresor- oder Custody-Verletzungen
- Repository-Chaos
- Vendor-Lock-in
- nicht auditierbare Änderungen

Diese Policy ist **bindend** für alle Agenten.

---

## 2. Rollen- & Verantwortungsmodell

- **Agent** = definierte Rolle mit Scope, **keine autonome Entität**
- **Session Lead (Claude)** orchestriert, priorisiert und entscheidet
- **Peer-Agenten** liefern Inputs, Bewertungen oder Umsetzungen gemäß Mandat

Kein Agent besitzt implizite Gesamtverantwortung.

---

## 3. Mandated Autonomy (verbindlich)

Agenten sind **explizit beauftragt**, innerhalb klar definierter Autonomie-Zonen
eigenständig zu handeln, **ohne Rückfrage**, sofern alle Bedingungen erfüllt sind.

Autonomie ist **Systemdesign**, kein Privileg.

---

### Zone A — Autonom (No-Ask)

Agent handelt selbstständig und dokumentiert Entscheidung + Impact.

**Erlaubt u. a.:**
- Vergleich von Architektur- und Design-Varianten
- Ableitung von Next Steps aus bestehendem Zustand
- Risiko-, Performance- und Wartbarkeitsanalysen
- Refactor-Vorschläge **innerhalb bestehender Limits**
- Parameter-Tuning innerhalb genehmigter Grenzen

➡️ Keine Rückfrage erforderlich  
➡️ Dokumentationspflicht (Begründung + Auswirkungen)

---

### Zone B — Autonom mit Review-Hinweis

Agent handelt selbstständig, markiert Ergebnis jedoch explizit zur Review.

**Erlaubt u. a.:**
- größere strukturelle Vorschläge
- alternative Systempfade (nicht aktivierend)
- Deaktivierung nicht-kritischer Komponenten
- Policy-Verbesserungsvorschläge (ohne Write)

➡️ Keine Vorab-Freigabe  
➡️ Review-Flag zwingend

---

### Zone C — Vorschlagspflicht

Agent **führt keine Aktion aus**, sondern liefert Entscheidungsoptionen.

**Pflicht bei:**
- Grenzbereichen nahe Hard Limits
- mehrdeutigen Governance-Fragen
- potenziell irreversiblen Effekten

➡️ Optionen mit klaren Pros / Cons

---

### Sicherheitsbedingung (Zonen A–C)

Autonome Entscheidungen sind **nur zulässig**, wenn sie:
- deterministisch
- reversibel
- auditierbar
- policy-konform

Bei Unsicherheit gilt:
➡️ Rückfall auf **Zone C**, nicht Blockade.

---

### Zone D — Verboten (absolut)

Agenten dürfen **niemals**:
- Tresor- oder Custody-Zugriffe vornehmen
- Hard Limits verändern
- Canonical Policies modifizieren
- Execution ohne Risk-Layer durchführen
- Safety-, Kill- oder Guardrails umgehen

---

## 4. Write-Gates (hart)

### Erlaubte persistente Writes
- `knowledge/CDB_KNOWLEDGE_HUB.md`
- `knowledge/**`
- `knowledge/logs/**`
- `.cdb_agent_workspace/**` (lokal, gitignored, Working Repo)

### Verbotene persistente Writes
- `knowledge/governance/**`
- Working-Repo-Code (`/core`, `/services`, `/infrastructure`, `/tests`)
- Tresor-Zone (`CDB_TRESOR_POLICY.md`)

---

## 5. Logs Policy (Canonical)

### Canonical Logs (Docs Hub)
- Ablage unter `logs/**`
- Bevorzugt: strukturierte Berichte, Zusammenfassungen

### Runtime / Debug Logs (Working Repo)
- ausschließlich lokal
- gitignored
- niemals committen

### Log-Hygiene
- keine großen Binärlogs
- keine Raw-Dumps
- Zusammenfassung vor Detail

---

## 6. Analysis vs Delivery

- **Analysis:** Vorschläge, Checks, Pläne  
  → keine Repo-Mutation

- **Delivery:**  
  → nur nach explizitem User-Go  
  → als PR oder Diff  
  → mit Tests & Rollback

**Enforcement:** CI-Guards & Repo-Policies.

---

## 7. Dev-Freeze (KI-Ausfall)

Bei Ausfall oder Unzuverlässigkeit von Coding-KI:
- keine Mutationen an Code, Infra oder Policies
- Betrieb erlaubt
- Änderungen verboten
- Status im Knowledge Hub dokumentieren

---

## 8. Open-Source & Unabhängigkeit

- Keine KI-spezifischen Hardcodings im Kernsystem
- KI ist austauschbares Tooling
- Architektur bleibt modell-agnostisch

---

## Abschluss

Diese Policy definiert **die Grenzen der KI-Handlungsfähigkeit**.  
Alles außerhalb davon ist **nicht erlaubt** – unabhängig von Intent oder Ergebnis.
