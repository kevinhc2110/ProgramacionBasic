# Funciones en Go: Bloques de construcción reutilizables

En Go, las funciones son bloques de código independientes que realizan tareas específicas y son reutilizables en todo su programa. Permiten modularizar su código, mejorar la legibilidad y promover la organización.

## Función Básica

```go
package main

import "fmt"

// Definición de una función básica
func saludo() {
    fmt.Println("Hola, Mundo!")
}

func main() {
    // Llamada a la función
    saludo()
}
```

## Funciones con Parámetros

```go
package main

import "fmt"

// Función con parámetros
func saludar(nombre string) {
    fmt.Printf("Hola, %s!\n", nombre)
}

func main() {
    // Llamada a la función con un argumento
    saludar("Carlos")
}
```

## Funciones con Resultados

```go
package main

import "fmt"

// Función que devuelve un resultado
func sumar(a int, b int) int {
    return a + b
}

func main() {
    // Llamada a la función y almacenamiento del resultado
    resultado := sumar(3, 4)
    fmt.Println("La suma es:", resultado)
}
```

## Funciones con Múltiples Resultados

```go
package main

import "fmt"

// Función que devuelve múltiples resultados
func dividir(a int, b int) (int, int) {
    cociente := a / b
    residuo := a % b
    return cociente, residuo
}

func main() {
    // Llamada a la función y almacenamiento de múltiples resultados
    cociente, residuo := dividir(10, 3)
    fmt.Printf("Cociente: %d, Residuo: %d\n", cociente, residuo)
}
```

## Funciones Anónimas

Las funciones pueden ser definidas sin un nombre y se conocen como funciones anónimas. Pueden ser usadas como valores y asignadas a variables:

```go
package main

import "fmt"

func main() {
    // Definición de una función anónima y asignación a una variable
    multiplicar := func(a int, b int) int {
        return a * b
    }

    // Uso de la función anónima
    resultado := multiplicar(3, 4)
    fmt.Println("El producto es:", resultado)
}
```

## Funciones como Parámetros

Las funciones pueden ser pasadas como parámetros a otras funciones:

```go
package main

import "fmt"

// Definición de una función que toma otra función como parámetro
func aplicarOperacion(a int, b int, operacion func(int, int) int) int {
    return operacion(a, b)
}

func main() {
    // Definición de una función anónima para la suma
    suma := func(a int, b int) int {
        return a + b
    }

    // Uso de la función aplicarOperacion con la función suma
    resultado := aplicarOperacion(5, 3, suma)
    fmt.Println("El resultado de la operación es:", resultado)
}
```

## Funciones con Defer

El uso de defer en funciones permite ejecutar una instrucción justo antes de que la función actual retorne:

```go
package main

import "fmt"

func main() {
    defer fmt.Println("Esto se ejecuta al final de la función main")

    fmt.Println("Esto se ejecuta primero")
}
```

En este ejemplo, la instrucción defer asegura que fmt.Println("Esto se ejecuta al final de la función main") se ejecute al final, justo antes de que main termine, sin importar dónde ocurra el return en la función main.
