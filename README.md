# Skill-Lab 🧪

Kuratierte Skills für AI-Agenten — entstanden aus der Beobachtung realer Probleme, die Nutzer mit AI-Agenten und KI-Systemen im Alltag erleben.

## Was hier liegt

**`/skills/`** — einsatzbereite Skills (je ein Ordner pro Skill mit einer `SKILL.md`).

Jeder Skill adressiert ein konkretes, wiederkehrendes Nutzerproblem — vom sicheren Umgang mit autonomen Coding-Agenten bis zur Kostenkontrolle — und ist direkt in einem Agenten nutzbar.

## Skills

| Skill | Problem | Beschreibung |
|---|---|---|
| [`vibe-coding-safety`](skills/vibe-coding-safety/SKILL.md) | Agenten löschen versehentlich Daten/Code, ignorieren Stopp-Befehle, arbeiten ohne Rollback | Safety-Net für hoch-autonome Coding-Agenten: Dry-Run, Backups, Stopp-Erzwingung, Verifikation |
| [`agent-token-budget`](skills/agent-token-budget/SKILL.md) | Agenten verbrennen Token: Endlos-Narration, Repo-Re-Reads, Wiederholungen | Hartes Budget setzen, Kontext-Lese-Limits, Narration unterdrücken, Messen & Loggen |
| [`obsidian-wissensbasis`](skills/obsidian-wissensbasis/SKILL.md) | Agenten vergessen dein Wissen zwischen Sessions, Kontext fehlt | Obsidian-Vault als zweites Gedächtnis: Struktur, Agent-Zugriff (suchen/lesen/schreiben), Backup-Workflow |

*Weitere kommen laufend hinzu.*

---

*Verwandt: [hermes-control-center](https://github.com/tolouiluxury-creator/hermes-control-center) — Dashboard für einen zentralen Agenten.*