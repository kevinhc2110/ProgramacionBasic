# Interfaces en Go

Las interfaces en Go son un mecanismo poderoso para definir contratos de comportamiento que pueden ser implementados por diferentes tipos de datos. Permiten escribir código más flexible, modular y reutilizable.

## Ejemplo de uso de interfaces

```go
package main

import (
 "fmt"
)

// Definición de una interfaz
type Saludador interface {
    Saludar()
}

// Definición de un struct Persona
type Persona2 struct {
    Nombre string
}

// Implementación del método Saludar para Persona
func (p2 Persona2) Saludar() {
    fmt.Printf("Hola, mi nombre es %s.\n", p2.Nombre)
}

func main() {
    // Creación de una instancia de Persona
    p2 := Persona2{
        Nombre: "Juan",
    }

    var s Saludador = p2
    s.Saludar()
}
```

## Beneficios de las interfaces

**Flexibilidad:** Las interfaces permiten escribir código que puede trabajar con diferentes tipos de datos sin necesidad de duplicar la lógica.
**Modularidad:** Las interfaces promueven la separación de preocupaciones al definir el comportamiento esperado sin preocuparse de la implementación específica.
**Reutilización:** Las funciones que operan con interfaces pueden ser reutilizadas con diferentes tipos de datos.
**Pruebas unitarias:** Las interfaces facilitan la creación de pruebas unitarias para código que depende del comportamiento y no de la implementación específica de un tipo.
