---
name: obsidian-wissensbasis
description: Use when building or maintaining a personal knowledge base for an AI agent (Hermes, Claude, ChatGPT) — set up an Obsidian vault as the agent's second brain, structure notes, sync conventions, and let the agent search/read/write there.
version: 1.0.0
---

# Obsidian-Wissensbasis für KI-Agenten

## Overview

KI-Agenten antworten nur so gut, wie ihr Kontext reicht. Eine Wissensdatenbank in Markdown (Obsidian-Vault) gibt dem Agenten dein Wissen: Projekte, Entscheidungen, Recherchen, Regeln. Statt jedes Mal neu zu erklären, liest der Agent die Notizen und liefert konkrete Antworten.

**Kernprinzip: Ein Ordner Markdown-Dateien + klare Struktur + Agent-Zugriff = zweites Gedächtnis.**

## When to Use

- Du willst, dass dein KI-Agent dein Wissen (Projekte, Regeln, Recherchen) nutzt
- Du verlierst Kontext zwischen Sessions und erklärst ständig dasselbe
- Du hast Notizen verstreut (Chats, Docs, Brainstorming) und willst sie zentralisieren
- Du willst eine dauerhafte, offline-verfügbare Wissensbasis ohne Cloud-Zwang

**Do NOT use for**: schnelle Einzelnotizen ohne Agenten-Anbindung (dafür reicht eine einfache Notizdatei).

## Quick Start (5 Schritte)

1. **Vault-Ordner anlegen** (z.B. `~/Vault` oder serverseitig `/root/obsidian-vault/`)
2. **Struktur definieren**: `Projekte/`, `Recherche/`, `Inbox/`, `So-arbeiten-wir.md`
3. **Projekt-Notizen** anlegen: Status, Ziel, offene Punkte als `- [ ]` Checkboxen
4. **Agent-Zugriff konfigurieren**: OBSIDIAN_VAULT_PATH setzen, Agent darf lesen/suchen/schreiben
5. **Konventionen**: eine `So-arbeiten-wir.md` für alle Regeln (Ton, Struktur, Dateibenennung)

## Agent-Workflow (wenn der Agent den Vault nutzt)

| Aktion | Vorgehen |
|--------|----------|
| Suchen | Markdown-Dateien nach Stichworten durchsuchen (grep/search_files) |
| Lesen | Relevante Notiz als Kontext in die Anfrage übernehmen |
| Schreiben | Neue Erkenntnisse als Notiz oder Ergänzung anlegen |
| Verknüpfen | `[[Wikilinks]]` setzen, damit die Basis zusammenhängt |
| Sichern | Vault als ZIP packen (z.B. jährlich), ZIP außerhalb ablegen |

## Pflicht-Workflow für Projekte

1. **Projektstart**: `Projekte/<Name>.md` anlegen — Status, Ziel, offene Punkte
2. **Session-Ende**: Notiz aktualisieren — Entscheidungen, neue Details, Pfade, URLs
3. **Nichts nur im Chat lassen**: Dateipfade, API-Key-Ort (niemals die Keys selbst), Domain-Namen, Entscheidungen → Vault
4. **Verlinken statt duplizieren**: `[[Note]]` statt Copy-Paste
5. **Inbox** für schnelle Ideen, später sortieren
6. **Konventionen** liegen im Vault-Root (`So-arbeiten-wir.md`)

## Struktur-Empfehlung

```
Vault/
├── So-arbeiten-wir.md      # Konventionen & Regeln (wird immer mitgelesen)
├── Wissensarchiv.md        # Index / Übersicht
├── Projekte/               # Ein File pro Projekt
├── Recherche/              # Themen-Notizen
├── Recht/                  # Dokumente, Fälle
├── Automation/             # Cron, Workflows, Setup-Notizen
└── Inbox/                  # Schnelle Ideen (wird sortiert)
```

## Best Practices

- **Kurze Dateien mit klaren Titeln** statt einer Riesen-Notiz — der Agent findet sie besser
- **Wikilinks nutzen**: `[[Projektname]]` verbindet verwandte Themen
- **Checkboxen für offene Punkte** (`- [ ]`), damit Status sichtbar ist
- **Keine Binärdaten im Vault** — nur Markdown und Text; Bilder/PDFs extern ablegen
- **Backup-Rhythmus definieren**: z.B. 1× jährlich als ZIP (Punkt 5 im Quick Start)
- **Datumsangaben** (z.B. `2026-08-18`) in Titeln oder Metadaten helfen beim Auffinden

## Known Pitfalls

- **Pfad-Variablen nicht auflösen**: Datei-Tools expandieren keine `$OBSIDIAN_VAULT_PATH` — immer absoluten Pfad nutzen
- **Leerer Vault-Index**: Ohne `Wissensarchiv.md`/Index weiß der Agent nicht, wo was liegt
- **Tote Links**: Wikilinks zu gelöschten Notizen verwirren — beim Löschen auch Links prüfen
- **Kein Sync**: Ohne jährliches Backup sind alle Notizen nur auf einem Gerät — Backup einplanen
- **Cron-Interaktion**: Wenn Cron-Jobs in den Vault schreiben, Backup-Zeitpunkt und Job-Zeiten abstimmen

## Verification

- [ ] Vault-Ordner existiert, `So-arbeiten-wir.md` + Index vorhanden
- [ ] Projekte als eigene Dateien mit `- [ ]` Checkboxen
- [ ] Agent kann via search_files nach Inhalten suchen
- [ ] Backup-Lauf getestet (ZIP erstellt, wieder entpackbar)