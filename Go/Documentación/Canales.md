# Canales en Go: Comunicación entre Goroutines

Los canales en Go son un mecanismo de comunicación fundamental para la programación concurrente. Permiten a las Goroutines (hilos de ejecución ligeros) enviar y recibir datos de forma segura y eficiente, facilitando la sincronización y el intercambio de información entre diferentes partes de un programa.

## Operaciones con canales

**len(channel):** Devuelve la cantidad de datos que están actualmente en el canal.
**cap(channel):** Devuelve la capacidad máxima del canal (la cantidad máxima de datos que puede almacenar).
**close(channel):** Cierra el canal, indicando que no se enviarán más datos.

## Beneficios de usar canales

**Comunicación segura:** Los canales garantizan la comunicación segura entre Goroutines, evitando conflictos de datos y problemas de concurrencia.
**Sincronización:** Los canales permiten sincronizar la ejecución de Goroutines, asegurándose de que se completen ciertas tareas antes de continuar con otras.
**Decoupling:** Los canales desacoplan las Goroutines entre sí, permitiendo una mayor modularidad y flexibilidad en el diseño del código.

### Ejemplo de sintaxis

```go
package main

import (
 "errors"
 "fmt"
 "time"
)

func main() {

  // Declaración de canal
  canal := make(chan int)
  // Goroutine anónima que se ejecuta en paralelo con la función principal
  go func() {
    // El operador <- se utiliza para recibir el valor del canal
    canal <- 42
  }()
  resultado := <-canal
  fmt.Println(resultado)
}

```

## Tipos de canales

**Canales unidireccionales:** Solo permiten enviar o recibir datos en una dirección. Se especifican con la palabra clave chan seguida del tipo de valor y la flecha de dirección (<- o ->).
**Canales bidireccionales sin Buffer :** Permiten enviar y recibir datos en ambas direcciones. Se especifican con la palabra clave chan seguida del tipo de valor.
**Canales bidireccionales con Buffer:** Canales con Buffer, permite almacenar un número limitado de valores se especifican con la palabra clave chan seguida del tipo de valor y su buffer

### Ejemplo de tipos de canales

```go
// Canales unidireccionales:
sendCh := make(chan<- int) // Canal de envío solo para valores enteros
recvCh := make(<-chan int) // Canal de recepción solo para valores enteros

// Canales bidireccionales sin Buffer
ch := make(chan bool)

// Canales bidireccionales con Buffer
ch := make(chan int, 10)
```

## Algunos ejemplos de uso

**Procesamiento de E/S:** Los canales pueden usarse para manejar solicitudes de red, operaciones de archivo u otras tareas de E/S de forma concurrente, mejorando la capacidad de respuesta de la aplicación.
**Cálculos intensivos:** Las tareas de cálculo intensivas se pueden dividir en Goroutines que se comunican a través de canales para compartir resultados y progresos.
**Aplicaciones web:** Los servidores web pueden usar canales para manejar múltiples solicitudes de clientes simultáneamente, mejorando el rendimiento y la escalabilidad.

## Otros conceptos importantes

## select

En Go, la instrucción select se utiliza para esperar simultáneamente en múltiples canales. Permite que un goroutine bloquee su ejecución hasta que uno de sus casos de canal esté listo para operar. Cuando varios casos están listos, select elige uno de ellos al azar para ejecutar. Si ninguno de los casos está listo y no hay un caso default, la ejecución de la goroutine se bloquea hasta que al menos uno de los casos esté listo.

## close

En Go, la función close() se utiliza para cerrar un canal. Cerrar un canal indica que no se enviarán más valores a ese canal. Cuando un canal se cierra, los receptores pueden seguir recibiendo valores del canal, pero ya no pueden enviar valores a él.

### Ejemplo de select + close

```go
package main

import (
 "fmt"
 "time"
)

func main() {
 ch := make(chan int)

 // Goroutine para enviar valores al canal
 go func() {
  for i := 1; i <= 5; i++ {
   time.Sleep(500 * time.Millisecond) // Simular alguna operación
   ch <- i
  }
  close(ch) // Cerrando el canal después de enviar todos los valores
 }()

 // Goroutine para recibir valores del canal
 go func() {
  for {
   select {
   case val, ok := <-ch:
    if !ok {
     fmt.Println("El canal está cerrado.")
     return
    }
    fmt.Println("Received:", val)
   }
  }
 }()

 // Esperar a que las goroutines terminen
 var input string
 fmt.Scanln(&input)
}
```

