# Claire de Binare Docs

Kanonisches Governance-, Wissens- und Agentensteuerungs-Repository für das System „Claire de Binare (CDB)".

## Übersicht

Dieses Repository ist der **zentrale Governance-Hub** für das Claire de Binare System. Es enthält:

- ✅ **Verfassung und Richtlinien** - Fundamentale Regeln und Strukturen
- ✅ **Agenten-Charter** - Rollendefinitionen und Verantwortlichkeiten
- ✅ **Wissensbasis** - Entscheidungen und Langzeit-Memory
- ✅ **Dokumentations-Index** - Strukturierung und Navigation

❌ **Kein Runtime-Code, keine Infrastruktur, keine Ausführung**

## Schnellstart

### 🎯 Neue Beitragende
1. Lies die [System-Verfassung](governance/CONSTITUTION.md)
2. Verstehe die [Repository-Richtlinien](governance/REPOSITORY_POLICY.md)
3. Folge den [Beitragsregeln](governance/CONTRIBUTION_RULES.md)

### 🤖 Agenten-Entwicklung
1. [Agenten-Übersicht](agents/README.md) lesen
2. [Charter-Template](agents/charter-template.yaml) studieren
3. [Rollen-Definitionen](agents/roles.yaml) prüfen

### 📚 Wissensbasis nutzen
1. [Wissens-Übersicht](knowledge/README.md) lesen
2. [Entscheidungen](knowledge/decisions/) durchsuchen
3. [Wissens-Index](knowledge/index.yaml) verwenden

## Dokumentations-Struktur

```
/
├── governance/              # Governance-Dokumente
│   ├── CONSTITUTION.md     # System-Verfassung
│   ├── REPOSITORY_POLICY.md # Repository-Richtlinien
│   └── CONTRIBUTION_RULES.md # Beitragsregeln
├── agents/                  # Agenten-System
│   ├── README.md           # Agenten-Übersicht
│   ├── charter-template.yaml # Charter-Vorlage
│   └── roles.yaml          # Rollen-Definitionen
├── knowledge/               # Wissensbasis
│   ├── README.md           # Wissens-Übersicht
│   ├── index.yaml          # Wissens-Index
│   └── decisions/          # Entscheidungsaufzeichnungen
└── docs/                    # Dokumentation
    ├── INDEX.md            # Dokumentations-Index
    └── templates/          # Dokumentvorlagen
```

## Kern-Dokumente

### Governance
- [System-Verfassung](governance/CONSTITUTION.md) - Grundlegende Prinzipien
- [Repository-Richtlinien](governance/REPOSITORY_POLICY.md) - Strikte Regeln
- [Beitragsregeln](governance/CONTRIBUTION_RULES.md) - Wie beitragen

### Agenten
- [Agenten-System](agents/README.md) - Übersicht
- [Charter-Template](agents/charter-template.yaml) - Vorlage
- [Rollen](agents/roles.yaml) - Definitionen

### Wissen
- [Wissensbasis](knowledge/README.md) - Übersicht
- [Wissens-Index](knowledge/index.yaml) - Strukturierter Zugriff
- [Entscheidungen](knowledge/decisions/) - ADRs

### Dokumentation
- [Dokumentations-Index](docs/INDEX.md) - Vollständiger Index
- [Templates](docs/templates/) - Vorlagen für neue Dokumente

## Grundprinzipien

### ✅ Erlaubt
- Markdown-Dateien (`.md`) für Dokumentation
- YAML-Dateien (`.yaml`, `.yml`) für strukturierte Daten
- Governance-Richtlinien und -Prozesse
- Agenten-Charter und Rollenbeschreibungen
- Wissens- und Entscheidungsstrukturen
- Dokumentations-Indizes und -Vorlagen

### ❌ Verboten
- Anwendungscode oder Implementierungen
- Services, APIs oder Microservices
- Infrastruktur-Code (Terraform, CloudFormation, etc.)
- Build-Tools oder Package-Dependencies
- Binärdateien oder kompilierte Artefakte
- Ausführbare Skripte (außer Dokumentationsbeispiele)

## Beitragen

Alle Beiträge müssen den [Beitragsregeln](governance/CONTRIBUTION_RULES.md) folgen und die [Repository-Richtlinien](governance/REPOSITORY_POLICY.md) respektieren.

### Quick Contribution Checklist
- [ ] Nur Markdown (`.md`) oder YAML (`.yaml`, `.yml`) Dateien
- [ ] Kein ausführbarer Code oder Infrastruktur
- [ ] Passt in definierte Verzeichnisstruktur
- [ ] Folgt Dokumentations-Standards
- [ ] Respektiert Agenten-Governance

## Lizenz

[Zu ergänzen - entsprechend der Projekt-Lizenz]

---

**Version**: 1.0.0  
**Status**: Aktiv  
**Letzte Änderung**: 2025-12-16
