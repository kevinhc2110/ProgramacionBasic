# Patrón de diseño "singleton"

El patrón de diseño Singleton es un patrón creacional que asegura que una clase tenga solo una instancia y proporciona un punto global de acceso a dicha instancia. Este patrón es útil cuando necesitas asegurarte de que solo exista una instancia de una clase a lo largo del ciclo de vida de una aplicación, por ejemplo, para gestionar conexiones de base de datos, configuraciones de aplicación, o registros de log.

## Ejemplo Genérico de Singleton en Go

**En este ejemplo, crearemos una clase Singleton que simulará un objeto de configuración de una aplicación. Este objeto solo tendrá una instancia en todo el programa.**

```go
package main

import (
 "fmt"
 "sync"
)

// Singleton es la estructura que queremos que tenga una única instancia.
type Singleton struct {
 config string
}

var (
 instance *Singleton
 // var once sync.Once garantiza que la inicialización de la instancia se realice solo una vez, incluso en entornos concurrentes
 once     sync.Once
)

// GetInstance retorna la única instancia de Singleton.
func GetInstance() *Singleton {
  // once.Do(func() { ... }) asegura que la función anónima se ejecute solo una vez, creando la instancia de Singleton.
  once.Do(func() {
    instance = &Singleton{config: "configuración inicial"}
  })
  return instance
}

func main() {
 // Obtener la instancia del singleton
 s1 := GetInstance()
 fmt.Println(s1.config)

 // Obtener otra instancia del singleton
 s2 := GetInstance()
 fmt.Println(s2.config)

 // Modificar la configuración de s2
 s2.config = "configuración modificada"

 // Comprobar que s1 y s2 son la misma instancia
 fmt.Println(s1.config) // Debería imprimir "configuración modificada"
 fmt.Println(s2.config) // Debería imprimir "configuración modificada"

 if s1 == s2 {
  fmt.Println("s1 y s2 son la misma instancia")
 } else {
  fmt.Println("s1 y s2 son instancias diferentes")
 }
}
```

### Ventajas del Patrón Singleton

**Control sobre la instancia: Solo se crea una única instancia de la clase, evitando problemas como la duplicación de recursos.**
**Acceso global: La instancia es accesible globalmente dentro de la aplicación.**
**Facilita la gestión de recursos compartidos: Ideal para casos donde se necesita un acceso controlado a un recurso compartido, como una conexión de base de datos.**

### Consideraciones en Go

**Concurrencia: El uso de sync.Once asegura que el singleton es seguro para concurrencia, lo cual es crucial en aplicaciones concurrentes.**
**Evitación de problemas comunes: En lenguajes sin soporte nativo para Singleton, como Go, es importante manejar manualmente la creación y el acceso a la instancia para evitar múltiples instancias.**
