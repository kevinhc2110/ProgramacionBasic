# Recursividad en Go: Dominando la repetición a través de la auto-referencia

La recursividad en Go es una técnica de programación que permite resolver problemas complejos dividiéndolos en subproblemas más pequeños y similares al problema original. Se basa en la idea de que una función se llama a sí misma para procesar cada subproblema. Si bien puede parecer un concepto complejo, la recursividad puede ser una herramienta poderosa para escribir código elegante y eficiente en Go.

## Concepto básico

### Una función recursiva se caracteriza por dos elementos clave

**Caso base:** Es la condición que detiene la recursión y proporciona una solución simple al problema.
**Paso recursivo:** Es la parte de la función que se llama a sí misma con un subproblema más pequeño, acercándose al caso base.

## Ejemplo de usos de recrusividad

```go
package main

import "fmt"

func recursividad() /*main*/ {

  // Iniciar la recursion con el número 100

  imprimirNumeros(100)

}

// Función recursiva para imprimir números del 100 al 0

func imprimirNumeros(n int) {

 //Cuando una función es recursiva, se repite a sí misma con un valor diferente de su parámetro hasta alcanzar una condición de parada (caso base).
 // Condición de parada: si n es menor que 0, termina la recursion

 if n < 0 {
   return
 }

 // Imprimir el número actual

 fmt.Println(n)

 // Llamada recursiva con el siguiente número menor

 imprimirNumeros(n - 1)

}
```
