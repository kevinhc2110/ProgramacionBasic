# Variables en Go: Dominando los fundamentos

Las variables en Go son elementos esenciales para almacenar y manipular datos dentro de tu programa. A continuación, se presenta un desglose de los conceptos clave relacionados con las variables en Go:

```go
package main

import (
 "fmt"
 "reflect"
)

//Declaración de variables

func variables() /*main*/  {
  var num int = 3
  var name string = "KevinDev"

  fmt.Println(num, name)

  // Declara e inicializa múltiples variables

  var a, b, c int = 1, 2, 3

  fmt.Println(a, b, c)

  num = 0
  name = "Sofia"

  var num2 = 0;
  var name2 string = "Dev"

  fmt.Println(num2, name2)

  // num2 = "" Seria un error porque el tipo que tomo anteriormente fue de int

  num2 = num2 + 8
  fmt.Println(num2)

  fmt.Println(num2 - 1)

  // Concatenar tipos diferentes

  fmt.Println(name2, num2)

  // Mostrar el tipo por consola

  fmt.Println(reflect.TypeOf(num))

  // Sumar entero y float

  var float1 float64 = 6.5
  fmt.Println(float1 + float64(num2))

  // Typecast
  // Convertir una variable de un tipo de dato a otro

  func average(length int, array []int) float64 {
      sum := 0
      for i := 0; i < length; i++ {
          sum += array[i]
      }
      return float64(sum) / float64(length)
  }

  // Mas tipos de datos

  // Booleans

  var bool1 bool = false
  fmt.Println(bool1)

  // Complejos

  var complejo complex128 = 2 + 3i
  fmt.Println(complejo)

  // Caracteres

  var caracter rune = 'a'
  fmt.Println(caracter)

  // Evitar usar el var para declarar e inicializar

  name3 := "Papi";
  fmt.Println(name3)

  // Constantes

  const myConst = "Kevin Llora"
  fmt.Println(myConst)
}
```

## Tipos de datos

_Go es un lenguaje de tipado estático, lo que significa que debes especificar el tipo de dato de una variable durante la declaración._
**Los tipos de datos comunes incluyen:**
_int:_ Enteros (números enteros)
_float32:_ Números de punto flotante con precisión de una sola precisión
_float64:_ Números de punto flotante con precisión doble
_string:_ Datos de texto
_bool:_ Valores booleanos (verdadero o falso)
_También puedes definir tipos de datos personalizados como estructuras y slices._
_"Runes" en Go se refiere al tipo de datos rune, que representa un punto de código Unicode._

## Alcance

_El alcance de una variable determina su visibilidad dentro de tu código._
_Las variables declaradas con var a nivel de paquete son accesibles en todo el programa._
_Las variables declaradas dentro de una función son locales a esa función y no se puede acceder a ellas desde el exterior._

## Valores cero

_Cada tipo de dato en Go tiene un valor cero predeterminado asignado a las variables no declaradas._
_Por ejemplo, el valor cero para int es 0, para float64 es 0.0, para string es una cadena vacía "" y para bool es false._

## Punteros

_Los punteros son variables que almacenan direcciones de memoria en lugar de valores directamente._
_Son útiles para modificar datos existentes y trabajar con funciones que esperan referencias._
_Los punteros se declaran con un asterisco (\*) antes del tipo de dato:_
