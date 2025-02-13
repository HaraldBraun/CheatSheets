### HTTP CRUD CheatSheet

| HTTP-Methode | Funktion | Beschreibung | Vorteile | Nachteile |
|--------------|----------|--------------|----------|-----------|
| **GET**      | Read     | Fordert Daten von einem Server an. Typischerweise verwendet, um Ressourcen abzurufen oder anzuzeigen. | Einfach zu implementieren. Keine Seiteneffekte auf dem Server. | Daten sind in der URL sichtbar, begrenzte Datenmenge aufgrund der URL-Länge. |
| **POST**     | Create   | Sendet Daten an den Server, um eine neue Ressource zu erstellen. Wird verwendet, um Daten zu senden, die auf dem Server gespeichert oder verarbeitet werden sollen. | Ermöglicht das Senden großer Datenmengen. Verschiedene Formate (z. B. JSON, XML) können verwendet werden. | Kann Seiteneffekte auf dem Server haben. Erhöhtes Sicherheitsrisiko (z. B. CSRF). |
| **PUT**      | Update   | Aktualisiert eine vorhandene Ressource vollständig mit den bereitgestellten Daten. Wird verwendet, um eine Ressource zu ersetzen. | Klarheit über die Aktualisierung der gesamten Ressource. | Erfordert vollständige Darstellung der Ressource. Kann zu Datenverlust führen, wenn nicht alle Felder bereitgestellt werden. |
| **DELETE**   | Delete   | Löscht eine vorhandene Ressource auf dem Server. Wird verwendet, um Daten zu entfernen. | Einfach zu implementieren. Entfernt unnötige Daten. | Kann Daten unwiederbringlich löschen. Erhöhtes Sicherheitsrisiko (z. B. unbefugtes Löschen). |

### Detaillierte Erklärungen

**GET:**
- **Funktion:** Abrufen von Daten
- **Beschreibung:** Die GET-Methode fordert eine bestimmte Ressource vom Server an. Sie wird häufig verwendet, um Daten anzuzeigen oder zu lesen.
- **Vorteile:**
  - Einfach zu implementieren
  - Keine Seiteneffekte auf dem Server (keine Datenänderung)
- **Nachteile:**
  - Daten werden in der URL sichtbar, was die Sicherheit beeinträchtigen kann
  - Begrenzte Datenmenge aufgrund der URL-Länge

**POST:**
- **Funktion:** Erstellen von Daten
- **Beschreibung:** Die POST-Methode sendet Daten an den Server, um eine neue Ressource zu erstellen. Sie wird verwendet, um Daten zu übermitteln, die auf dem Server gespeichert werden sollen.
- **Vorteile:**
  - Ermöglicht das Senden großer Datenmengen
  - Verschiedene Datenformate (z. B. JSON, XML) können verwendet werden
- **Nachteile:**
  - Kann Seiteneffekte auf dem Server haben (z. B. Datenänderung)
  - Erhöhtes Sicherheitsrisiko (z. B. Cross-Site Request Forgery, CSRF)

**PUT:**
- **Funktion:** Aktualisieren von Daten
- **Beschreibung:** Die PUT-Methode aktualisiert eine vorhandene Ressource vollständig mit den bereitgestellten Daten. Sie ersetzt die gesamte Ressource.
- **Vorteile:**
  - Klarheit über die Aktualisierung der gesamten Ressource
- **Nachteile:**
  - Erfordert vollständige Darstellung der Ressource
  - Kann zu Datenverlust führen, wenn nicht alle Felder bereitgestellt werden

**DELETE:**
- **Funktion:** Löschen von Daten
- **Beschreibung:** Die DELETE-Methode löscht eine vorhandene Ressource auf dem Server. Sie wird verwendet, um Daten zu entfernen.
- **Vorteile:**
  - Einfach zu implementieren
  - Entfernt unnötige Daten
- **Nachteile:**
  - Kann Daten unwiederbringlich löschen
  - Erhöhtes Sicherheitsrisiko (z. B. unbefugtes Löschen)
