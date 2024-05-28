# Estructuras en Go: Bloques de construcción para datos compuestos

En Go, un struct (estructura) es un tipo de dato compuesto que permite agrupar varios campos, cada uno de los cuales puede tener un tipo diferente. Los structs son similares a las clases en otros lenguajes de programación orientados a objetos, aunque Go no soporta directamente la orientación a objetos tradicional.

## Casos de uso comunes para estructuras

_Representar entidades del mundo real (por ejemplo, Persona, Producto, Pedido)_
_Agrupar datos relacionados para una mejor organización (por ejemplo, Punto con coordenadas X e Y)_
_Pasar estructuras de datos complejas como argumentos de función_
_Crear tipos de datos personalizados con comportamiento (usando métodos)_

## Puntos clave

_Las estructuras proporcionan una forma estructurada de organizar datos._
_Puede acceder a los campos usando la notación de punto._
_Los valores cero se asignan cuando los campos no se inicializan explícitamente._
_Los punteros de estructura permiten el acceso y la modificación indirectos._
_Los métodos de estructura agregan funcionalidad a sus estructuras._

### Ejemplo de uso de struct

```go
package main

import "fmt"

// Definimos una estructura llamada Persona

type Persona struct {
 Nombre  string
 Edad    int
 Correo  string
}

func main() {

 // No hay clases si no estructuras

 // Crear una nueva instancia de Persona

 persona := NuevaPersona("Juan Pérez", 30, "juan.perez@example.com")

 // Imprimir los detalles de la persona

 fmt.Println("Detalles iniciales de la persona:")
 persona.ImprimirDetalles()

 // Modificar los detalles de la persona

 persona.ModificarDetalles("María López", 25, "maria.lopez@example.com")

 // Imprimir los detalles modificados de la persona

 fmt.Println("\nDetalles modificados de la persona:")
 persona.ImprimirDetalles()

}

// Método para inicializar una nueva Persona

func NuevaPersona(nombre string, edad int, correo string) *Persona {
 return &Persona{
  Nombre: nombre,
  Edad:   edad,
  Correo: correo,
 }
}

// Método para imprimir los detalles de la Persona

func (p *Persona) ImprimirDetalles() {
 fmt.Printf("Nombre: %s\nEdad: %d\nCorreo: %s\n", p.Nombre, p.Edad, p.Correo)
}

// Método para modificar los detalles de la Persona

func (p *Persona) ModificarDetalles(nombre string, edad int, correo string) {
 p.Nombre = nombre
 p.Edad = edad
 p.Correo = correo
}
```
