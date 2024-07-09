# El Principio de Sustitución de Liskov (Liskov Substitution Principle, LSP)

es uno de los principios SOLID en la programación orientada a objetos. Este principio establece que los objetos de una clase derivada deben poder sustituir a los objetos de la clase base sin alterar el correcto funcionamiento del programa. En otras palabras, si S es una subclase de T, entonces los objetos de tipo T pueden ser reemplazados por objetos de tipo S sin afectar la funcionalidad del programa.

Imaginemos una jerarquía de clases para formas geométricas con un método Area().

```go
package main

import (
 "fmt"
 "math"
)

// Forma es una interfaz que representa una forma geométrica
type Forma interface {
 Area() float64
}

// Rectangulo es una estructura que implementa la interfaz Forma
type Rectangulo struct {
 Ancho  float64
 Alto   float64
}

func (r Rectangulo) Area() float64 {
 return r.Ancho * r.Alto
}

// Circulo es una estructura que implementa la interfaz Forma
type Circulo struct {
 Radio float64
}

func (c Circulo) Area() float64 {
 return math.Pi * c.Radio * c.Radio
}

func main() {
 var forma Forma

 forma = Rectangulo{Ancho: 3, Alto: 4}
 fmt.Printf("Área del rectángulo: %.2f\n", forma.Area())

 forma = Circulo{Radio: 5}
 fmt.Printf("Área del círculo: %.2f\n", forma.Area())
}
```

En este ejemplo, tanto Rectangulo como Circulo implementan la interfaz Forma. Podemos intercambiar instancias de Rectangulo y Circulo sin problemas porque ambos cumplen con el contrato de la interfaz Forma, que es tener un método Area().

## Ejemplo Incorrecto

```go
package main

import (
 "fmt"
)

// Avestruz es una estructura que representa un avestruz
type Avestruz struct{}

// Volar intenta implementar una función de vuelo para Avestruz
func (a Avestruz) Volar() string {
 return "Las avestruces no pueden volar"
}

// Pajaro es una estructura que representa un pájaro genérico
type Pajaro struct{}

// Volar implementa una función de vuelo para Pajaro
func (p Pajaro) Volar() string {
 return "El pájaro está volando"
}

// Ave es una interfaz que representa un ave
type Ave interface {
 Volar() string
}

func main() {
 var ave Ave

 ave = Pajaro{}
 fmt.Println(ave.Volar())

 ave = Avestruz{}
 fmt.Println(ave.Volar())
}
```

En este ejemplo, tenemos una interfaz Ave con un método Volar(). La estructura Pajaro cumple con este contrato, pero la estructura Avestruz no lo hace de manera adecuada porque las avestruces no pueden volar. Aquí, la sustitución de un Pajaro por un Avestruz en el contexto de la interfaz Ave rompe el contrato implícito de que todos los Ave pueden volar.

## Ejemplo Correcto

```go
package main

import (
 "fmt"
)

// Ave es una interfaz que representa un ave con habilidades comunes
type Ave interface {
 Caminar() string
}

// AveVoladora es una interfaz que representa un ave que puede volar
type AveVoladora interface {
 Ave
 Volar() string
}

// Pajaro es una estructura que representa un pájaro genérico
type Pajaro struct{}

func (p Pajaro) Caminar() string {
 return "El pájaro está caminando"
}

func (p Pajaro) Volar() string {
 return "El pájaro está volando"
}

// Avestruz es una estructura que representa un avestruz
type Avestruz struct{}

func (a Avestruz) Caminar() string {
 return "El avestruz está caminando"
}

func main() {
 var ave Ave
 var aveVoladora AveVoladora

 ave = Avestruz{}
 fmt.Println(ave.Caminar())

 aveVoladora = Pajaro{}
 fmt.Println(aveVoladora.Caminar())
 fmt.Println(aveVoladora.Volar())
}
```

En este caso, hemos separado las habilidades comunes (Caminar) en una interfaz Ave y las habilidades de vuelo en una interfaz AveVoladora. De esta manera, las avestruces pueden implementar la interfaz Ave sin necesidad de implementar un método Volar() que no tiene sentido para ellas.
