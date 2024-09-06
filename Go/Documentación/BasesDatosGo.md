# Bases de Datos en Go

## Conexión a Bases de Datos

Go ofrece una forma estándar de conectarse a diversas bases de datos a través del paquete database/sql. Este paquete proporciona una interfaz abstracta que permite interactuar con diferentes sistemas de gestión de bases de datos (SGBD) utilizando controladores específicos.

```go
package main

import (
        "database/sql"
        _ "github.com/go-sql-driver/mysql" // Importa el driver MySQL
        "fmt"
)

func main() {
        db, err := sql.Open("mysql", "usuario:contraseña@/basededatos")
        if err != nil {
                panic(err)
        }
        defer db.Close()

        // Realizar consultas SQL
        rows, err := db.Query("SELECT * FROM usuarios")
        if err != nil {
                panic(err)
        }
        defer rows.Close()

        // Iterar sobre los resultados
        for rows.Next() {
                var id int
                var nombre string
                if err := rows.Scan(&id, &nombre); err != nil {
                        panic(err)
                }
                fmt.Println(id, nombre)
        }
}
```

## Conexión a una base de datos NoSQL

La conexión a bases de datos NoSQL varía según el tipo de base de datos (MongoDB, Cassandra, etc.). Generalmente, se utiliza el driver específico proporcionado por la base de datos.

## Consultas SQL

Go permite ejecutar consultas SQL directamente utilizando el método Query del objeto db. Las consultas más comunes son:

_SELECT:_ Para seleccionar datos de una o más tablas.
_INSERT:_ Para insertar nuevos registros en una tabla.
_UPDATE:_ Para modificar registros existentes.
_DELETE:_ Para eliminar registros.
_JOIN:_ Para combinar filas de dos o más tablas.

```go
rows, err := db.Query("SELECT usuarios.nombre, pedidos.fecha FROM usuarios INNER JOIN pedidos ON usuarios.id = pedidos.usuario_id")
```

## ORM (Object-Relational Mapping)

Un ORM facilita la interacción entre objetos en Go y las tablas de una base de datos relacional. Mapea las estructuras de datos de Go a las tablas de la base de datos y viceversa.

```go
type User struct {
        gorm.Model
        Name  string
        Email string
}

func main() {
        db, err := gorm.Open("mysql", "usuario:contraseña@/basededatos")
        if err != nil {
                panic("failed to connect database")
        }

        // Crear una tabla de usuarios
        db.AutoMigrate(&User{})

        // Crear un nuevo usuario
        user := User{Name: "John Doe", Email: "johndoe@example.com"}
        db.Create(&user)
}
```

**Relacionales:** Aplicaciones empresariales, sistemas transaccionales, análisis de datos estructurados.
**NoSQL:** Big data, aplicaciones web a gran escala, almacenamiento de documentos, análisis de datos no estructurados.
