# Capítulo 5 - Exquisiteces

## Gestión de Errores

**Mediante valores de retorno, no excepciones:**

```go
package main

import (
    "fmt"
    "os"
    "strconv"
)

func main() {
    if len(os.Args) != 2 {
        os.Exit(1)
    }
    n, err := strconv.Atoi(os.Args[1])
    if err != nil {
        fmt.Println("no es un número válido")
    } else {
        fmt.Println(n)
    }
}
```

**Puedes definir tus propios tipos de error que cumplan con la interfaz error:**

```go
import (
    "errors"
)

func process(count int) error {
    if count < 1 {
        return errors.New("Invalid count")
    }
    // ...
    return nil
}
```

**La librería estándar utiliza variables de error predefinidas, como io.EOF:**

```go
package main

import (
    "fmt"
    "io"
)

func main() {
    var input int
    _, err := fmt.Scan(&input)
    if err == io.EOF {
        fmt.Println("no more input!")
    }
}
```

## Defers

**La palabra clave defer permite posponer la ejecución de una función hasta que la función que lo envuelve haya terminado:**

```go
package main

import (
    "fmt"
    "os"
)

func main() {
    file, err := os.Open("un_fichero_que_leer")
    if err != nil {
        fmt.Println(err)
        return
    }
    defer file.Close()
    // leer el fichero
}
```

## go fmt

**El comando go fmt formatea el código según las reglas de formato de Go:**

```bash
go fmt ./...
```

## If Inicializado

**En Go, puedes inicializar una variable antes de evaluar una condición en un if:**

```go
if x := 10; count > x {
    // ...
}
```

## Interfaces Vacías y Conversiones

**La interfaz vacía interface{} permite representar cualquier tipo de dato:**

```go
func add(a interface{}, b interface{}) interface{} {
    return a.(int) + b.(int)
}

switch a.(type) {
case int:
    fmt.Printf("a es un entero y vale %d\n", a)
case bool, string:
    // ...
default:
    // ...
}
```

## Strings y Arrays de Bytes

**Conversión entre strings y arrays de bytes:**

```go
stra := "the spice must flow"
byts := []byte(stra)
strb := string(byts)
```

**Conversión entre tipos:**

```go
int64(count)
```

**Longitud de strings y caracteres Unicode:**

```go
fmt.Println(len(" ahora esto"))
```

**Iterar sobre un string usando range:**

## Funciones con Tipo

**En Go, las funciones son ciudadanos de primer nivel y tienen tipo. Por ejemplo:**

```go
type Add func(a int, b int) int
```

## Ejemplo de uso de funciones con tipo

```go
package main

import "fmt"

type Add func(a int, b int) int

func main() {
    fmt.Println(process(func(a int, b int) int {
        return a + b
    }))
}

func process(adder Add) int {
    return adder(1, 2)
}
```
