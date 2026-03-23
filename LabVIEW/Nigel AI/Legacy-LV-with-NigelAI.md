# Dokumentation eines Legacy‑LabVIEW‑Projekts mit Nigel™ AI  
### Schritt‑für‑Schritt‑Anleitung

---

## 1. Vorbereitung

### 1.1 Projekt bereinigen
- Unbenutzte VIs identifizieren und auslagern  
- Alte Test‑ oder Debug‑VIs markieren  
- Build‑Spezifikationen prüfen (EXE, Installer, PPLs)

### 1.2 Dokumentationsziel definieren
- Umfang festlegen: produktiver Code vs. gesamtes Projekt  
- Zielstruktur: Markdown‑Dokumentation, später optional PDF/Wiki

### 1.3 Ordnerstruktur anlegen
```text
docs/
  00_Overview.md
  10_Modules/
  20_VIs/
  30_Crosscutting/
```


---

## 2. Architektur grob erfassen

### 2.1 Projektübersicht mit Nigel erzeugen
**Frage an Nigel:**
> „Analysiere dieses Projekt und beschreibe mir die grobe Architektur, Hauptmodule und Datenflüsse in Markdown.“

Ergebnis in `00_Overview.md` speichern.

### 2.2 Funktionale Bereiche identifizieren
**Frage an Nigel:**
> „Welche funktionalen Bereiche erkennst du in diesem Projekt? Bitte als Markdown‑Liste.“

Typische Bereiche:
- Messung  
- Regelung  
- UI  
- Logging  
- Kommunikation  
- Fehlerbehandlung  

Diese als Kapitel in `00_Overview.md` ergänzen.

---

## 3. Modulweise Dokumentation

### 3.1 VIs pro Modul sammeln
**Frage an Nigel:**
> „Liste alle VIs auf, die zur Messfunktionalität gehören, und ordne sie nach Rolle (Top‑Level, SubVI, Helper).“

### 3.2 Modul‑Steckbrief erstellen
**Frage an Nigel:**
> „Erstelle eine Markdown‑Dokumentation für das Messmodul: Zweck, Haupt‑VIs, Datenflüsse, Schnittstellen, Abhängigkeiten.“

Speichern unter:  
`docs/10_Modules/Messung.md`

---

## 4. VI‑Ebene detailliert dokumentieren

### 4.1 Jedes VI einzeln dokumentieren
Für jedes relevante VI:

**Frage an Nigel:**
> „Dokumentiere dieses VI vollständig in Markdown: Zweck, Inputs, Outputs, interne Logik, Fehlerbehandlung, Abhängigkeiten, verwendete globale Variablen/Queues/Events.“

Speichern unter:  
`docs/20_VIs/<Modul>_<VI-Name>.md`

### 4.2 Aufrufhierarchien erfassen
**Frage an Nigel:**
> „Zeige mir die Aufrufhierarchie für dieses VI in Markdown.“

In Modul‑ oder VI‑Dokumentation einfügen.

---

## 5. Querschnittsthemen dokumentieren

### 5.1 Globale Variablen & Shared State
**Frage an Nigel:**
> „Liste alle globalen Variablen und deren Verwendung im Projekt in Markdown auf.“

Speichern unter:  
`docs/30_Crosscutting/Globals.md`

### 5.2 Kommunikationsmechanismen
**Frage an Nigel:**
> „Dokumentiere alle Kommunikationsmechanismen (Queues, Events, TCP/UDP, Feldbus, etc.) in Markdown.“

Speichern unter:  
`docs/30_Crosscutting/Communication.md`

### 5.3 Fehlerbehandlung & Logging
**Frage an Nigel:**
> „Beschreibe das Fehlerhandling‑Konzept und das Logging‑Verhalten dieses Projekts in Markdown.“

---

## 6. Konsolidierung & Review

### 6.1 Vollständigkeit prüfen
- Sind alle produktiven VIs dokumentiert?  
- Sind alle Module beschrieben?  
- Gibt es VIs ohne Modulzuordnung?

### 6.2 Lücken mit Nigel finden
**Frage an Nigel:**
> „Gibt es VIs im Projekt, die noch nicht in der Dokumentation erwähnt sind? Liste sie in Markdown.“

### 6.3 Finale Spezifikation erstellen
- Markdown‑Dateien zusammenführen  
- Optional nach PDF exportieren (z. B. Pandoc, VS Code, Typora, Word)

---

## 7. Optional: Verantwortlichkeiten ergänzen

### 7.1 Zuständigkeiten ableiten
**Frage an Nigel:**
> „Ordne die Module und VIs nach funktionalen Zuständigkeiten und erstelle eine Übersicht in Markdown.“

In `00_Overview.md` als Kapitel „Zuständigkeiten“ ergänzen.
