# Principio de Responsabilidad Única (Single Responsibility Principle, SRP)

El Principio de Responsabilidad Única establece que una clase debe tener una, y solo una, razón para cambiar. En otras palabras, una clase debe estar enfocada en una única tarea o responsabilidad.

## Ejemplo Correcto e Incorrecto en Go

```go
package main

import (
 "fmt"
 "log"
 "os"
)

// Usuario gestiona los usuarios y el logging
type Usuario struct {
 Nombre  string
 Correo  string
 logger  *log.Logger
}

// NuevoUsuario crea una nueva instancia de Usuario
func NuevoUsuario(nombre, correo string) *Usuario {
 file, err := os.OpenFile("app.log", os.O_APPEND|os.O_CREATE|os.O_WRONLY, 0666)
 if err != nil {
  log.Fatal(err)
 }
 logger := log.New(file, "INFO: ", log.Ldate|log.Ltime|log.Lshortfile)

 return &Usuario{
  Nombre:  nombre,
  Correo:  correo,
  logger:  logger,
 }
}

// Guardar guarda la información del usuario (ejemplo simplificado)
func (u *Usuario) Guardar() {
 // Lógica para guardar el usuario en la base de datos
 fmt.Printf("Guardando usuario: %s, %s\n", u.Nombre, u.Correo)
 u.logger.Println("Usuario guardado")
}

// Eliminar elimina al usuario (ejemplo simplificado)
func (u *Usuario) Eliminar() {
 // Lógica para eliminar el usuario de la base de datos
 fmt.Printf("Eliminando usuario: %s\n", u.Nombre)
 u.logger.Println("Usuario eliminado")
}

func main() {
 usuario := NuevoUsuario("Juan", "juan@example.com")
 usuario.Guardar()
 usuario.Eliminar()
}
```

**Problema del Ejemplo Incorrecto:**

En este ejemplo, la estructura Usuario tiene más de una responsabilidad: maneja la información de los usuarios y también realiza logging. Esto va en contra del principio SRP porque cualquier cambio en la forma en que se maneja el logging afectará a la clase Usuario.

## Ejemplo Correcto

Ahora, dividimos las responsabilidades en dos estructuras: Usuario y Logger.

```go
package main

import (
 "fmt"
 "log"
 "os"
)

// Usuario gestiona los usuarios
type Usuario struct {
 Nombre string
 Correo string
}

// Logger gestiona el logging
type Logger struct {
 logger *log.Logger
}

// NuevoUsuario crea una nueva instancia de Usuario
func NuevoUsuario(nombre, correo string) *Usuario {
 return &Usuario{
  Nombre: nombre,
  Correo: correo,
 }
}

// NuevoLogger crea una nueva instancia de Logger
func NuevoLogger() *Logger {
 file, err := os.OpenFile("app.log", os.O_APPEND|os.O_CREATE|os.O_WRONLY, 0666)
 if err != nil {
  log.Fatal(err)
 }
 logger := log.New(file, "INFO: ", log.Ldate|log.Ltime|log.Lshortfile)

 return &Logger{
  logger: logger,
 }
}

// Guardar guarda la información del usuario (ejemplo simplificado)
func (u *Usuario) Guardar() {
 // Lógica para guardar el usuario en la base de datos
 fmt.Printf("Guardando usuario: %s, %s\n", u.Nombre, u.Correo)
}

// Eliminar elimina al usuario (ejemplo simplificado)
func (u *Usuario) Eliminar() {
 // Lógica para eliminar el usuario de la base de datos
 fmt.Printf("Eliminando usuario: %s\n", u.Nombre)
}

// LogInfo registra información
func (l *Logger) LogInfo(mensaje string) {
 l.logger.Println(mensaje)
}

func main() {
 usuario := NuevoUsuario("Juan", "juan@example.com")
 logger := NuevoLogger()

 usuario.Guardar()
 logger.LogInfo("Usuario guardado")

 usuario.Eliminar()
 logger.LogInfo("Usuario eliminado")
}
```

_Usuario:_ Se encarga únicamente de manejar la información de los usuarios.
_Logger:_ Se encarga únicamente del logging.

De esta manera, cada estructura tiene una única responsabilidad, siguiendo así el principio de responsabilidad única. Esto hace que el código sea más mantenible y que los cambios en una responsabilidad no afecten a la otra.
