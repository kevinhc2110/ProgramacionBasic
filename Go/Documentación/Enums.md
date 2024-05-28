# Enumeraciones en Go: Equivalentes y Alternativas

En Go, no existe un tipo de datos enum como en otros lenguajes de programación como C, C++ o Java. Sin embargo, es posible simular enumeraciones utilizando constantes (const) y tipos personalizados. Esta técnica permite crear un conjunto de valores relacionados, lo que proporciona una funcionalidad similar a los enums.

## Creación de Enums en Go

**Definir un Tipo Personalizado:** Se define un tipo personalizado usando type.
**Usar iota:** Se utiliza iota para crear constantes secuenciales.

### Ejemplo de uso de "enums"

```go
package main

import "fmt"

type DiaSemana int

// Definir constantes para los días de la semana

const (

 // Empezamos desde 1 utilizando iota, que es una constante predeclarada que genera valores secuenciales.

 Lunes DiaSemana = iota + 1
 Martes
 Miercoles
 Jueves
 Viernes
 Sabado
 Domingo
)

// Función para obtener el nombre del día de la semana

func NombreDia(dia DiaSemana) string {
 switch dia {
 case Lunes:
  return "Lunes"
 case Martes:
  return "Martes"
 case Miercoles:
  return "Miércoles"
 case Jueves:
  return "Jueves"
 case Viernes:
  return "Viernes"
 case Sabado:
  return "Sábado"
 case Domingo:
  return "Domingo"
 default:
  return "Día no válido"
 }
}

func main(){
 // Ejemplo de uso de la función dayToString para el número 1
 dia := 1
 fmt.Printf("Día %d: %s\n", dia, NombreDia(DiaSemana(dia)))

 for i := 1; i <= 7; i++ {
  fmt.Printf("Día %d: %s\n", i, NombreDia(DiaSemana(i)))
 }
}
```