## done

done es un canal utilizado para señalizar que una goroutine ha terminado su trabajo. Es un canal de tipo booleano (chan bool) que se utiliza para enviar una señal simple (true en este caso) cuando la goroutine ha completado su tarea.

## errCh

Los canales de error (errCh) se utilizan para manejar errores de forma concurrente. En el ejemplo, errCh es un canal de tipo error (chan error) que se utiliza para enviar posibles errores generados por la ejecución de alguna tarea. En la goroutine dentro de main, se llama a la función doSomething que realiza una tarea que podría fallar y devuelve un error. Este error se envía a través del canal errCh para que pueda ser manejado de manera concurrente en el bloque principal (main). Si hay un error, se imprime; de lo contrario, se asume que la tarea se completó correctamente.

### Ejemplo de done + errorCh

```go
package main

import (
 "fmt"
 "errors"
)

// Función que realiza algún trabajo y notifica cuando termina
func doWork(done chan bool) {
 // Simulación de alguna tarea
 fmt.Println("Haciendo algo...")
 // Notificar que el trabajo ha terminado
 done <- true
}

// Función que realiza algún trabajo y envía un posible error
func doSomething() error {
 // Simulación de alguna tarea que puede fallar
 return errors.New("algo salió mal")
}

func main() {
 // Canal de señalización para notificar que la goroutine ha terminado
 done := make(chan bool)

 // Goroutine para realizar el trabajo y notificar cuando termina
 go doWork(done)

 // Esperar hasta que el trabajo haya terminado
 <-done
 fmt.Println("El trabajo ha finalizado.")

 // Canal de errores para manejar posibles errores concurrentemente
 errCh := make(chan error)

 // Goroutine para realizar alguna tarea que puede generar un error
 go func() {
  err := doSomething()
  errCh <- err
 }()

 // Esperar a que se reciba un posible error del canal de errores
 err := <-errCh
 if err != nil {
  fmt.Println("Error:", err)
 } else {
  fmt.Println("La tarea se completó sin errores.")
 }
}
```

## Canales de Datos y Control

Canales de Datos y Control son dos tipos de canales que se usan conjuntamente para manejar la transmisión de datos y la sincronización del control entre goroutines.

**Canales de Datos:** Se utilizan para transmitir datos entre goroutines.
**Canales de Control:** Se utilizan para enviar señales de control, como notificaciones de que una tarea ha terminado o que se ha producido un evento particular.

## Canales de Resultado

Se utilizan para devolver resultados de funciones concurrentes. Son útiles cuando una goroutine realiza una operación que produce un resultado que debe ser utilizado por otra goroutine o la función principal.

### Ejemplo de canal de datos y control + canal de resultados

```go
package main

import (
 "fmt"
 "time"
)

// Función que genera datos y envía al canal de datos
func sendData(dataCh chan int, controlCh chan bool) {
 for i := 1; i <= 5; i++ {
  time.Sleep(500 * time.Millisecond) // Simulación de alguna tarea
  dataCh <- i                        // Enviar datos al canal de datos
 }
 close(dataCh) // Cerrar el canal de datos una vez que se hayan enviado todos los datos
 controlCh <- true
}

func main() {
 // Canal de datos para enviar números
 dataCh := make(chan int)

 // Canal de control para recibir señales de finalización
 controlCh := make(chan bool)

 // Goroutine para enviar datos y controlar su flujo
 go sendData(dataCh, controlCh)

 // Bucle para recibir datos del canal de datos hasta que se cierre
 for val := range dataCh {
  fmt.Println("Received data:", val)
 }

 // Recibir señal de control para confirmar la finalización
 <-controlCh
 fmt.Println("Data transmission completed.")

 // Canal de resultado para recibir el resultado de una tarea concurrente
 resultCh := make(chan int)

 // Goroutine para realizar alguna tarea y enviar el resultado al canal de resultado
 go func() {
  // Simulación de alguna tarea que tarda un tiempo en completarse
  time.Sleep(1 * time.Second)
  resultCh <- 42 // Enviar el resultado al canal de resultado
 }()

 // Esperar y recibir el resultado del canal de resultado
 result := <-resultCh
 fmt.Println("Result received:", result)
}

```
