# Collection of CheatSheets

Eine Sammlung von CheatSheets und Abläufen für verschiedene Themenbereiche.

## 📂 Struktur

Das Repository ist in folgende Hauptbereiche unterteilt:

- [**Algorithmen/Search**](./Algorithms/Search) – Wichtige Suchalgorithmen und deren Erklärungen.
- [**HTTP/Rest Operations**](./HTTP) – Befehle und Abläufe für HTTP- und REST-Operationen.
- [**Docker**](./Docker) – Nützliche Befehle und Abläufe zur Container-Verwaltung und -Einrichtung.
- [**.NET**](./dotNet) – Wichtige .NET-spezifische Befehle und Konzepte.

Jeder dieser Bereiche kann weitere Unterordner mit spezifischen Themen enthalten.

## 🔍 Nutzung

Einfach die gewünschten Markdown-Dateien im entsprechenden Ordner öffnen und nutzen. Die Dateien enthalten kompakte Anleitungen und Befehle für den jeweiligen Bereich.

## 💡 Beiträge (Contributing)

Ich arbeite derzeit allein an diesem Repository, aber jeder ist willkommen, sich zu beteiligen!

Falls du neue CheatSheets hinzufügen oder bestehende verbessern möchtest:

1. Stelle sicher, dass dein Beitrag in Markdown (`.md`) verfasst ist.
2. Nutze eine einheitliche Struktur (z. B. Abschnittsüberschriften, Codeblöcke für Befehle).
3. Füge neue Inhalte in den passenden Unterordner ein oder erstelle ggf. eine neue Kategorie.
4. Öffne einen Pull Request mit einer kurzen Beschreibung deiner Änderungen.

### 📝 Formatierungs- und Strukturvorschläge

Diese Vorschläge sollen helfen, eine einheitliche Struktur beizubehalten, sind aber nicht zwingend erforderlich:

- **Dateinamen:** Verwende kurze, aber aussagekräftige Namen (z. B. `docker-commands.md` statt `commands.md`).
- **Abschnitte:** Strukturiere dein CheatSheet mit sinnvollen Überschriften (`## Hauptthema`, `### Unterthema`).
- **Codeblöcke:** Nutze ``` für Codebeispiele und gib die Sprache an, z. B.:
  
  ```bash
  docker ps -a
  ```
- **Listen:** Verwende Aufzählungen (`-` oder `1.`) für Schritt-für-Schritt-Anleitungen.
- **Konsistente Schreibweise:** Vermeide gemischte Begriffe (z. B. `Docker Image` vs. `Docker-Image`).
- **Verweise:** Falls dein Beitrag auf ein anderes CheatSheet verweist, nutze relative Links, z. B.:  
  `[Siehe Docker-Befehle](../Docker/docker-commands.md)`

### 🔍 Automatische Prüfungen

Um eine einheitliche Formatierung und Struktur sicherzustellen, können folgende Tools genutzt werden:

- **Markdownlint**: Prüft die Einhaltung von Markdown-Standards.
- **Prettier**: Formatiert Markdown-Dateien automatisch.
- **Vale**: Ermöglicht eine konsistente Schreibweise und Stilprüfung.

Falls du Änderungen vorschlägst, kannst du diese Tools lokal ausführen, um sicherzustellen, dass dein Beitrag den Richtlinien entspricht.
Falls du dir nicht sicher bist, kannst du auch einen anderen für die Prüfung des Dokumentes eintragen bevor du einen Push durchführst.

## 📜 Lizenz

Dieses Repository enthält frei verfügbare Informationen und ist zur Nutzung und Erweiterung gedacht.
