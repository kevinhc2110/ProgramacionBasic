# El Contexto en Go: Controlando la Ejecución y Comunicando Valores

En Go, el contexto (context) es un paquete estándar que proporciona un método para pasar información y señales a través de los límites de la API y entre goroutines. Es especialmente útil para gestionar la cancelación de operaciones, establecer tiempos de espera (timeouts) y almacenar valores específicos de solicitud en aplicaciones concurrentes.

El paquete context es ampliamente utilizado en aplicaciones que manejan múltiples goroutines, como servidores web, para propagar la cancelación de operaciones a través de llamadas de función anidadas.

## Características principales del contexto

**Propagación de valores:** El contexto permite propagar valores clave-valor a través de diferentes niveles de la pila de llamadas, lo que facilita el acceso a información contextual en diferentes partes de la aplicación.
**Cancelación de operaciones:** El contexto proporciona mecanismos para cancelar operaciones en curso, como solicitudes HTTP o tareas de larga duración, evitando recursos no utilizados y mejorando la eficiencia.
**Detección de plazos:** El contexto permite establecer plazos para las operaciones, lo que garantiza que se completen dentro de un tiempo determinado y se eviten bloqueos o tiempos de espera infinitos.
**Valores de contexto personalizados:** Se pueden definir valores de contexto personalizados para almacenar información específica de la aplicación, como identificadores de solicitudes, datos de autenticación o información de rastreo.

## Componentes del Paquete context

### El paquete context define cuatro tipos principales

**context.Context:** Una interfaz que lleva plazos (deadlines), cancelaciones y otros valores a través de los límites de la API.
**context.Background:** Devuelve un contexto vacío. Es el contexto raíz más básico, generalmente utilizado en la función principal o en los tests.
**context.TODO:** Devuelve un contexto vacío que se usa cuando el contexto aún no se ha decidido o no está disponible.
**context.WithCancel, context.WithTimeout, context.WithDeadline, context.WithValue:** Funciones para crear contextos derivados.

### Ejemplo de uso de context

```go
package main

import (
 "context"
 "fmt"
 "time"
)

func main() {

 // Crear un contexto con cancelación

 ctx, cancel := context.WithCancel(context.Background())

 // Lanzar una goroutine para realizar una tarea que puede tardar mucho tiempo

 go func() {
  for {
   select {
   case <-ctx.Done():
    fmt.Println("Tarea cancelada.")
    return
   default:
    // Simular una tarea que lleva tiempo
    time.Sleep(1 * time.Second)
    fmt.Println("Realizando tarea...")
   }
  }
 }()

 // Simular una acción del usuario que desencadena la cancelación

 time.Sleep(3 * time.Second)
 fmt.Println("Cancelando tarea...")
 cancel() // Cancelar la tarea

 // Esperar un momento para que la goroutine tenga tiempo de finalizar

 time.Sleep(1 * time.Second)
 fmt.Println("Programa terminado.")
}
```
