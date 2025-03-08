# Breadth-First Search (BFS) – Detaillierte Erklärung

## 1. Was ist BFS?
Breadth-First Search (BFS) ist ein Algorithmus zur Traversierung oder Suche in einem Graphen oder Baum. BFS arbeitet schichtweise: zuerst werden alle direkten Nachbarn eines Knotens besucht, dann deren Nachbarn usw., bis alle erreichbaren Knoten besucht wurden.

## 2. Was brauchen wir in unserem Code?
Um BFS umzusetzen, brauchen wir folgende Konzepte in C#:

  ✅ Einen Graphen – eine Datenstruktur, die speichert, welche Knoten verbunden sind. 
  
  ✅ Eine Warteschlange (Queue) – damit BFS weiß, welcher Knoten als nächstes besucht wird.
  
  ✅ Eine Liste der besuchten Knoten – um doppelte Besuche zu vermeiden.
  
  ✅ Eine Schleife – die durch den Graphen läuft und BFS ausführt.

## 3. Beispiel für BFS
### Graph-Struktur:
```
    A
   / \
  B   C
 / \   \
D   E   F
```
BFS-Traversierung ab `A`: **A → B → C → D → E → F**

## 4. Vergleich von BFS mit anderen Algorithmen
| Algorithmus | Strategie | Speicherverbrauch | Beste Anwendung |
|------------|----------|----------------|-----------------|
| **BFS** | Schichtweise (breit zuerst) | Hoch (merkt sich viele Knoten) | Kürzeste Wege in ungewichteten Graphen, Level-Order Traversierung |
| **DFS** | Tief zuerst | Gering (nur ein Pfad im Speicher) | Wenn der Graph groß ist und wir nur einen Pfad brauchen |
| **Dijkstra** | Kürzester Pfad mit Gewichten | Mittel-Hoch | Wenn Kanten unterschiedlich lange Wege haben |
| **A*** | Kürzester Pfad mit Heuristik | Hoch | Intelligente Wegfindung (z. B. Google Maps) |

## 5. Wann ist BFS sinnvoll?
| Anwendungsfall | Warum BFS? |
|--------------|----------|
| Kürzeste Wege in ungewichteten Graphen | BFS findet den kürzesten Pfad zuverlässig |
| Erreichbarkeit von Knoten | BFS kann prüfen, ob ein Knoten von einem anderen aus erreichbar ist |
| Level-Order Traversierung in Bäumen | BFS besucht Knoten Ebene für Ebene |
| Rätsel oder Spiele mit begrenzten Zügen | BFS findet die schnellste Lösung |

## 6. Wann ist BFS nicht geeignet?
| Problem | Besserer Algorithmus |
|---------|-------------------|
| Kanten haben unterschiedliche Gewichte | **Dijkstra oder A*** |
| Graph ist sehr groß | **DFS oder bidirektionale Suche** |
| Lösung liegt tief im Baum | **Iterative Deepening DFS (IDDFS)** |

## 7. BFS-Implementierung in C#
```csharp
using System;
using System.Collections.Generic;

class Program
{
    static void BFS(Dictionary<char, List<char>> graph, char start)
    {
        Queue<char> queue = new Queue<char>();
        HashSet<char> visited = new HashSet<char>();

        queue.Enqueue(start);
        visited.Add(start);

        while (queue.Count > 0)
        {
            char node = queue.Dequeue();
            Console.Write(node + " ");

            foreach (char neighbor in graph[node])
            {
                if (!visited.Contains(neighbor))
                {
                    queue.Enqueue(neighbor);
                    visited.Add(neighbor);
                }
            }
        }
    }

    static void Main()
    {
        Dictionary<char, List<char>> graph = new Dictionary<char, List<char>>
        {
            {'A', new List<char> { 'B', 'C' }},
            {'B', new List<char> { 'A', 'D', 'E' }},
            {'C', new List<char> { 'A', 'F' }},
            {'D', new List<char> { 'B' }},
            {'E', new List<char> { 'B' }},
            {'F', new List<char> { 'C' }}
        };

        Console.WriteLine("BFS Traversierung ab Knoten A:");
        BFS(graph, 'A');
    }
}
```

## 8. Fazit: Wann sollte ich BFS nutzen?
✔ **Ja, wenn:**
- Du den kürzesten Weg in einem ungewichteten Graphen suchst.
- Du wissen willst, ob zwei Knoten verbunden sind.
- Du eine Level-Order Traversierung eines Baums brauchst.
- Das Problem überschaubar groß ist.

❌ **Nein, wenn:**
- Kanten unterschiedliche Gewichte haben (Dijkstra ist besser).
- Der Graph sehr groß ist (DFS oder heuristische Algorithmen sind besser).
- Die Lösung tief im Baum liegt (DFS oder A* ist besser).

---
Hast du Fragen oder brauchst du weitere Erklärungen? 😊
