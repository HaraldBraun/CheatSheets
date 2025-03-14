# Erstellung eines Docker-Containers mit Visual Studio

Diese Anleitung beschreibt die Erstellung eines Docker-Containers für ein **Visual Studio**-Projekt. Sie umfasst die Grundlagen eines **Dockerfiles**, notwendige und optionale Schritte sowie die Nutzung einer `.dockerignore`-Datei. Außerdem wird erläutert, ob Docker Desktop erforderlich ist, wenn Docker bereits auf einer **Synology NAS** installiert ist.

---

## **1. Voraussetzungen**
Bevor du startest, stelle sicher, dass du folgende Tools installiert hast:
- **Visual Studio** (ab Version 2019 mit Docker-Unterstützung)
- **Docker Desktop** (nur erforderlich für lokale Entwicklung, siehe Abschnitt 8)
- **Docker auf einer Synology NAS** (falls du die NAS als Build- und Laufzeitumgebung nutzen möchtest)
- **.NET SDK** (falls ein .NET-Projekt containerisiert wird)

Falls Docker in Visual Studio nicht aktiviert ist:
1. Öffne **Visual Studio Installer**.
2. Wähle deine **Visual Studio-Installation** aus.
3. Aktiviere die Option **Containerentwicklungstools**.

---

## **2. Was ist ein Dockerfile?**
Ein **Dockerfile** ist eine Skriptdatei, die Anweisungen enthält, um ein Docker-Image zu erstellen. Es definiert:
- Die **Basis** des Images (z. B. ein Betriebssystem oder eine Laufzeitumgebung wie `mcr.microsoft.com/dotnet/aspnet`)
- **Abhängigkeiten** und **Konfigurationsdateien**
- Den **Build-Prozess**
- Den **Startbefehl** für den Container

---

## **3. Erstellung eines Dockerfiles für Visual Studio**
### **3.1. Notwendige Schritte**
Ein **Dockerfile** sollte mindestens folgende Schritte enthalten:
1. **Base Image definieren** (z. B. ein .NET- oder Node.js-Image).
2. **Arbeitsverzeichnis erstellen** (`WORKDIR`).
3. **Abhängigkeiten kopieren und installieren** (`COPY` und `RUN`).
4. **Den Code kopieren und kompilieren** (`COPY`, `RUN dotnet build`).
5. **Den Container-Startbefehl setzen** (`CMD` oder `ENTRYPOINT`).

### **3.2. Optionale Schritte**
- **Mehrstufiger Build**: Spart Speicherplatz und optimiert den Container.
- **Portfreigaben**: Ermöglicht Zugriff auf den Container (`EXPOSE`).
- **Umgebungsvariablen setzen** (`ENV`).
- **Datenvolumen definieren** (`VOLUME`).

---

## **4. Beispiel für ein Dockerfile**
Hier ein Beispiel für eine **ASP.NET Core**-Anwendung:

```dockerfile
# Basis-Image für die Laufzeit
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS base
WORKDIR /app
EXPOSE 80

# Build-Image
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY ["MyProject/MyProject.csproj", "MyProject/"]
RUN dotnet restore "MyProject/MyProject.csproj"
COPY . .
WORKDIR "/src/MyProject"
RUN dotnet build --no-restore -c Release -o /app/build

# Publish
FROM build AS publish
RUN dotnet publish -c Release -o /app/publish --no-restore

# Laufzeit-Container
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "MyProject.dll"]
```

### **Erklärung:**
- **`FROM base`**: Das Laufzeit-Image wird definiert.
- **`FROM build`**: Enthält das SDK zum Kompilieren der Anwendung.
- **`dotnet restore` & `dotnet build`**: Installiert Abhängigkeiten und kompiliert den Code.
- **`dotnet publish`**: Veröffentlicht die Anwendung.
- **`COPY --from=publish`**: Kopiert nur die endgültige Anwendung ins Basis-Image.

---

## **5. Was ist eine .dockerignore-Datei?**
Ähnlich wie eine `.gitignore`, verhindert eine `.dockerignore`, dass bestimmte Dateien ins Docker-Image aufgenommen werden. Dies spart Speicherplatz und verbessert die Performance.

### **Typische Einträge in einer .dockerignore:**
```plaintext
bin/
obj/
.vscode/
.git/
.dockerignore
Dockerfile
node_modules/
```

Diese Datei verhindert, dass temporäre Dateien oder Build-Artefakte in das Image gelangen.

---

## **6. Container mit Visual Studio erstellen und ausführen**
### **6.1. Container-Support aktivieren**
Falls nicht bereits aktiviert:
1. Öffne dein **Visual Studio-Projekt**.
2. Klicke mit der rechten Maustaste auf das **Projekt** → **Container-Orchestrierung hinzufügen**.
3. Wähle **Docker** als Zielumgebung.
4. Wähle das **richtige Basis-Image** (Linux oder Windows).

### **6.2. Container über Visual Studio starten**
1. Wähle oben in Visual Studio **Docker** als Startoption.
2. Klicke auf **Starten (F5)**.
3. Visual Studio erstellt das Docker-Image und startet den Container.

### **6.3. Container über die CLI starten** *(optional)*
Falls du die Befehlszeile nutzen möchtest, kannst du dein Image manuell bauen und starten:

```sh
# Image bauen
docker build -t myproject .

# Container starten
docker run -d -p 8080:80 --name mycontainer myproject
```

---

## **7. Ist Docker Desktop notwendig, wenn Docker auf einer Synology NAS installiert ist?**
### **Nein, Docker Desktop ist nicht notwendig**, wenn Docker bereits auf deiner **Synology NAS** installiert ist. 

Docker Desktop wird hauptsächlich für lokale Entwicklungsumgebungen auf **Windows oder macOS** genutzt, während die Synology NAS eine eigenständige Docker-Engine bereitstellt.

### **Wann brauchst du Docker Desktop?**
- **Wenn du lokal auf deinem PC entwickelst** und Container testen möchtest, bevor du sie auf die NAS überträgst.
- **Wenn du Visual Studio oder eine andere IDE verwendest**, die eine lokale Docker-Umgebung erfordert.
- **Wenn du Kubernetes oder erweiterte Entwicklungs-Tools von Docker Desktop nutzen möchtest**.

### **Wann reicht Docker auf der Synology NAS?**
- **Wenn du Container nur auf der NAS betreiben möchtest** (ohne lokale Entwicklung).
- **Wenn du die Docker-CLI oder Portainer zur Verwaltung nutzt**.
- **Wenn du ein leichtgewichtiges Setup ohne zusätzliche Software auf dem PC bevorzugst**.

Falls du Visual Studio mit Docker nutzen möchtest, aber die NAS als **Build- und Laufzeitumgebung** verwenden willst, kannst du deinen PC per **Remote-Docker** mit der Synology NAS verbinden.

---

## **8. Fazit**
- Ein **Dockerfile** definiert die Umgebung für den Container.
- Ein **mehrstufiger Build** reduziert die Image-Größe.
- Eine **`.dockerignore`**-Datei hilft, unnötige Dateien auszuschließen.
- Visual Studio kann Container automatisch erstellen und verwalten.
- **Docker Desktop ist nicht notwendig, wenn Docker auf einer Synology NAS genutzt wird**.
