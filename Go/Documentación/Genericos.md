# Genéricos en Go: Desbloqueando el poder de la programación polimórfica

Los genéricos llegaron a Go en la versión 1.18, introduciendo un paradigma poderoso para escribir código más flexible y reutilizable. Permiten definir funciones, estructuras y tipos de datos que pueden operar sobre diferentes tipos de datos sin necesidad de reescribir el código para cada tipo específico.

## Beneficios de los genéricos

**Mayor reutilización de código:** Las funciones y estructuras genéricas pueden ser utilizadas con diferentes tipos de datos, reduciendo la duplicación de código y mejorando la organización.
**Código más seguro:** Los genéricos permiten al compilador verificar la seguridad del tipo en tiempo de compilación, lo que reduce la posibilidad de errores en tiempo de ejecución.
**Mayor expresividad del código:** Los genéricos permiten expresar algoritmos y estructuras de datos de manera más concisa y elegante.

```go
package main

import "fmt"

func main() {

 fmt.Println(maxInt(1,3))
 fmt.Println(maxString("a", "b"))
 fmt.Println(max("a","b"))

 fmt.Println(sum("key1", 1, 3))
 fmt.Println(sum("key2", 3, 3))
}

// Considere una función que compara dos valores y devuelve el valor más grande. En Go tradicional, se necesitarían dos funciones separadas para comparar números enteros y cadenas de texto.

func maxInt(a, b int) int {
 if a > b {
  return a
 }
 return b
}

func maxString(a, b string) string {
 if a > b {
  return a
 }
 return b
}

// Con datos genéricos, se puede escribir una única función genérica que compara dos valores de cualquier tipo comparable.

func max[T int | string](a, b T) T {
 if  a > b {
  return a
 }
 return b
}

// Se puede usar con types

type Numeric interface {
 int | float64 |float32 | int32 | int64
}

func sum[K string, T Numeric](key K, a,b T)T {
 fmt.Println(key)
 return a + b
}
```
