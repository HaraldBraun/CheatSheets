# Aufzählung der klassischen Grundmuster für die Einteilung eines Applikationsfensters

## 1. **Das BorderLayout (5 Bereiche)**  
Es teilt das Fenster in Himmelsrichtungen ein:
* **North (Norden):** Meist für die Menüleiste oder Toolbar reserviert.
* **South (Süden):** Ort für die Statuszeile oder ergänzende Informationen.
* **West (Westen):** Platz für Navigationsbäume oder Seitenleisten.
* **East (Osten):** Bereich für sekundäre Werkzeuge, Eigenschaften-Paletten oder Werbung.
* **Center (Zentrum):** Der Hauptarbeitsbereich, der den verbleibenden Platz einnimmt.
  
## 2. **Das GridLayout (Raster)**  
Das Fenster wird in ein strenges Raster aus gleich großen Zellen unterteilt (z. B. 2x2, 3x3).
* **Einsatz:** Taschenrechner, Bildergalerien oder Dashboard-Kacheln. Jedes Element hat die exakt gleiche Gewichtung.
  
## 3. **Das FlowLayout (Fluss-Prinzip)**  
Die Elemente werden wie Wörter in einem Text nebeneinander angeordnet. Wenn eine Zeile voll ist, bricht der Inhalt in die nächste Zeile um.
* **Einsatz:** Werkzeugleisten mit vielen kleinen Icons oder Tag-Listen.
  
## 4. **Das CardLayout (Stapel-Prinzip)**  
Hier liegen verschiedene Bereiche übereinander wie in einem Stapel Spielkarten. Es ist immer nur ein Bereich (eine "Karte") gleichzeitig sichtbar.
* **Einsatz:** Installations-Assistenten ("Weiter"-Buttons), Tab-Panels oder die Einstellungen in mobilen Apps.
  
## 5. **Das BoxLayout (Achsen-Prinzip)**  
Die Komponenten werden entweder streng vertikal (untereinander) oder horizontal (nebeneinander) angeordnet, ohne Umbruch.
* **Einsatz:** Einfache Seitenmenüs oder Login-Masken.
  
## 6. **Das GridBagLayout (Flexibles Raster)**  
Dies ist die komplexe Weiterentwicklung des GridLayouts. Ein Element kann mehrere Zeilen oder Spalten gleichzeitig einnehmen (z. B. ein Header, der über drei Spalten geht).
* **Einsatz:** Komplexe Formulare oder professionelle Software-Interfaces (wie IDEs oder Videoschnittprogramme).
  
