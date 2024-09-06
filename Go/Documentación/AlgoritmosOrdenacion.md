# Ordenación en Go

Golang ofrece varias formas de ordenar slices de diferentes tipos de datos. Aquí te presento las más comunes:

**Ordenación con el paquete sort:**

El paquete sort proporciona funciones para ordenar slices de tipos de datos integrados como enteros, strings, floats, etc.

_sort.Ints(slice):_ Ordena un slice de enteros en orden ascendente.
_sort.Strings(slice):_ Ordena un slice de strings en orden lexicográfico (alfabético).
_sort.Floats(slice):_ Ordena un slice de floats en orden ascendente.

```go
package main

import (
  "fmt"
  "sort"
)

func main() {
  numeros := []int{50, 10, 30, 20, 40}

  fmt.Println("Slice original:", numeros)

  sort.Ints(numeros) // Ordena en forma ascendente

  fmt.Println("Slice ordenado:", numeros)
}
```

**Ordenación personalizada:**

Para ordenar slices con tipos de datos personalizados o con criterios específicos, puedes definir una función Less y utilizar la función sort.Slice.

```go
package main

import (
  "fmt"
  "sort"
)

type Persona struct {
  Nombre string
  Edad   int
}

func (p Persona) Less(other Persona) bool {
  return p.Edad < other.Edad // Ordena por edad ascendente
}

func main() {
  personas := []Persona{
    {"Juan", 30},
    {"Maria", 25},
    {"Pedro", 40},
  }

  fmt.Println("Slice original:", personas)

  sort.Slice(personas, func(i, j int) bool {
    return personas[i].Nombre < personas[j].Nombre // Ordena por nombre ascendente
  })

  fmt.Println("Slice ordenado:", personas)
}
```

**Ordenación inversa:**

Para ordenar en forma inversa, utiliza la función sort.Reverse.

```go
package main

import (
  "fmt"
  "sort"
)

func main() {
  numeros := []int{50, 10, 30, 20, 40}

  fmt.Println("Slice original:", numeros)

  sort.Ints(numeros)   // Ordena en forma ascendente
  sort.Reverse(numeros) // Invierte el orden

  fmt.Println("Slice ordenado inversamente:", numeros)
}
```

**Bubble Sort(No es el mejor):**

El algoritmo Bubble Sort es un algoritmo de intercambio simple que compara elementos adyacentes y los intercambia si están en el orden incorrecto.

```go
package main

import (
    "fmt"
)

// Función `bubbleSort` que ordena un slice de enteros usando el algoritmo Bubble Sort.
func bubbleSort(slice []int) {
    // Se recorre el slice hasta que no se realicen más intercambios.
    for i := 0; i < len(slice)-1; i++ {
        // Se recorre el slice desde el inicio hasta el final, excluyendo el elemento ya ordenado en la última iteración.
        for j := 0; j < len(slice)-i-1; j++ {
            // Si el elemento actual es mayor que el siguiente, se intercambian.
            if slice[j] > slice[j+1] {
                slice[j], slice[j+1] = slice[j+1], slice[j]
            }
        }
    }
}

func main() {
    // Slice de enteros sin ordenar.
    slice := []int{5, 2, 4, 1, 3}
    fmt.Println("Slice sin ordenar:", slice)

    // Se ordena el slice usando Bubble Sort.
    bubbleSort(slice)

    // Se imprime el slice ordenado.
    fmt.Println("Slice ordenado con Bubble Sort:", slice)
}
```

**Quick Sort:**

El algoritmo Quick Sort utiliza un enfoque de división y conquista para ordenar slices de manera eficiente.

```go
package main

import (
    "fmt"
    "math/rand"
)

// Función `quickSort` que ordena un slice de enteros usando el algoritmo Quick Sort.
func quickSort(slice []int, left int, right int) {
    // Si el sub-slice no está vacío (left < right)
    if left < right {
        // Se selecciona un pivote aleatorio del sub-slice.
        pivot := partition(slice, left, right)

        // Se ordenan recursivamente los sub-slices a la izquierda y derecha del pivote.
        quickSort(slice, left, pivot-1)
        quickSort(slice, pivot+1, right)
    }
}

// Función `partition` que reordena el slice alrededor de un pivote.
func partition(slice []int, left int, right int) int {
    // Se selecciona el valor del elemento del extremo derecho como pivote.
    pivot := slice[right]
    i := left - 1 // Índice del último elemento menor que el pivote.

    // Se recorre el slice desde el inicio hasta el elemento anterior al pivote.
    for j := left; j < right; j++ {
        // Si el elemento actual es menor o igual que el pivote, se intercambia con el elemento en la posición `i + 1`.
        if slice[j] <= pivot {
            i++
            slice[i], slice[j] = slice[j], slice[i]
        }
    }

    // Se intercambia el pivote con el elemento en la posición `i + 1`.
    i++
    slice[i], slice[right] = slice[right], slice[i]

    // Se retorna la posición final del pivote.
    return i
}

func main() {
    // Slice de enteros sin ordenar.
    slice := []int{5, 2, 4, 1, 3}
    fmt.Println("Slice sin ordenar:", slice)

    // Se ordena el slice usando Quick Sort.
    quickSort(slice, 0, len(slice)-1)

    // Se imprime el slice ordenado.
    fmt.Println("Slice ordenado con Quick Sort:", slice)
}
```

**Merge Sort:**

El algoritmo Merge Sort es un algoritmo de división y conquista que divide recursivamente el slice en sub-slices, los ordena individualmente y luego los fusiona en un orden general.

```go
package main

import (
    "fmt"
)

// Función `mergeSort` que ordena un slice de enteros usando el algoritmo Merge Sort.
func mergeSort(slice []int) []int {
    // Si el slice tiene un solo elemento o menos, ya está ordenado.
    if len(slice) <= 1 {
        return slice
    }

    // Se divide el slice en dos sub-slices iguales.
    middle := len(slice) / 2
    left := mergeSort(slice[:middle])
    right := mergeSort(slice[middle:])

    // Se fusionan los sub-slices ordenados en un solo slice ordenado.
    return merge(left, right)
}

// Función `merge` que fusiona dos slices de enteros ordenados en un solo slice ordenado.
func merge(left, right []int) []int {
    result := []int{}
    i := 0
    j := 0

    // Se recorren ambos slices simultáneamente.
    for i < len(left) && j < len(right) {
        // Si el elemento del slice izquierdo es menor o igual al del slice derecho, se agrega al slice resultante.
        if left[i] <= right[j] {
            result = append(result, left[i])
            i++
        } else {
            // Si el elemento del slice derecho es menor, se agrega al slice resultante.
            result = append(result, right[j])
            j++
        }
    }

    // Se agregan los elementos restantes del slice que no se han recorrido.
    result = append(result, left[i:]...)
    result = append(result, right[j:]...)

    // Se retorna el slice fusionado y ordenado.
    return result
}

func main() {
    // Slice de enteros sin ordenar.
    slice := []int{5, 2, 4, 1, 3}
    fmt.Println("Slice sin ordenar:", slice)

    // Se ordena el slice usando Merge Sort.
    sortedSlice := mergeSort(slice)

    // Se imprime el slice ordenado.
    fmt.Println("Slice ordenado con Merge Sort:", sortedSlice)
}
```
