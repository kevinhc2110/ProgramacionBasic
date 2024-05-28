# Callbacks en Go: Definir comportamiento dinámico

Los callbacks son un concepto fundamental en la programación funcional que permiten pasar una función como argumento a otra función. Esto te permite crear código más flexible y reutilizable al definir el comportamiento de una función en tiempo de ejecución.

## Implementación en Go

Si bien Go no tiene una sintaxis integrada para callbacks como otros lenguajes, puedes lograr una funcionalidad similar usando funciones anónimas y valores de función. Así es como funciona:

### Ejemplo de uso de callbacks

```go
package main

import "fmt"

type Callback func(int) int

// La función procesarNumeros toma una lista de números y una función de callback,
// y aplica la función de callback a cada número de la lista.

func procesarNumeros(numeros []int, callback Callback) {
 for _, num := range numeros {
  resultado := callback(num)
  fmt.Println("Resultado:", resultado)
 }
}

// Función de ejemplo que duplica un número.

func duplicar(numero int) int {
 return numero * 2
}

// Función de ejemplo que suma 10 a un número.

func sumar10(numero int) int {
 return numero + 10
}

func main() {

 // Creamos una lista de números.

 numeros := []int{1, 2, 3, 4, 5}

 fmt.Println("Aplicando la función duplicar:")

 // Llamamos a procesarNumeros con la función duplicar como callback.

 procesarNumeros(numeros, duplicar)

 fmt.Println("\nAplicando la función sumar10:")

 // Llamamos a procesarNumeros con la función sumar10 como callback.

 procesarNumeros(numeros, sumar10)
}
```
