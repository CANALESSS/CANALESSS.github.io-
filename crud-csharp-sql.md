# CRUD en C# con SQL Server desde Cero

## 🔧 Requisitos
- Visual Studio 2022 (Community Edition)
- SQL Server Express
- Paquete NuGet: `System.Data.SqlClient`

## Paso 1: Crear la Base de Datos
```sql
CREATE DATABASE MiTienda;
USE MiTienda;
CREATE TABLE Productos (
    Id INT PRIMARY KEY IDENTITY,
    Nombre NVARCHAR(100) NOT NULL,
    Precio DECIMAL(10,2) NOT NULL
);
```
// Cadena de conexión - Cambia "localhost" si usas un servidor remoto
## Paso 2: Conexión en C#
```csharp
using System.Data.SqlClient;

string connectionString = "Server=localhost;Database=MiTienda;Trusted_Connection=True;";
SqlConnection conexion = new SqlConnection(connectionString);
try {
    conexion.Open();
    Console.WriteLine("¡Conexión exitosa!");
} catch (Exception ex) {
    Console.WriteLine("Error: " + ex.Message);
}
```


## Paso 3: Insertar Datos
```csharp
string query = "INSERT INTO Productos (Nombre, Precio) VALUES (@Nombre, @Precio)";
SqlCommand cmd = new SqlCommand(query, conexion);
cmd.Parameters.AddWithValue("@Nombre", "Teclado");
cmd.Parameters.AddWithValue("@Precio", 29.99);
cmd.ExecuteNonQuery();
