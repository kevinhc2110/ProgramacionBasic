# El Principio de Segregación de Interfaces (Interface Segregation Principle, ISP)

Establece que una clase no debería estar obligada a implementar interfaces que no usa. En lugar de una interfaz grande, es preferible crear interfaces más pequeñas y específicas para cada cliente.

## Ejemplo Incorrecto

Supongamos que tenemos una interfaz grande que representa las operaciones de un trabajador en una empresa.

```go
package main

import (
 "fmt"
)

// Trabajador define una interfaz grande con muchas operaciones
type Trabajador interface {
 DesarrollarSoftware()
 AdministrarServidores()
 LlevarContabilidad()
}

// Desarrollador es una estructura que representa a un desarrollador de software
type Desarrollador struct{}

func (d Desarrollador) DesarrollarSoftware() {
 fmt.Println("Desarrollando software...")
}

func (d Desarrollador) AdministrarServidores() {
 // No se necesita este método para un desarrollador
}

func (d Desarrollador) LlevarContabilidad() {
 // No se necesita este método para un desarrollador
}

func main() {
 var trabajador Trabajador = Desarrollador{}
 trabajador.DesarrollarSoftware()
 // Los otros métodos no son necesarios, pero deben ser implementados
}
```

En este ejemplo, la interfaz Trabajador es demasiado grande y obliga a la clase Desarrollador a implementar métodos que no necesita (AdministrarServidores y LlevarContabilidad).

## Ejemplo Correcto

Para seguir el principio de segregación de interfaces, dividimos la interfaz Trabajador en varias interfaces más pequeñas y específicas.

```go
package main

import (
 "fmt"
)

// DesarrolladorDeSoftware define una interfaz para desarrollo de software
type DesarrolladorDeSoftware interface {
 DesarrollarSoftware()
}

// AdministradorDeServidores define una interfaz para administración de servidores
type AdministradorDeServidores interface {
 AdministrarServidores()
}

// Contable define una interfaz para llevar la contabilidad
type Contable interface {
 LlevarContabilidad()
}

// Desarrollador es una estructura que representa a un desarrollador de software
type Desarrollador struct{}

func (d Desarrollador) DesarrollarSoftware() {
 fmt.Println("Desarrollando software...")
}

// Administrador es una estructura que representa a un administrador de servidores
type Administrador struct{}

func (a Administrador) AdministrarServidores() {
 fmt.Println("Administrando servidores...")
}

// Contador es una estructura que representa a un contable
type Contador struct{}

func (c Contador) LlevarContabilidad() {
 fmt.Println("Llevando la contabilidad...")
}

func main() {
 var desarrollador DesarrolladorDeSoftware = Desarrollador{}
 var administrador AdministradorDeServidores = Administrador{}
 var contable Contable = Contador{}

 desarrollador.DesarrollarSoftware()
 administrador.AdministrarServidores()
 contable.LlevarContabilidad()
}
```

Con esta segregación de interfaces, seguimos el principio ISP, asegurándonos de que las clases no se vean forzadas a implementar métodos que no necesitan. Esto hace que el código sea más limpio, mantenible y fácil de entender.
