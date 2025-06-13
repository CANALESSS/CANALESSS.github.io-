# CRUD en C# con SQL Server (Guía Teórica)

> 🔍 **Nota para el lector**:  
> Este tutorial sigue los estándares oficiales de Microsoft. Para ejecutarlo, necesitarás Visual Studio y SQL Server.  
> [Ver instrucciones de instalación](#-requisitos).

## Requisitos
- **Software**:
  - Visual Studio 2022 ([Descargar Community Edition](https://visualstudio.microsoft.com/es/vs/community/))
  - SQL Server Express ([Descargar](https://www.microsoft.com/es-es/sql-server/sql-server-downloads))
- **Paquete NuGet**: `System.Data.SqlClient`

## Estructura de la Base de Datos
```sql
CREATE DATABASE MiTienda;
USE MiTienda;
CREATE TABLE Productos (
    Id INT PRIMARY KEY IDENTITY,
    Nombre NVARCHAR(100) NOT NULL,
    Precio DECIMAL(10,2) NOT NULL
);
```

## Conexión Básica
```csharp
using System.Data.SqlClient;

string connectionString = "Server=localhost;Database=MiTienda;Trusted_Connection=True;";
using SqlConnection conexion = new SqlConnection(connectionString);

try {
    conexion.Open();
    Console.WriteLine("¡Conexión exitosa!");
} catch (Exception ex) {
    Console.WriteLine($"Error: {ex.Message}");
}
```

## Operaciones CRUD (Teóricas)

### INSERT
```csharp
// Ejemplo teórico - Ajusta valores según necesites
string insertQuery = "INSERT INTO Productos (Nombre, Precio) VALUES (@Nombre, @Precio)";
using SqlCommand cmdInsert = new SqlCommand(insertQuery, conexion);
cmdInsert.Parameters.AddWithValue("@Nombre", "Monitor");
cmdInsert.Parameters.AddWithValue("@Precio", 129.99);
cmdInsert.ExecuteNonQuery();
```

### SELECT
```csharp
string selectQuery = "SELECT * FROM Productos";
using SqlCommand cmdSelect = new SqlCommand(selectQuery, conexion);
using SqlDataReader reader = cmdSelect.ExecuteReader();

while (reader.Read()) {
    Console.WriteLine($"ID: {reader["Id"]}, Nombre: {reader["Nombre"]}, Precio: {reader["Precio"]}");
}
```

## 🚨 Posibles Errores y Soluciones
| Error | Causa Probable | Solución |
|-------|---------------|----------|
| `Login failed for user` | Autenticación incorrecta | Usa `Trusted_Connection=True` o credenciales válidas |
| `Cannot open database` | La BD no existe | Ejecuta primero el script SQL de creación |

## 📚 Recursos Adicionales
- [Documentación oficial de SqlConnection](https://learn.microsoft.com/es-es/dotnet/api/system.data.sqlclient.sqlconnection)
- [Ejemplos de CRUD en .NET](https://dotnettutorials.net)
