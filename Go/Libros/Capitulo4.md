# Capítulo 4: Organización del Código e Interfaces

## Paquetes en Go

- Unidades de organización de código
- Estructura jerárquica en el workspace

### Ejemplo de uso de paquetes

```go
// Contenido del archivo db.go dentro de shopping/db:
package db

type Item struct {
    Price float64
}

func LoadItem(id int) *Item {
    return &Item{
        Price: 9.001,
    }
}

// Contenido del archivo pricecheck.go dentro de shopping:
package shopping

import "shopping/db"

func PriceCheck(itemId int) (float64, bool) {
    item := db.LoadItem(itemId)
    if item == nil {
        return 0, false
    }
    return item.Price, true
}

// Contenido del archivo main.go dentro de shopping/main:
package main

import (
    "fmt"
    "shopping"
)

func main() {
    fmt.Println(shopping.PriceCheck(4343))
}
```

## Importaciones cíclicas en Go

Problemas de compilación por importaciones mutuas

## Visibilidad

**Identificadores con mayúscula: públicos**
**Identificadores con minúscula: privados**

```go
// Ejemplo de función con visibilidad:
func NewItem() *Item {
    // ...
}
```

## Gestión de Paquetes

**Comando go get para obtener una dependencia de terceros**

```go
go get github.com/mattn/go-sqlite3
```

```go
import (
"github.com/mattn/go-sqlite3"
)
```

## Gestión de Dependencias

### go get
- Escanea ficheros por imports de librerías de terceros
- Descarga librerías automáticamente
- Funciona como:
  - Gemfile
  - package.json
  - pom.xml
  - build.gradle

### Actualización de Paquetes
- `go get -u`
  - Actualiza todos los paquetes
  - Ejemplo para un paquete específico:
    ```bash
    go get -u NOMBRE_COMPLETO_DEL_PAQUETE
    ```

### Herramientas de Terceros
- goop
- godep
- Lista completa en la go-wiki


## Interfaces

```go
// Ejemplo de definición de interfaz Logger
type Logger interface {
    Log(message string)
}
```

**Uso de Interfaces:**

Pueden ser campos de estructuras o parámetros de funciones

```go
// Ejemplo de estructura con un campo de tipo Logger
type Server struct {
    logger Logger
}

// Ejemplo de función que toma un parámetro de tipo Logger
func process(logger Logger) {
    logger.Log("hello!")
}
```

**Implementación de Interfaces:**

Una estructura implementa una interfaz si tiene una función con la firma requerida

```go
// Implementación de la interfaz Logger mediante una estructura ConsoleLogger
type ConsoleLogger struct {}

func (l ConsoleLogger) Log(message string) {
    fmt.Println(message)
}
```

### Ventajas de las Interfaces

_Facilitan la creación de código desacoplado._
_Permite tener interfaces pequeñas y enfocadas en tareas específicas._
_La librería estándar de Go está llena de interfaces que facilitan la interoperabilidad entre paquetes._
