# logging

El concepto de "logging" se refiere al proceso de registrar mensajes informativos, advertencias y errores que ocurren durante la ejecución de un programa.
En Go, el paquete estándar log proporciona funcionalidades básicas para el logging. Sin embargo, para una mayor flexibilidad y funcionalidad, es común utilizar paquetes de terceros como logrus o zap.

## Utilizando el paquete log estándar

```go
package main

import (
    "log"
    "os"
)

func main() {
    // Configuración básica del logger
    log.SetOutput(os.Stdout)
    log.SetFlags(log.Ldate | log.Ltime | log.Lshortfile)

    // Mensajes de registro
    log.Println("INFO: Este es un mensaje INFO")
    log.Println("WARNING: Este es un mensaje WARNING")
    log.Println("ERROR: Este es un mensaje ERROR")
}
```

En este ejemplo, usamos log.Println para emitir mensajes de log con prefijos para simular diferentes niveles de severidad. Sin embargo, para un manejo más sofisticado de los niveles de severidad, se recomienda utilizar una biblioteca de logging más avanzada.

## Utilizando logrus

logrus es una biblioteca popular para el logging en Go que soporta niveles de severidad, hooks, formateadores personalizados y más.

```bash
go get github.com/sirupsen/logrus
```

```go
package main

import (
    log "github.com/sirupsen/logrus"
)

func main() {
    // Configuración básica de logrus
    log.SetFormatter(&log.TextFormatter{
        FullTimestamp: true,
    })
    log.SetLevel(log.DebugLevel)

    // Mensajes de registro con diferentes niveles de severidad
    log.Debug("Este es un mensaje DEBUG")
    log.Info("Este es un mensaje INFO")
    log.Warn("Este es un mensaje WARNING")
    log.Error("Este es un mensaje ERROR")
    log.Fatal("Este es un mensaje FATAL")   // Llama a os.Exit(1) después de registrar el mensaje
    log.Panic("Este es un mensaje PANIC")   // Llama a panic() después de registrar el mensaje
}
```

## Explicación de la Configuración

_log.SetFormatter:_ Establece el formateador para los mensajes de log. TextFormatter muestra los mensajes en formato de texto legible.
_log.SetLevel:_ Establece el nivel mínimo de severidad para los mensajes de log. En este caso, es DebugLevel, lo que significa que todos los mensajes de DEBUG y niveles superiores serán registrados.
_Mensajes de log como log.Debug, log.Info, log.Warn, log.Error, log.Fatal, y log.Panic emiten mensajes con diferentes niveles de severidad._

### Ejemplo de Salida

```bash
time="2024-06-21T10:15:30Z" level=debug msg="Este es un mensaje DEBUG"
time="2024-06-21T10:15:30Z" level=info msg="Este es un mensaje INFO"
time="2024-06-21T10:15:30Z" level=warning msg="Este es un mensaje WARNING"
time="2024-06-21T10:15:30Z" level=error msg="Este es un mensaje ERROR"
time="2024-06-21T10:15:30Z" level=fatal msg="Este es un mensaje FATAL"
```

El mensaje FATAL también terminará el programa, y el mensaje PANIC (si estuviera presente) lanzará un panic.
