
## **1️⃣ Benötigte Pakete installieren**  
Führe folgende Befehle im Projektordner aus:  
```bash
dotnet add package Microsoft.EntityFrameworkCore
dotnet add package Pomelo.EntityFrameworkCore.MySql
dotnet add package Microsoft.EntityFrameworkCore.Design
dotnet add package Microsoft.EntityFrameworkCore.Tools
```

Falls EF-Tools noch nicht installiert sind, installiere sie mit:  
```bash
dotnet tool install --global dotnet-ef
```

---

## **2️⃣ Verbindung zur bestehenden MariaDB in `appsettings.json` eintragen**  
Öffne `appsettings.json` und füge die **Connection String** hinzu:  
```json
"ConnectionStrings": {
  "DefaultConnection": "Server=localhost;Port=3306;Database=ProductDb;User=root;Password=root;"
}
```
🛠 **Falls nötig anpassen:**  
- `Server=localhost` → Ersetze `localhost` mit der tatsächlichen IP/Domain.  
- `Database=ProductDb` → Ersetze `ProductDb` mit der bestehenden Datenbank.  
- `User=root;Password=root` → Benutzername & Passwort entsprechend ändern.

---

## **3️⃣ `DbContext` aus der bestehenden Datenbank generieren**  
Verwende den folgenden Befehl, um die Model-Klassen und den `DbContext` aus der bestehenden Datenbank zu erstellen:  
```bash
dotnet ef dbcontext scaffold "Server=localhost;Port=3306;Database=ProductDb;User=root;Password=root;" Pomelo.EntityFrameworkCore.MySql -o Models --context ApplicationDbContext --force
```
🔹 **Erklärung:**  
- `"Server=localhost;Port=3306;Database=ProductDb;User=root;Password=root;"` → Verbindung zur bestehenden MariaDB  
- `Pomelo.EntityFrameworkCore.MySql` → Der MariaDB-Provider für EF Core  
- `-o Models` → Model-Klassen im Ordner `Models` speichern  
- `--context ApplicationDbContext` → Der generierte `DbContext` heißt `ApplicationDbContext`  
- `--force` → Falls bereits Model-Klassen existieren, diese überschreiben  

✅ **Nach diesem Schritt wurden folgende Dateien erstellt:**  
- `Models/ApplicationDbContext.cs` (Datenbankkontext)  
- `Models/Product.cs` (und andere Tabellen als Klassen)  

---

## **4️⃣ `Program.cs` für EF und MariaDB konfigurieren**  
Öffne `Program.cs` und passe die Datenbankkonfiguration an:  
```csharp
using Microsoft.EntityFrameworkCore;
using MyApi.Models;

var builder = WebApplication.CreateBuilder(args);

builder.Services.AddControllers();
builder.Services.AddEndpointsApiExplorer();
builder.Services.AddSwaggerGen();

// Verbindung zur bestehenden MariaDB
builder.Services.AddDbContext<ApplicationDbContext>(options =>
    options.UseMySql(builder.Configuration.GetConnectionString("DefaultConnection"),
        new MySqlServerVersion(new Version(10, 5, 0))));

var app = builder.Build();

if (app.Environment.IsDevelopment())
{
    app.UseSwagger();
    app.UseSwaggerUI();
}

app.UseAuthorization();
app.MapControllers();
app.Run();
```

---

## **5️⃣ API-Controller erstellen**  
Falls du noch keinen API-Controller hast, erstelle eine Datei `Controllers/ProductController.cs`:  
```csharp
using Microsoft.AspNetCore.Mvc;
using Microsoft.EntityFrameworkCore;
using MyApi.Models;
using System.Collections.Generic;
using System.Threading.Tasks;

namespace MyApi.Controllers
{
    [Route("api/[controller]")]
    [ApiController]
    public class ProductController : ControllerBase
    {
        private readonly ApplicationDbContext _context;

        public ProductController(ApplicationDbContext context)
        {
            _context = context;
        }

        [HttpGet]
        public async Task<ActionResult<IEnumerable<Product>>> GetProducts()
        {
            return await _context.Products.ToListAsync();
        }

        [HttpGet("{id}")]
        public async Task<ActionResult<Product>> GetProduct(int id)
        {
            var product = await _context.Products.FindAsync(id);
            if (product == null) return NotFound();
            return product;
        }

        [HttpPost]
        public async Task<ActionResult<Product>> AddProduct(Product product)
        {
            _context.Products.Add(product);
            await _context.SaveChangesAsync();
            return CreatedAtAction(nameof(GetProduct), new { id = product.Id }, product);
        }

        [HttpPut("{id}")]
        public async Task<IActionResult> UpdateProduct(int id, Product updatedProduct)
        {
            if (id != updatedProduct.Id) return BadRequest();
            _context.Entry(updatedProduct).State = EntityState.Modified;
            await _context.SaveChangesAsync();
            return NoContent();
        }

        [HttpDelete("{id}")]
        public async Task<IActionResult> DeleteProduct(int id)
        {
            var product = await _context.Products.FindAsync(id);
            if (product == null) return NotFound();
            _context.Products.Remove(product);
            await _context.SaveChangesAsync();
            return NoContent();
        }
    }
}
```

---

## **6️⃣ API starten & testen**  
Starte die API mit:
```bash
dotnet run
```
Teste die API mit **Postman**, **Swagger** oder **cURL**:  
```bash
curl -X GET http://localhost:5000/api/product
```

---

## **7️⃣ Weitere Befehle für Database-First**  
Falls sich die Datenbankstruktur ändert, kannst du das Model erneut generieren:  
```bash
dotnet ef dbcontext scaffold "Server=localhost;Port=3306;Database=ProductDb;User=root;Password=root;" Pomelo.EntityFrameworkCore.MySql -o Models --context ApplicationDbContext --force
```
Oder nur die `DbContext`-Datei neu generieren:  
```bash
dotnet ef dbcontext scaffold "Server=localhost;Port=3306;Database=ProductDb;User=root;Password=root;" Pomelo.EntityFrameworkCore.MySql --context ApplicationDbContext --force --no-onconfiguring
```
Falls du **nur bestimmte Tabellen** importieren möchtest:  
```bash
dotnet ef dbcontext scaffold "Server=localhost;Port=3306;Database=ProductDb;User=root;Password=root;" Pomelo.EntityFrameworkCore.MySql -o Models --context ApplicationDbContext --table products --force
```
Falls du das Schema nicht überschreiben möchtest:  
```bash
dotnet ef dbcontext scaffold "Server=localhost;Port=3306;Database=ProductDb;User=root;Password=root;" Pomelo.EntityFrameworkCore.MySql -o Models --context ApplicationDbContext --use-database-names
```

---

## **8️⃣ Troubleshooting**
🔍 **Falls Fehler auftreten:**  
❌ `Unable to connect to database` → Prüfe die Verbindung in `appsettings.json`.  
❌ `Unknown column` → Überprüfe die generierten Spaltennamen in `Models/Product.cs`.  
❌ `Table 'ProductDb.products' doesn't exist` → Prüfe, ob die Tabelle in MariaDB vorhanden ist.  

---

## **9️⃣ Weitere Verbesserungen**
✅ **Validierung** mit `[Required]`, `[Range]`, `[MaxLength]`  
✅ **DTOs** zur Trennung von Model und API-Response  
✅ **Repository Pattern** für bessere Code-Struktur  
✅ **Swagger UI aktivieren** mit `services.AddSwaggerGen()`  
✅ **Authentifizierung** mit JWT  
✅ **Docker für ASP.NET API hinzufügen**  
