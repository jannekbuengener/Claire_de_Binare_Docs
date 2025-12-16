# Agenten-System des Claire de Binare

## Übersicht

Das Claire de Binare (CDB) System wird durch spezialisierte Agenten gesteuert, die jeweils spezifische Rollen und Verantwortlichkeiten haben.

## Agenten-Architektur

### Grundprinzipien
1. **Rollenbasiert**: Jeder Agent hat eine klar definierte Rolle
2. **Governance-gesteuert**: Alle Agenten folgen der System-Verfassung
3. **Kollaborativ**: Agenten arbeiten koordiniert zusammen
4. **Dokumentiert**: Jede Agenten-Rolle ist formal in einer Charter definiert

## Agenten-Hierarchie

### Governance-Agenten
Verantwortlich für System-Governance und Regelkonformität

### Wissens-Agenten
Verwalten und kuratieren die Wissensbasis

### Dokumentations-Agenten
Erstellen und pflegen System-Dokumentation

### Koordinations-Agenten
Koordinieren Aktivitäten zwischen verschiedenen Agenten

## Agenten-Charter

Jeder Agent muss eine formale Charter haben, die definiert:
- **Identität**: Name und Zweck
- **Rolle**: Verantwortlichkeiten und Befugnisse
- **Schnittstellen**: Interaktionen mit anderen Agenten
- **Beschränkungen**: Was der Agent nicht tun darf
- **Governance**: Wie der Agent kontrolliert wird

### Charter-Format
Alle Charters verwenden das YAML-Format und folgen dem Template in `charter-template.yaml`.

### Charter-Speicherort
Agenten-Charters werden gespeichert als:
- `agents/<agent-name>.yaml` - Charter-Definition
- `agents/<agent-name>.md` - Ausführliche Dokumentation (optional)

## Rollen-Definitionen

Siehe `roles.yaml` für die vollständige Liste definierter Agenten-Rollen im System.

## Charter erstellen

1. Kopiere `charter-template.yaml`
2. Benenne um zu `<agent-name>.yaml`
3. Fülle alle erforderlichen Felder aus
4. Erstelle optional begleitende `.md` Dokumentation
5. Update `roles.yaml` mit der neuen Rolle
6. Erstelle Pull Request mit Governance-Review

## Agenten-Lifecycle

### 1. Proposal
- Neue Agenten-Rolle wird vorgeschlagen
- Begründung und Charter-Entwurf

### 2. Review
- Governance-Review der Charter
- Prüfung auf Konsistenz mit System-Zielen

### 3. Approval
- Formale Genehmigung durch Governance
- Merge der Charter ins Repository

### 4. Active
- Agent ist aktiv im System
- Charter ist bindend

### 5. Update
- Charter-Updates folgen gleichem Prozess
- Versionierung erforderlich

### 6. Deactivation (falls notwendig)
- Agent wird deaktiviert
- Charter bleibt zur Historie

## Verantwortlichkeiten

### Charter-Owner
Jede Charter hat einen Owner, verantwortlich für:
- Aktualität der Charter
- Konformität des Agenten
- Updates bei Änderungen

### Governance-Board
Genehmigt:
- Neue Agenten-Rollen
- Wesentliche Charter-Updates
- Deaktivierungen

## Konfliktlösung

Bei Konflikten zwischen Agenten:
1. Referenz zu jeweiligen Charters
2. Prüfung gegen System-Verfassung
3. Eskalation zu Governance-Board bei Bedarf

---
**Version**: 1.0.0  
**Letzte Änderung**: 2025-12-16
