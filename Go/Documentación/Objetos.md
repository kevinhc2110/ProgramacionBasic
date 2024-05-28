# Objetos en Go: Encapsulando datos y comportamiento

En Go, los objetos se basan en la idea de tipos de datos definidos por el usuario que encapsulan datos (atributos) y comportamiento (métodos). Si bien Go no es un lenguaje orientado a objetos tradicional como Java o C++, sí permite crear estructuras similares a objetos a través de tipos de datos y métodos.

```go
package main

import "fmt"

//En Go, no existe la herencia en el mismo sentido que en otros lenguajes orientados a objetos como Java o Python. Sin embargo, Go usa interfaces y composición para lograr un comportamiento similar.
// Definir la interfaz Animal

type Animal interface {
 HacerSonido() string
}

// Definir la estructura Perro

type Perro struct {
 Nombre string
}

// Implementar el método HacerSonido para Perro

func (p Perro) HacerSonido() string {
 return "Guau"
}

// Definir la estructura Gato

type Gato struct {
 Nombre string
}

// Implementar el método HacerSonido para Gato

func (g Gato) HacerSonido() string {
 return "Miau"
}

// Función para imprimir el sonido de cualquier Animal

func imprimirSonido(animal Animal) {
 fmt.Println(animal.HacerSonido())
}

func objetos() /*main*/ {

 // Crear instancias de Perro y Gato

 perro := Perro{Nombre: "Fido"}
 gato := Gato{Nombre: "Misu"}

 // Imprimir el sonido de cada animal

 imprimirSonido(perro)
 imprimirSonido(gato)
}
```
