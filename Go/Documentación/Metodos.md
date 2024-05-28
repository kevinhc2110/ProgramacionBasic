# Métodos en Go: Funciones asociadas a tipos de datos

Los métodos en Go son funciones que se asocian a tipos de datos definidos por el usuario. Permiten encapsular comportamientos específicos de un tipo y mejorar la organización y legibilidad del código. Veamos sus características principales:

```go
package main

import "fmt"

func metodos() /*main*/  {

  // Usamos el método en nuestra función main

  p := Persona{
   Nombre: "Juan",
   Edad:   30,
  }
  p.Saludar()


  // Modificamos campo usando métodos receptores puntero
  p1 := Persona1{
   Nombre: "Juan",
   Edad:   30,
  }
  p1.CumplirAños()
  fmt.Println("Edad después de cumplir años:", p1.Edad)
}

// Métodos para estructuras

type Persona struct {
 Nombre string
 Edad   int
}

func (p Persona) Saludar() {
 fmt.Printf("Hola, mi nombre es %s y tengo %d años.\n", p.Nombre, p.Edad)
}

// Métodos con receptores puntero: Se usan para modificar el campo del struct

type Persona1 struct {
 Nombre string
 Edad   int
}

// Definición de un método para cambiar la edad
func (p1 *Persona1) CumplirAños() {
 p1.Edad++
}
```
