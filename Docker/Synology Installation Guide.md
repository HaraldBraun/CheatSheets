# Docker auf einer Synology NAS nutzen

Diese Anleitung beschreibt die Nutzung von Docker auf einer **Synology NAS** mit **DSM (DiskStation Manager)**. Sie deckt die grundlegende Bedienung über die DSM-Oberfläche sowie die Installation von **NGINX** und **Portainer** ab.

## **1. Installation von Docker**
Falls Docker nicht installiert ist:
1. Öffne das **Paket-Zentrum** in der DSM-Oberfläche deiner NAS.
2. Suche nach **Docker** und installiere es.
3. Nach der Installation findest du die **Docker-Anwendung** im Hauptmenü.

---

## **2. Überblick über die Docker-Oberfläche**
Nach dem Öffnen der Docker-Anwendung gibt es mehrere Registerkarten:
- **Übersicht**: Status der laufenden Container.
- **Container**: Alle gestarteten oder gestoppten Container.
- **Registrierung**: Suche und lade Container-Images aus Docker Hub.
- **Image**: Verwaltung der heruntergeladenen Images.
- **Netzwerk**: Netzwerkkonfiguration der Container.
- **Protokoll**: Protokolle zu Containern.

---

## **3. Warum NGINX und Portainer installieren?**
### **3.1. Warum NGINX?**
NGINX ist ein **leichter, schneller und flexibler Webserver**, der sich für verschiedene Aufgaben eignet:
- **Reverse Proxy**: Vermittelt Anfragen an interne Dienste, sodass sie unter einer einzigen Domain erreichbar sind.
- **Load Balancer**: Verteilt Traffic gleichmäßig über mehrere Server.
- **Statische Webseiten hosten**: Ideal für einfache Websites oder Web-Apps.
- **TLS/SSL-Verschlüsselung**: Ermöglicht HTTPS mit Let's Encrypt.

Auf einer Synology NAS kann NGINX nützlich sein, um:  
✅ Webanwendungen zu hosten.  
✅ Einen sicheren Zugang zu internen Diensten per Reverse Proxy zu ermöglichen.  
✅ Die Performance und Sicherheit von Webanfragen zu verbessern.  

### **3.2. Warum Portainer?**
Portainer ist eine **grafische Benutzeroberfläche für Docker**, die die Verwaltung von Containern erleichtert. Die Standard-Docker-Oberfläche auf der Synology NAS ist eingeschränkt – Portainer bietet deutlich mehr Funktionen.

Mit Portainer kannst du:
- Container starten, stoppen und verwalten, ohne die DSM-Docker-GUI zu nutzen.
- **Docker-Compose nutzen**, um mehrere Container mit einer einzigen Datei zu verwalten.
- Logs, Netzwerke, Volumes und Images einfach über das Webinterface managen.
- Direkt über den Browser auf deine Container zugreifen.

Portainer ist besonders hilfreich, wenn du **mehrere Container betreibst** oder tiefer in Docker einsteigen möchtest.

---

## **4. Einen Container installieren und starten**
### **4.1. Image herunterladen**
1. Öffne den Tab **Registrierung**.
2. Suche nach einem Container-Image, z. B. `nginx` oder `portainer/portainer-ce`.
3. Wähle das gewünschte Image aus und klicke auf **Download**.
4. Wähle die gewünschte Version (z. B. `latest`).

### **4.2. Container erstellen**
1. Öffne den Tab **Image**.
2. Wähle das heruntergeladene Image aus und klicke auf **Starten**.
3. Konfiguriere den Container:
   - **Container-Name**: Beliebiger Name.
   - **Netzwerk**: Standardmäßig „bridge“.
   - **Port-Einstellungen**: Falls nötig, hostseitige Ports anpassen.
   - **Volume**: Ordner von der NAS mit dem Container verbinden.
4. Klicke auf **Übernehmen**, um den Container zu starten.

---

## **5. Portainer als Web-GUI für Docker installieren**
### **5.1. Portainer starten**
1. Lade das `portainer/portainer-ce` Image über die **Registrierung** herunter.
2. Erstelle einen neuen Container mit folgenden Einstellungen:
   - **Port**: 9000:9000
   - **Volume**: `/var/run/docker.sock → /var/run/docker.sock` (Docker-API-Zugriff)
3. Starte den Container und rufe **http://[NAS-IP]:9000** im Browser auf.

### **5.2. Portainer einrichten**
1. Erstelle ein Administrator-Konto.
2. Wähle „Docker“ als Umgebung.
3. Klicke auf „Verbinden“, um das Dashboard zu nutzen.

---

## **6. Verwaltung der Container**
- **Container starten/stoppen**: Im Reiter **Container** den gewünschten Container auswählen und auf **Starten** oder **Stoppen** klicken.
- **Logs anzeigen**: Wähle den Container aus und gehe auf den Tab **Protokoll**.
- **Container löschen**: Stoppe den Container, dann klicke auf **Aktion → Löschen**.

---

## **7. Fazit**
- **NGINX** = Webserver & Reverse Proxy → Perfekt, um interne Dienste übers Internet bereitzustellen.
- **Portainer** = Docker-GUI → Erleichtert die Verwaltung deiner Container.
