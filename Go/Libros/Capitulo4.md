# Capítulo 4: Organización del Código e Interfaces

## Paquetes en Go

Los paquetes en Go son unidades de organización que agrupan código relacionado. Su estructura sigue la jerarquía de directorios en el workspace de Go. Al importar un paquete, se debe especificar la ruta completa desde la raíz del workspace.

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

Las importaciones cíclicas en Go se producen cuando dos o más paquetes se importan mutuamente. Esto puede generar problemas de compilación, ya que el compilador no puede determinar el orden en que se deben cargar los paquetes.

## Visibilidad

En Go, la visibilidad de los identificadores está determinada por si su nombre comienza con mayúscula o minúscula. Los identificadores que comienzan con mayúscula son visibles fuera del paquete, mientras que los que comienzan con minúscula son privados dentro del paquete.

```go
// Ejemplo de función con visibilidad:
func NewItem() *Item {
    // ...
}
```

## Gestión de Paquetes

go get se utiliza para obtener dependencias de terceros en Go. También hay herramientas adicionales como goop y godep para gestionar dependencias de forma más avanzada.

**Comando go get para obtener una dependencia de Github:**

```go
go get github.com/mattn/go-sqlite3
```

```go
import (
"github.com/mattn/go-sqlite3"
)
```

## Gestión de Dependencias

go get guarda un par de ases bajo la manga. Si usamos go get en un proyecto se escanearán todos los ficheros buscando imports con librerías de terceros y las descargará. En cierta medida, nuestro propio código fuente se convierte en un Gemfile, un package.json, un pom.xml o un build.gradle.
Si utilizas go get -u actualizarás todos los paquetes (también puedes actualizar un paquete específico usando go get -u NOMBRE_COMPLETO_DEL_PAQUETE)
Puedes usar una herramienta de gestión de dependencias de terceros. Todavía son jóvenes pero las dos más prometedoras son goop y godep. Hay una lista más completa en la go-wiki.

```go
go get
```

## Interfaces

Los interfaces en Go son tipos que especifican un contrato sin contener implementación. Permiten desacoplar el código de implementaciones específicas.

```go
// Ejemplo de definición de interfaz Logger
type Logger interface {
    Log(message string)
}
```

**Uso de Interfaces:**

Los interfaces se utilizan de la misma manera que cualquier otro tipo en Go. Pueden ser campos de una estructura o parámetros de funciones.

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

Una estructura puede implementar una interfaz si tiene una función con la firma requerida por la interfaz.

```g
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
