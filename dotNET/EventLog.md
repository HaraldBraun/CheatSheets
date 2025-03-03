```markdown
# CheatSheet: Erstellung eines EventLogs

## Schritte zur Erstellung eines neuen EventLogs

1. **Öffne die Eingabeaufforderung als Administrator**:
   - Drücke `Win + X` und wähle "Eingabeaufforderung (Administrator)" oder "Windows PowerShell (Administrator)".

2. **Erstelle das neue Eventlog**:
   ```powershell
   New-EventLog -LogName "MeinNeuesLog" -Source "MeineQuelle"
   ```
   - `LogName` ist der Name des neuen Logs.
   - `Source` ist die Quelle, die Ereignisse in dieses Log schreibt.

3. **Überprüfe die Erstellung des Logs**:
   ```powershell
   Get-EventLog -List | Where-Object { $_.Log -eq "MeinNeuesLog" }
   ```

4. **Schreibe ein Testereignis in das neue Log**:
   ```powershell
   Write-EventLog -LogName "MeinNeuesLog" -Source "MeineQuelle" -EventID 1000 -EntryType Information -Message "Dies ist ein Testereignis."
   ```

5. **Öffne die Ereignisanzeige**:
   - Drücke `Win + R`, gib `eventvwr` ein und drücke `Enter`.
   - Navigiere zu deinem neuen Log unter "Anwendungs- und Dienstprotokolle".

## Erstellung eines EventLogs während der Installation einer Anwendung

1. **Erstelle eine Funktion zur Erstellung des EventLogs**:
   ```csharp
   using System;
   using System.Diagnostics;

   public class EventLogInstaller
   {
       public static void CreateEventLog()
       {
           string logName = "MeinNeuesLog";
           string sourceName = "MeineQuelle";

           if (!EventLog.SourceExists(sourceName))
           {
               EventLog.CreateEventSource(sourceName, logName);
               Console.WriteLine("Event Source Created");
           }
           else
           {
               Console.WriteLine("Event Source already exists");
           }
       }
   }
   ```

2. **Rufe die Funktion während der Installation auf**:
   - Füge den Aufruf der `CreateEventLog`-Funktion in das Installationsskript oder die Setup-Routine deiner Anwendung ein.

3. **Wartezeit einbauen (optional)**:
   - Um sicherzustellen, dass das Eventlog registriert ist, kannst du eine kurze Wartezeit einbauen:
   ```csharp
   using System.Threading;

   public class EventLogInstaller
   {
       public static void CreateEventLog()
       {
           string logName = "MeinNeuesLog";
           string sourceName = "MeineQuelle";

           if (!EventLog.SourceExists(sourceName))
           {
               EventLog.CreateEventSource(sourceName, logName);
               Console.WriteLine("Event Source Created");
           }
           else
           {
               Console.WriteLine("Event Source already exists");
           }

           // Wartezeit einbauen
           Thread.Sleep(5000); // 5 Sekunden warten
       }
   }
   ```

4. **Schreibe ein Testereignis nach der Installation**:
   ```csharp
   public class EventLogTester
   {
       public static void WriteTestEvent()
       {
           string logName = "MeinNeuesLog";
           string sourceName = "MeineQuelle";

           EventLog eventLog = new EventLog();
           eventLog.Source = sourceName;
           eventLog.Log = logName;

           eventLog.WriteEntry("Dies ist ein Testereignis.", EventLogEntryType.Information, 1000);
           Console.WriteLine("Ereignis geschrieben");
       }
   }
   ```

