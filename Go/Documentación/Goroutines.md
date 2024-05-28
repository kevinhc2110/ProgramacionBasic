# Goroutines: Concurrencia liviana en Go

Los Goroutines son una de las características distintivas del lenguaje de programación Go. Son hilos de ejecución ligeros y gestionados por el runtime de Go, lo que permite ejecutar tareas de forma concurrente sin la complejidad y la sobrecarga de los hilos tradicionales del sistema operativo.

## Características principales de los Goroutines

- **Ligeros**: Los Goroutines requieren menos memoria y recursos de CPU en comparación con los hilos tradicionales.
- **Gestionados por el runtime**: El runtime de Go se encarga de la creación, programación y eliminación de Goroutines, simplificando la gestión de la concurrencia.
- **Comunicación a través de canales**: Los Goroutines se comunican entre sí mediante canales, que permiten enviar y recibir valores de forma segura.
- **Ejecución en un mismo espacio de direcciones**: Los Goroutines comparten el mismo espacio de direcciones de memoria, lo que facilita el acceso y la modificación de datos compartidos.

## Ventajas de usar Goroutines

- **Mejora del rendimiento**: Al ejecutar tareas de forma concurrente, los Goroutines pueden mejorar el rendimiento general de la aplicación, especialmente en tareas intensivas en E/S o que no requieren mucha CPU.
- **Mayor escalabilidad**: Las aplicaciones que utilizan Goroutines pueden escalarse de manera eficiente para aprovechar al máximo los recursos disponibles.
- **Simplifica la programación concurrente**: La abstracción de los Goroutines y la gestión por parte del runtime facilitan la escritura de código concurrente sin la complejidad de los hilos tradicionales.

## Ejemplos de uso de Goroutines

- **Procesamiento de E/S**: Los Goroutines se pueden usar para manejar solicitudes de red, operaciones de archivo u otras tareas de E/S de forma concurrente, mejorando la capacidad de respuesta de la aplicación.
- **Cálculos intensivos**: Las tareas de cálculo intensivas se pueden dividir en Goroutines para aprovechar múltiples núcleos de CPU y acelerar el procesamiento.
- **Aplicaciones web**: Los servidores web pueden usar Goroutines para manejar múltiples solicitudes de clientes simultáneamente, mejorando el rendimiento y la escalabilidad.

## Comparación con hilos tradicionales

Los Goroutines se diferencian de los hilos tradicionales del sistema operativo en varios aspectos:

- **Ligeros**: Los Goroutines requieren menos memoria y recursos de CPU que los hilos tradicionales.
- **Gestión por el runtime**: El runtime de Go se encarga de la gestión de Goroutines, mientras que los hilos tradicionales requieren programación manual por parte del desarrollador.
- **Comunicación a través de canales**: Los Goroutines se comunican mediante canales, mientras que los hilos tradicionales utilizan mecanismos como mutex y semáforos para la sincronización.
- **Ejecución en un mismo espacio de direcciones**: Los Goroutines comparten el mismo espacio de direcciones de memoria, mientras que los hilos tradicionales tienen sus propios espacios de direcciones.

### Ejemplo de uso de Goroutines

```go
package main

import (
    "fmt"
    "time"
)

// Función que se ejecutará de manera asíncrona.
// Recibe el nombre de la tarea, la duración en segundos y un canal done para notificar cuando termina.
// Simula la duración de la ejecución usando time.Sleep.
// Imprime el tiempo de inicio, la duración y el tiempo de finalización.

func ejecutarAsincrono(nombre string, duracion int, done chan bool) {
    fmt.Printf("La función '%s' empieza a las %v\n", nombre, time.Now())
    fmt.Printf("La función '%s' se ejecutará durante %d segundos\n", nombre, duracion)
    time.Sleep(time.Duration(duracion) * time.Second)
    fmt.Printf("La función '%s' terminó a las %v\n", nombre, time.Now())
    done <- true
}

func main() {
    // Crear un canal para sincronización.
    done := make(chan bool)

    // Ejecutar la función en una Goroutine para que se ejecute de manera asíncrona.
    go ejecutarAsincrono("Tarea Asíncrona", 5, done)

    // Esperar a que la función termine leyendo del canal done.
    <-done
    fmt.Println("La ejecución ha finalizado")
}
```

