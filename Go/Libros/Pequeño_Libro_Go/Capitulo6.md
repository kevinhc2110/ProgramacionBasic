# Capítulo 5 - Exquisiteces

## Go-rutinas

Una go-rutina es similar a un hilo, pero es gestionada por Go, no por el sistema operativo. Permite la ejecución concurrente de código.

### Ejemplo de Go-rutinas

```go
package main
import (
    "fmt"
    "time"
)

func main() {
    fmt.Println("inicio")
    go process()                      // Inicia una nueva go-rutina que ejecuta la función process
    time.Sleep(time.Millisecond * 10) // Espera 10 milisegundos para dar tiempo a la go-rutina
    fmt.Println("terminado")
}

func process() {
    fmt.Println("procesando")         // Código ejecutado por la go-rutina
}
```

_Se usa time.Sleep para evitar que la función main termine antes de que la go-rutina process tenga la oportunidad de ejecutarse. Este enfoque es una mala práctica._

### Funciones anónimas

Para ejecutar un poco de código sin definir una función separada, podemos usar una función anónima:

```go
go func() {
    fmt.Println("procesando") // Código ejecutado por la go-rutina anónima
}()
```

## Sincronización en Go

Es necesario coordinar el código concurrente.

### Conceptos Básicos de Concurrencia

Escribir código concurrente implica prestar atención a dónde y cómo se leen y escriben valores.

**Ejemplo de concurrencia incorrecta:**

```go
package main
import (
    "fmt"
    "time"
)

var counter = 0

func main() {
    for i := 0; i < 2; i++ {
        go incr()                  // Inicia dos go-rutinas que ejecutan la función incr
    }
    time.Sleep(time.Millisecond * 10) // Espera 10 milisegundos para dar tiempo a las go-rutinas
}

func incr() {
    counter++                      // Incrementa el contador
    fmt.Println(counter)           // Imprime el valor del contador
}
```

**Problemas:**

_Salida no determinística_
_Riesgos de concurrencia_

### Sincronización con Mutex

Las escrituras necesitan estar sincronizadas. Una forma común de lograr esto es usar un mutex.

**Ejemplo de Sincronización con Mutex:**

```go
package main
import (
    "fmt"
    "time"
    "sync"
)

var (
    counter = 0
    lock    sync.Mutex
)

func main() {
    for i := 0; i < 2; i++ {
        go incr()                  // Inicia dos go-rutinas que ejecutan la función incr
    }
    time.Sleep(time.Millisecond * 10) // Espera 10 milisegundos para dar tiempo a las go-rutinas
}

func incr() {
    lock.Lock()                    // Bloquea el acceso al código protegido
    defer lock.Unlock()            // Desbloquea al finalizar la función
    counter++                      // Incrementa el contador de forma segura
    fmt.Println(counter)           // Imprime el valor del contador
}
```

_Mutex: Un mutex organiza el acceso a un código protegido. lock sync.Mutex crea un mutex inicialmente desbloqueado._
_Bloqueo y Desbloqueo: lock.Lock() bloquea el acceso y lock.Unlock() lo desbloquea. El uso de defer asegura que el mutex se libere al finalizar la función._

**Problemas comunes:**

_Sobreprotección: roteger una gran cantidad de código puede menoscabar la concurrencia, creando cuellos de botella._
_Deadlocks: Pueden ocurrir si se tienen múltiples bloqueos y una go-rutina necesita un bloqueo que otra ya tiene. Incluso con un único bloqueo, olvidarse de liberarlo puede causar un deadlock._

_Ejemplo de Deadlock:_

```go
package main
import (
    "time"
    "sync"
)

var lock sync.Mutex

func main() {
    go func() { lock.Lock() }()   // Inicia una go-rutina que bloquea el mutex
    time.Sleep(time.Millisecond * 10)
    lock.Lock()                   // Intenta bloquear el mutex que ya está bloqueado
}
```

**Lectura y Escritura Concurrente:**

Existen mutex de lectura-escritura como sync.RWMutex que permiten bloquear lectores y escritores de manera independiente.

## Canales en Go

Los canales en Go hacen la programación concurrente más sencilla al eliminar los datos compartidos. Un canal es un medio de comunicación entre go-rutinas que se utiliza para enviar datos.

### Creación y Uso de Canales

```go
c := make(chan int)
```

_El tipo del canal es chan int. Para mandar el canal a una función como parámetro, la firma debe ser:_

```go
func worker(c chan int) { ... }
```

### Operaciones en Canales

Los canales permiten dos operaciones: enviar y recibir.

```go
CANAL <- DATOS // Enviamos aso
```

```go
VARIABLE := <-CANAL // Recibimos asi
```

Enviar y recibir a y desde un canal es bloqueante. Esto significa que la go-rutina no continuará hasta que los datos estén disponibles o hayan sido recibidos.

**Ejemplo de Uso de Canales:**

Considera un sistema donde manejamos los datos de entrada en go-rutinas separadas.

```go
package main

import (
    "fmt"
    "time"
    "math/rand"
)

// Definición de la estructura Worker
type Worker struct {
    id int
}

// Método process de la estructura Worker
func (w Worker) process(c chan int) {
    for {
        data := <-c // Espera a recibir datos del canal c
        fmt.Printf("worker %d got %d\n", w.id, data) // Procesa los datos recibidos
    }
}

func main() {
    c := make(chan int) // Creación de un canal de tipo int

    // Iniciamos varios workers que procesan datos del canal
    for i := 0; i < 4; i++ {
        worker := Worker{id: i}
        go worker.process(c) // Inicia la go-rutina del worker con el canal c
    }

    // Simulación de una fuente de trabajo constante enviando datos aleatorios al canal
    for {
        c <- rand.Int() // Envía datos aleatorios al canal c
        time.Sleep(time.Millisecond * 50) // Espera un tiempo antes de enviar el siguiente dato
    }
}
```

### Canales con Buffer

Los canales pueden tener un buffer para almacenar datos temporalmente si no hay go-rutinas disponibles para procesarlos de inmediato:

```go
c := make(chan int, 100)
```

_Eventualmente el buffer puede llenarse, causando bloqueos al intentar enviar más datos._

### Uso de select

select nos permite manejar múltiples canales y especificar un comportamiento cuando los canales no están disponibles.

```go
for {
    select {
    case c <- rand.Int():
        // Datos enviados exitosamente
    default:
        // Canal está lleno, descartar el dato
        fmt.Println("dropped")
    }
    time.Sleep(time.Millisecond * 50)
}
```

**Timeout con select:**

Podemos usar time.After para implementar un timeout

```go
for {
    select {
    case c <- rand.Int():
    case <-time.After(time.Millisecond * 100):
        fmt.Println("timed out")
    }
    time.Sleep(time.Millisecond * 50)
}
```

_time.After devuelve un canal que envía un valor después del tiempo especificado. Si el canal c está bloqueado, el caso time.After se ejecutará después del timeout._
