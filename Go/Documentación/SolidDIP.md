# Principio SOLID de Inversión de Dependencias (Dependency Inversion Principle, DIP)

Es uno de los cinco principios SOLID de diseño de software. Este principio establece que:

_Los módulos de alto nivel no deberían depender de módulos de bajo nivel. Ambos deberían depender de abstracciones._
_Las abstracciones no deberían depender de detalles. Los detalles deberían depender de abstracciones._

## Ejemplo Incorrecto

En el ejemplo incorrecto, un módulo de alto nivel depende directamente de un módulo de bajo nivel.

```go
package main

import "fmt"

// Modulo de bajo nivel
type MySQLDatabase struct{}

func (db *MySQLDatabase) Connect() {
    fmt.Println("Connecting to MySQL Database")
}

// Modulo de alto nivel
type UserService struct {
    db *MySQLDatabase
}

func NewUserService() *UserService {
    return &UserService{
        db: &MySQLDatabase{},
    }
}

func (us *UserService) GetUser() {
    us.db.Connect()
    fmt.Println("Getting user from database")
}

func main() {
    userService := NewUserService()
    userService.GetUser()
}
```

En este ejemplo, UserService (módulo de alto nivel) depende directamente de MySQLDatabase (módulo de bajo nivel). Si quisiéramos cambiar la base de datos, tendríamos que modificar el UserService.

## Ejemplo Correcto

En el ejemplo correcto, usamos una abstracción (una interfaz) para que el módulo de alto nivel dependa de esta, en lugar de depender directamente de un módulo de bajo nivel.

```go
package main

import "fmt"

// Abstracción
type Database interface {
    Connect()
}

// Modulo de bajo nivel
type MySQLDatabase struct{}

func (db *MySQLDatabase) Connect() {
    fmt.Println("Connecting to MySQL Database")
}

// Otro modulo de bajo nivel
type PostgreSQLDatabase struct{}

func (db *PostgreSQLDatabase) Connect() {
    fmt.Println("Connecting to PostgreSQL Database")
}

// Modulo de alto nivel
type UserService struct {
    db Database
}

func NewUserService(db Database) *UserService {
    return &UserService{
        db: db,
    }
}

func (us *UserService) GetUser() {
    us.db.Connect()
    fmt.Println("Getting user from database")
}

func main() {
    // Podemos usar cualquier implementación de la interfaz Database
    mySQLDB := &MySQLDatabase{}
    userService := NewUserService(mySQLDB)
    userService.GetUser()

    fmt.Println()

    postgreSQLDB := &PostgreSQLDatabase{}
    userService = NewUserService(postgreSQLDB)
    userService.GetUser()
}
```

En este ejemplo, UserService depende de la interfaz Database, no de una implementación específica. Esto permite cambiar la implementación de la base de datos sin modificar el UserService.
