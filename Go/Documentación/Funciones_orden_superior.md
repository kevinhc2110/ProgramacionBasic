# Funciones de orden superior en Go

Las funciones de orden superior son aquellas funciones que pueden recibir otras funciones como argumentos y/o devolver funciones como resultado. Este concepto es muy poderoso y se utiliza comúnmente en lenguajes de programación funcional y en muchos otros lenguajes modernos, incluido Go.

## Ejemplo 1: Función que recibe otra función como argumento

En este ejemplo, vamos a crear una función aplicaFuncion que toma una función y un entero como argumentos, y aplica la función al entero.

```go
package main

import (
 "fmt"
)

// Definimos una función de orden superior que toma una función y un entero como argumentos
func aplicaFuncion(f func(int) int, x int) int {
 return f(x)
}

// Una función simple que vamos a pasar como argumento
func cuadrado(x int) int {
 return x * x
}

// Otra función simple que vamos a pasar como argumento
func doble(x int) int {
 return x * 2
}

func main() {
 // Aplicamos la función cuadrado al número 5 usando aplicaFuncion
 resultado := aplicaFuncion(cuadrado, 5)
 fmt.Printf("El cuadrado de 5 es: %d\n", resultado)

 // Aplicamos la función doble al número 5 usando aplicaFuncion
 resultado = aplicaFuncion(doble, 5)
 fmt.Printf("El doble de 5 es: %d\n", resultado)
}
```

## Ejemplo 2: Función que devuelve otra función

En este ejemplo, vamos a crear una función crearMultiplicador que toma un entero y devuelve una función que multiplica su argumento por ese entero.

```go
package main

import (
 "fmt"
)

// Definimos una función de orden superior que devuelve una función
func crearMultiplicador(factor int) func(int) int {
 return func(x int) int {
  return x * factor
 }
}

func main() {
 // Creamos una función que multiplica por 3
 multiplicaPorTres := crearMultiplicador(3)

 // Usamos la nueva función para multiplicar números
 fmt.Printf("3 * 4 = %d\n", multiplicaPorTres(4))
 fmt.Printf("3 * 7 = %d\n", multiplicaPorTres(7))

 // Creamos otra función que multiplica por 5
 multiplicaPorCinco := crearMultiplicador(5)

 // Usamos la nueva función para multiplicar números
 fmt.Printf("5 * 4 = %d\n", multiplicaPorCinco(4))
 fmt.Printf("5 * 7 = %d\n", multiplicaPorCinco(7))
}
```

## Ejemplo 3: Función que recibe y devuelve otra función

En este ejemplo, vamos a crear una función componeFunciones que toma dos funciones y devuelve una nueva función que es la composición de las dos funciones originales.

```go
package main

import (
 "fmt"
)

// Definimos una función de orden superior que toma dos funciones y devuelve una nueva función
func componeFunciones(f, g func(int) int) func(int) int {
 return func(x int) int {
  return f(g(x))
 }
}

// Funciones simples para usar en la composición
func sumaDos(x int) int {
 return x + 2
}

func multiplicaPorTres(x int) int {
 return x * 3
}

func main() {
 // Componemos las funciones sumaDos y multiplicaPorTres
 // La nueva función primero multiplica por 3 y luego suma 2
 nuevaFuncion := componeFunciones(sumaDos, multiplicaPorTres)

 // Usamos la nueva función para calcular el resultado
 fmt.Printf("3 * 4 + 2 = %d\n", nuevaFuncion(4)) // (4 * 3) + 2 = 14
 fmt.Printf("3 * 7 + 2 = %d\n", nuevaFuncion(7)) // (7 * 3) + 2 = 23
}
```
