# Recursividad en Go: Dominando la repetición a través de la auto-referencia

La recursividad en Go es una técnica de programación que permite resolver problemas complejos dividiéndolos en subproblemas más pequeños y similares al problema original. Se basa en la idea de que una función se llama a sí misma para procesar cada subproblema. Si bien puede parecer un concepto complejo, la recursividad puede ser una herramienta poderosa para escribir código elegante y eficiente en Go.

## Concepto básico

## Una función recursiva se caracteriza por dos elementos clave

**Caso base:** Es la condición que detiene la recursión y proporciona una solución simple al problema.
**Paso recursivo:** Es la parte de la función que se llama a sí misma con un subproblema más pequeño, acercándose al caso base.

## Evitar

**Riesgo de Desbordamiento de Pila:**

Go no optimiza las llamadas de tail-recursion, por lo que las llamadas recursivas profundas pueden causar desbordamiento de pila. Si el número de llamadas recursivas puede ser grande, es mejor usar una versión iterativa.

**Problemas de Eficiencia:**

Las llamadas recursivas pueden ser menos eficientes que las iterativas debido al sobrecosto de mantener el contexto de cada llamada en la pila.

### Ejemplo de usos de recursividad

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

## Cuándo Usar Recursividad

**Estructuras de Datos Recursivas:**

_Árboles:_ El recorrido de árboles (preorden, en orden, postorden) se maneja de manera natural con recursión.
_Listas Enlazadas:_ Operaciones como la reversión o la búsqueda en listas enlazadas pueden ser implementadas recursivamente.

**Problemas que se Dividen Naturalmente en Subproblemas:**

_Divide y Vencerás:_ Algoritmos como la búsqueda binaria, quicksort y mergesort se prestan bien a implementaciones recursivas.

### Ejemplos avanzado de recursividad

```go
func quicksort(arr []int) {
    // Caso base: si el array tiene menos de 2 elementos, ya está ordenado
    if len(arr) < 2 {
        return
    }

    // Elegimos el primer elemento como pivote
    pivot := arr[0]

    // Declaramos dos slices: uno para los elementos menores o iguales al pivote y otro para los mayores
    left := []int{}
    right := []int{}

    // Iteramos sobre los elementos restantes del array (a partir del segundo elemento)
    for _, v := range arr[1:] {
        // Si el elemento es menor o igual al pivote, lo agregamos al slice 'left'
        if v <= pivot {
            left = append(left, v)
        } else {
            // Si el elemento es mayor al pivote, lo agregamos al slice 'right'
            right = append(right, v)
        }
    }

    // Llamada recursiva a quicksort para ordenar el slice 'left'
    quicksort(left)

    // Llamada recursiva a quicksort para ordenar el slice 'right'
    quicksort(right)

    // Copiamos los elementos ordenados de 'left', el pivote y 'right' de vuelta al array original
    copy(arr, append(append(left, pivot), right...))
}
```

```go
type TreeNode struct {
    Val   int
    Left  *TreeNode
    Right *TreeNode
}

func traverse(root *TreeNode) {
    if root == nil {
        return
    }
    fmt.Println(root.Val)
    traverse(root.Left)
    traverse(root.Right)
}
```
