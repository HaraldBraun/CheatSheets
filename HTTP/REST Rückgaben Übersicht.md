**GET - Erfolgreiche Antworten**

| Rückgabeart | Code | Wann verwenden? |
|-------------|------|----------------|
| OK | 200 | Die Anfrage war erfolgreich, und die Antwort enthält die angeforderten Daten. |
| No Content | 204 | Die Anfrage war erfolgreich, aber es gibt keine zurückzugebenden Daten. |

**POST - Erfolgreiche Antworten**

| Rückgabeart | Code | Wann verwenden? |
|-------------|------|----------------|
| Created | 201 | Die Anfrage war erfolgreich, und eine neue Ressource wurde erstellt. |
| Accepted | 202 | Die Anfrage wurde akzeptiert, aber die Verarbeitung ist noch nicht abgeschlossen. |

**PUT - Erfolgreiche Antworten**

| Rückgabeart | Code | Wann verwenden? |
|-------------|------|----------------|
| OK | 200 | Die Ressource wurde erfolgreich aktualisiert, und die Antwort enthält die aktualisierten Daten. |
| No Content | 204 | Die Ressource wurde erfolgreich aktualisiert, aber es gibt keine zurückzugebenden Daten. |

**Fehlermeldungen und Empfehlungen**

| Rückgabeart | Code | Wann verwenden? |
|-------------|------|----------------|
| Bad Request | 400 | Die Anfrage ist fehlerhaft oder unvollständig. Empfohlen für ungültige oder fehlende Parameter. |
| Unauthorized | 401 | Authentifizierung erforderlich oder fehlgeschlagen. |
| Forbidden | 403 | Der Benutzer hat keine Berechtigung für die angeforderte Ressource. |
| Not Found | 404 | Die angeforderte Ressource wurde nicht gefunden. |
| Method Not Allowed | 405 | Die HTTP-Methode ist für diese Ressource nicht erlaubt. |
| Conflict | 409 | Konflikt mit dem aktuellen Zustand der Ressource (z. B. doppelte Einträge). |
| Internal Server Error | 500 | Ein unerwarteter Fehler auf dem Server ist aufgetreten. |
| Service Unavailable | 503 | Der Server ist vorübergehend nicht verfügbar, z. B. wegen Wartungsarbeiten. |