## Paralelismo en Go

En el mundo de la programación, el paralelismo se refiere a la capacidad de ejecutar múltiples tareas simultáneamente para lograr un mayor rendimiento y eficiencia.
Go es un lenguaje diseñado para aprovechar la concurrencia de manera eficiente, lo que incluye tanto la concurrencia como el paralelismo.

### Concurrencia vs Paralelismo

- **Concurrencia**: Se refiere a la capacidad de ejecutar múltiples tareas en un período de tiempo solapado. En Go, se logra fácilmente con goroutines, que son hilos de ejecución ligeros. La concurrencia es ideal para manejar operaciones I/O intensivas, como solicitudes de red o escritura en disco, donde la CPU está esperando a que se complete la operación.
- **Paralelismo**: Implica ejecutar múltiples tareas simultáneamente en múltiples núcleos de CPU. En Go, el paralelismo se logra ejecutando múltiples goroutines en paralelo. Es especialmente útil para operaciones CPU-bound, como cálculos intensivos, donde se puede distribuir la carga de trabajo en varios núcleos de CPU para mejorar el rendimiento.

## `sync.WaitGroup`

En Go, `sync.WaitGroup` es una estructura que se utiliza para coordinar y esperar la finalización de múltiples goroutines antes de continuar la ejecución del programa principal.

- `wg.Add(1)`: Se utiliza para incrementar el contador de la `WaitGroup` antes de iniciar cada goroutine.
- `wg.Done()`: Se llama al finalizar cada goroutine para indicar que ha terminado su ejecución.
- `wg.Wait()`: Bloquea la ejecución del programa principal hasta que todas las goroutines hayan llamado a `Done`.

## `sync.Mutex`

Un Mutex (mutual exclusion) es una estructura de datos utilizada en programación concurrente para controlar el acceso a un recurso compartido, garantizando que solo una goroutine pueda acceder a ese recurso en un momento dado. Esencialmente, un Mutex actúa como un candado que una goroutine debe adquirir antes de acceder al recurso compartido y luego liberar una vez que haya terminado de utilizarlo.

En Go, el paquete `sync` proporciona una implementación de Mutex a través de la estructura `sync.Mutex`. Un Mutex tiene dos métodos principales: `Lock` y `Unlock`. Cuando una goroutine quiere acceder al recurso protegido por el Mutex, llama al método `Lock` para bloquearlo, evitando que otras goroutines accedan al recurso simultáneamente. Una vez que ha terminado de usar el recurso, la goroutine llama al método `Unlock` para desbloquear el Mutex y permitir que otras goroutines accedan al recurso.

### Ejemplo de uso de `sync.WaitGroup` & `sync.Mutex`

```go
package main

import (
    "fmt"
    "sync"
)

var contador int // Recurso compartido

func incrementar(wg *sync.WaitGroup, mu *sync.Mutex) {

    defer wg.Done() // Indica al grupo de espera que esta goroutine ha finalizado al salir de la función
    mu.Lock()       // Bloquea el Mutex para garantizar exclusión mutua al acceder al recurso compartido
    contador++      // Accede y modifica el recurso compartido (variable contador) de manera segura
    mu.Unlock()     // Desbloquea el Mutex después de usar el recurso compartido
}

func main() {
    var wg sync.WaitGroup // Declara una instancia de WaitGroup para coordinar las goroutines
    var mu sync.Mutex     // Declara una instancia de Mutex para garantizar la exclusión mutua

    // Bucle para iniciar 1000 goroutines
    for i := 0; i < 1000; i++ {
        wg.Add(1)                 // Agrega una goroutine al grupo de espera
        go incrementar(&wg, &mu)  // Inicia una goroutine que ejecuta la función incrementar
    }

    wg.Wait() // Bloquea la ejecución del programa principal hasta que todas las goroutines hayan finalizado

    // Una vez que todas las goroutines han finalizado, muestra el valor final del contador
    fmt.Println("Valor final del contador:", contador)
}
```
