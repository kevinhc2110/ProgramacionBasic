# Capítulo 5 - Exquisiteces

## Gestión de Errores

**La gestión de errores en Go se realiza mediante valores de retorno, no excepciones. Por ejemplo, la función strconv.Atoi convierte un string a entero:**

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

```go
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

Las interfaces vacías se utilizan con frecuencia para manipular datos de tipos desconocidos. Aunque puede no ser la forma más limpia de escribir código, a veces es la única opción en lenguajes estáticos.

## Strings y Arrays de Bytes

**Los strings y los arrays de bytes están estrechamente relacionados en Go, y podemos convertir entre ellos fácilmente:**

```go
stra := "the spice must flow"
byts := []byte(stra)
strb := string(byts)
```

De hecho, este tipo de conversión es común entre otros tipos también. Por ejemplo, algunas funciones esperan explícitamente un int32 o un int64, o sus homólogos sin signo. Por lo tanto, es posible que te encuentres haciendo conversiones como esta:

```go
int64(count)
```

Es algo que probablemente acabes haciendo con frecuencia cuando utilices bytes y strings. Es importante tener en cuenta que cuando utilizas []byte(X) o string(X), se realiza una copia de los datos. Esto es necesario ya que los strings son inmutables.

Los strings están compuestos de runas, que son letras Unicode. Por lo tanto, si intentas recuperar la longitud de un string, es posible que no obtengas el valor que esperas. Por ejemplo, el siguiente código imprimirá 3:

```go
fmt.Println(len(" ahora esto"))
```

Esto se debe a que el string contiene caracteres Unicode, y la función len cuenta el número de bytes en el string, no el número de caracteres. Cada carácter Unicode puede ocupar más de un byte en memoria.

Si iteras sobre un string utilizando range, obtendrás las runas en lugar de los bytes. Sin embargo, cuando conviertes un string en un []byte, obtienes los datos correctos.

## Funciones con Tipo

**En Go, las funciones son ciudadanos de primer nivel y tienen tipo. Por ejemplo:**

```go
type Add func(a int, b int) int
```

Esto significa que las funciones pueden ser utilizadas en cualquier lugar, como tipo de un campo, como parámetro o como valor de retorno. Por ejemplo:

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

El uso de funciones como esta puede ayudar a desacoplar el código de implementaciones específicas, al igual que lo hacemos con los interfaces.
