# Arrays y Slices en Go: Diferencias y Usos Comunes

En Go, los arrays y slices son estructuras de datos fundamentales para almacenar colecciones de elementos. Si bien ambos sirven para guardar valores de un mismo tipo, presentan diferencias importantes en su funcionamiento y uso.

## Arrays en Go

**Tamaño fijo:** Un array tiene un tamaño definido en el momento de su declaración que no puede modificarse posteriormente.
**Tipados:** Los arrays están tipados por el tipo de elemento que almacenan.
**Acceso por índice:** Se accede a los elementos de un array utilizando su índice numérico.
**Declaración:** La sintaxis para declarar un array es tipoDeElemento [tamaño]variable.

```go
package main

import "fmt"

func main() {

  // Array

  // Crear array
  var myArray [3]int

  // Crear un array de strings con datos predefinidos
  datos := [5]string{"dato1", "dato2", "dato3", "dato4", "dato5"}

  myArray[0] = 1
  myArray[1] = 1
  myArray[2] = 1

  fmt.Println(myArray)
  fmt.Println(myArray[2])
}
```

## Slices en Go

**Tamaño dinámico:** Un slice tiene un tamaño inicial que puede crecer o disminuir durante la ejecución del programa.
**Tipados:** Los slices están tipados por el tipo de elemento que almacenan.
**Acceso por índice:** Se accede a los elementos de un slice utilizando su índice numérico.
**Declaración:** La sintaxis para declarar un slice es tipoDeElemento []variable.

```go
func main() {

 // Creación de un slice vacío

 var s []int

 // Agregar elementos al slice usando la función append

 s = append(s, 2, 3, 4)

 fmt.Println(s)

 // Acceder a elementos individuales del slice

 fmt.Println("Primer elemento:", s[0])
 fmt.Println("Segundo elemento:", s[1])

 // Modificar elementos del slice

 s[0] = 5
 fmt.Println("Slice modificado:", s)

 // Obtener longitud y capacidad del slice

 fmt.Println("Longitud del slice:", len(s))
 fmt.Println("Capacidad del slice:", cap(s))

 // Crear un slice con make especificando longitud y capacidad
 // Longitud (Length): La longitud de un slice es el número de elementos que contiene actualmente.
 // Capacidad (Capacity): La capacidad de un slice es el número máximo de elementos que puede contener sin tener que asignar más memoria.
 // Puedes obtener la capacidad de un slice usando la función cap().

 s2 := make([]int, 3, 5) // longitud: 3, capacidad: 5
 fmt.Println("Slice s2:", s2)
 fmt.Println("Longitud de s2:", len(s2))
 fmt.Println("Capacidad de s2:", cap(s2))

 // Iterar sobre los elementos del slice

 fmt.Println("Iterando sobre los elementos de s:")
 for i, v := range s {
   fmt.Printf("Índice: %d, Valor: %d\n", i, v)
 }

 // Conjunto slice

 // Crear un slice vacío para simular el conjunto de datos

 conjunto := []int{}

 // Añadir un elemento al final

 conjunto = append(conjunto, 10)

 // Añadir un elemento al principio
 // El ... después de conjunto indica que se están pasando todos los elementos de conjunto como argumentos individuales a la función append.

 conjunto = append([]int{5}, conjunto...)

 // Añadir varios elementos en bloque al final

 conjunto = append(conjunto, []int{20, 30, 40}...)

 // Añadir varios elementos en bloque en una posición concreta

 posicion := 2
 elementos := []int{15, 25}
 conjunto = append(conjunto[:posicion], append(elementos, conjunto[posicion:]...)...)

 // Eliminar un elemento en una posición concreta
 // conjunto[:posicionEliminar]: Obtiene una porción del slice conjunto que va desde el inicio hasta la posición especificada (sin incluir la posición).

 posicionEliminar := 3
 conjunto = append(conjunto[:posicionEliminar], conjunto[posicionEliminar+1:]...)

 // Actualizar el valor de un elemento en una posición concreta

 posicionActualizar := 1
 nuevoValor := 50
 conjunto[posicionActualizar] = nuevoValor

 // Comprobar si un elemento está en el conjunto

 elementoBuscar := 30
 encontrado := false
 for _, num := range conjunto {
  if num == elementoBuscar {
   encontrado = true
   break
  }
 }
 if encontrado {
  fmt.Printf("El elemento %d está en el conjunto.\n", elementoBuscar)
 } else {
  fmt.Printf("El elemento %d no está en el conjunto.\n", elementoBuscar)
 }

 // Eliminar todo el contenido del conjunto

 conjunto = nil

 // Imprimir el conjunto después de todas las operaciones

 fmt.Println("Contenido del conjunto:", conjunto)
}
```
