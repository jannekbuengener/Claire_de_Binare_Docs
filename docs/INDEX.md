# Dokumentations-Index

## Übersicht

Dieser Index bietet Zugang zu allen Dokumentations-Ressourcen im Claire de Binare (CDB) System.

## Haupt-Dokumentation

### Governance
Zentrale Governance-Dokumente, die die Regeln und Strukturen des Systems definieren.

- [System-Verfassung](../governance/CONSTITUTION.md) - Grundlegende Prinzipien und Strukturen
- [Repository-Richtlinien](../governance/REPOSITORY_POLICY.md) - Strikte Regeln für dieses Repository
- [Beitragsregeln](../governance/CONTRIBUTION_RULES.md) - Wie man zu diesem Repository beiträgt

### Agenten-System
Dokumentation des Agenten-basierten Governance-Systems.

- [Agenten-Übersicht](../agents/README.md) - Einführung in das Agenten-System
- [Charter-Template](../agents/charter-template.yaml) - Vorlage für Agenten-Charters
- [Rollen-Definitionen](../agents/roles.yaml) - Alle definierten Agenten-Rollen

### Wissensbasis
Langzeit-Wissen und Entscheidungen.

- [Wissens-Übersicht](../knowledge/README.md) - Einführung in die Wissensbasis
- [Wissens-Index](../knowledge/index.yaml) - Strukturierter Index aller Einträge
- [Entscheidungen](../knowledge/decisions/) - Architektur- und Governance-Entscheidungen

## Schnellstart

### Für neue Beitragende
1. Lies die [System-Verfassung](../governance/CONSTITUTION.md)
2. Verstehe die [Repository-Richtlinien](../governance/REPOSITORY_POLICY.md)
3. Folge den [Beitragsregeln](../governance/CONTRIBUTION_RULES.md)
4. Verwende [Templates](./templates/) für neue Dokumente

### Für Agenten-Entwicklung
1. Lies die [Agenten-Übersicht](../agents/README.md)
2. Studiere das [Charter-Template](../agents/charter-template.yaml)
3. Prüfe existierende [Rollen](../agents/roles.yaml)
4. Erstelle neue Charter nach dem Template

### Für Wissens-Kuratierung
1. Lies die [Wissens-Übersicht](../knowledge/README.md)
2. Verstehe das ADR-Format
3. Update den [Wissens-Index](../knowledge/index.yaml)
4. Folge Dokumentations-Standards

## Dokumentations-Struktur

```
/
├── README.md                           # Repository-Hauptseite
├── governance/                         # Governance-Dokumente
│   ├── CONSTITUTION.md                # System-Verfassung
│   ├── REPOSITORY_POLICY.md           # Repository-Richtlinien
│   └── CONTRIBUTION_RULES.md          # Beitragsregeln
├── agents/                             # Agenten-System
│   ├── README.md                      # Agenten-Übersicht
│   ├── charter-template.yaml          # Charter-Vorlage
│   ├── roles.yaml                     # Rollen-Definitionen
│   └── [agent-name].yaml              # Individuelle Charters
├── knowledge/                          # Wissensbasis
│   ├── README.md                      # Wissens-Übersicht
│   ├── index.yaml                     # Wissens-Index
│   └── decisions/                     # Entscheidungen
│       └── ADR-NNN-titel.md          # Einzelne ADRs
└── docs/                               # Dokumentation
    ├── INDEX.md                       # Dieser Index
    └── templates/                     # Vorlagen
        ├── adr-template.md            # ADR-Vorlage
        └── governance-doc-template.md # Governance-Vorlage
```

## Vorlagen

Verwende diese Templates für konsistente Dokumentation:

- [ADR-Template](./templates/adr-template.md) - Für Entscheidungsaufzeichnungen
- [Governance-Template](./templates/governance-doc-template.md) - Für Governance-Dokumente

## Dokumentations-Standards

### Markdown-Konventionen
- Verwende ATX-Style Headers (`#`, `##`, etc.)
- Ein Leerzeile zwischen Sections
- Code-Blöcke mit Sprach-Annotation
- Relative Links für interne Referenzen

### YAML-Konventionen
- 2 Leerzeichen für Einrückung
- Kommentare für Klarheit
- Konsistente Namensgebung (kebab-case für IDs)
- Version und Datum in Metadaten

### Dateinamen
- Kebab-case: `mein-dokument.md`
- ADRs: `ADR-NNN-titel.md` (z.B. `ADR-001-repository-structure.md`)
- Charters: `agent-name.yaml`
- Beschreibend aber kurz

## Navigation

### Nach Thema
- **Governance**: Start bei [Verfassung](../governance/CONSTITUTION.md)
- **Agenten**: Start bei [Agenten-Übersicht](../agents/README.md)
- **Wissen**: Start bei [Wissens-Übersicht](../knowledge/README.md)
- **Beitragen**: Start bei [Beitragsregeln](../governance/CONTRIBUTION_RULES.md)

### Nach Rolle
- **Governance-Verantwortliche**: [Governance](../governance/), [Verfassung](../governance/CONSTITUTION.md)
- **Agenten-Maintainer**: [Agenten](../agents/), [Rollen](../agents/roles.yaml)
- **Wissens-Kuratoren**: [Wissen](../knowledge/), [Index](../knowledge/index.yaml)
- **Beitragende**: [Contribution Rules](../governance/CONTRIBUTION_RULES.md), [Templates](./templates/)

## Such-Tipps

### Mit grep
```bash
# Suche in allen Markdown-Dateien
grep -r "Suchbegriff" . --include="*.md"

# Suche in YAML-Dateien
grep -r "key:" . --include="*.yaml"
```

### Nach Kategorie
```bash
# Alle Governance-Dokumente
find governance/ -name "*.md"

# Alle Agent-Charters
find agents/ -name "*.yaml"
```

## Wartung

### Dokumentations-Maintainer
Verantwortlich für:
- Index-Aktualität
- Konsistenz der Struktur
- Qualität der Dokumentation
- Navigation und Verlinkung

### Review-Prozess
Neue Dokumentation wird geprüft auf:
- Strukturelle Konsistenz
- Vollständigkeit
- Klarheit
- Korrekte Verlinkung

## Updates

Dieser Index sollte aktualisiert werden bei:
- Neuen Haupt-Dokumenten
- Struktur-Änderungen
- Neuen Templates
- Wichtigen Richtlinien-Updates

---
**Version**: 1.0.0  
**Letzte Änderung**: 2025-12-16  
**Maintainer**: documentation-architect
