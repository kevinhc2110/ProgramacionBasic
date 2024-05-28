# Excepciones en Go: Manejo de errores y recuperación de pánico

En Go, las excepciones no forman parte del diseño central del lenguaje. En cambio, Go utiliza una combinación de mecanismos de manejo de errores y recuperación de pánico para gestionar situaciones inesperadas y mantener la estabilidad del programa.

## La interfaz error

En Go, la interfaz error es una forma estándar de representar un error. La interfaz se define de la siguiente manera:

```go
type error interface {
    Error() string
}
```

Cualquier tipo que implemente el método Error() string se considera un error. La función errors.New y el paquete fmt son dos maneras comunes de crear errores.

## Creación de Errores

**Usando errors.New:**

```go
import "errors"

func ejemplo() error {
    return errors.New("este es un error")
}
```

**Usando fmt.Errorf:**

```go
import "fmt"

func ejemplo() error {
    return fmt.Errorf("este es un error: %d", 404)
}
```

## Manejo de Errores

Los errores en Go se manejan verificando el valor de retorno de las funciones. Aquí hay un ejemplo típico:

```go
package main

import (
    "errors"
    "fmt"
)

func dividir(a, b float64) (float64, error) {
    if b == 0 {
        return 0, errors.New("no se puede dividir por cero")
    }
    return a / b, nil
}

func main() {
    resultado, err := dividir(4, 0)
    if err != nil {
        fmt.Println("Error:", err)
        return
    }
    fmt.Println("Resultado:", resultado)
}
```

## Error Wrapping y Unwrapping

Go 1.13 introdujo la capacidad de envolver y descomponer errores usando el paquete errors.

**Envolviendo Errores:**

```go
import "fmt"

func ejemplo() error {
    return fmt.Errorf("error original: %w", errors.New("este es un error"))
}
```

**Descomponiendo Errores:**

```go
import (
    "errors"
    "fmt"
)

func ejemplo() error {
    return fmt.Errorf("error original: %w", errors.New("este es un error"))
}

func main() {
    err := ejemplo()
    var e *error
    if errors.As(err, &e) {
        fmt.Println("Error:", e)
    }
}
```

## Uso de defer, panic, y recover

Aunque no es el mecanismo principal para manejar errores, Go también tiene panic y recover para manejar situaciones excepcionales:

**Defer:** Pospone la ejecución de una función hasta que la función que la contiene haya terminado
**panic:** Se utiliza para situaciones inesperadas y críticas
**recover:** Se utiliza para recuperar un programa de un estado de pánico.

```go
package main

import (
    "fmt"
)

func causarPanico() {
    defer func() {
        if r := recover(); r != nil {
            fmt.Println("Recuperado del pánico:", r)
        }
    }()
    fmt.Println("A punto de entrar en pánico")
    panic("¡algo salió terriblemente mal!")
    fmt.Println("Esto no se imprimirá")
}

func main() {
    causarPanico()
    fmt.Println("El programa continúa")
}
```

En este ejemplo, panic interrumpe el flujo normal del programa y recover permite capturar y manejar el pánico, permitiendo que el programa continúe su ejecución.
