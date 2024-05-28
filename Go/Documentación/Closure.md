# Closures en Go: Funciones encapsulando variables de su entorno

En Go, un closure (o cierre) es una función que "captura" las variables de su entorno. Es decir, una función puede referenciar variables fuera de su cuerpo y esas variables permanecen accesibles cuando la función es invocada más tarde, incluso si ya ha salido del ámbito en el que fue definida.

Los closures son útiles porque permiten la creación de funciones que mantienen estado entre llamadas sucesivas sin necesidad de utilizar variables globales. Esta técnica es común en la programación funcional y se encuentra en muchos lenguajes modernos, incluyendo Go.

## Características de los closures en Go

**Encapsulación:** Los closures encapsulan una función junto con las variables de su entorno, creando una unidad autocontenida.
**Acceso a variables externas:** Las funciones dentro de closures pueden acceder y modificar variables de su entorno externo, incluso después de que el entorno haya finalizado.
**Preservación de estado:** Los closures preservan el estado de las variables encapsuladas, lo que permite crear funciones con memoria interna persistente.
**Creación de funciones personalizadas:** Los closures permiten crear funciones personalizadas que se adaptan al contexto en el que se definen.

### Ejemplo de uso de closure

```go
package main

import "fmt"

func  main() {

 // Definimos una función llamada "incrementador" que retorna otra función.

 incrementador := func() func() int {
  x := 0
  return func() int {
   x++
   return x
  }
 }

 // Creamos una instancia de la función incrementador.

 incremento := incrementador()

 // Llamamos al closure varias veces para ver cómo cambia el valor de "x".

 fmt.Println(incremento()) // Output: 1
 fmt.Println(incremento()) // Output: 2
 fmt.Println(incremento()) // Output: 3
}
```
