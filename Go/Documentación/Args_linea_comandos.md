# Argumentos de la línea de comandos

Los argumentos de la línea de comandos en Go son valores que se pasan a un programa cuando se ejecuta. Se pueden utilizar para proporcionar información al programa sobre cómo debe ejecutarse o para especificar opciones y configuraciones. En Go, se pueden manejar de manera eficiente usando el paquete flag y el paquete os.

## Usando el paquete flag

El paquete flag es una manera sencilla de definir y parsear los argumentos de la línea de comandos.

```go
package main

import (
 "flag"
 "fmt"
)

func main() {
 // Definir los flags
 name := flag.String("name", "World", "a name to say hello to")
 age := flag.Int("age", 0, "your age")

 // Parsear los flags
 flag.Parse()

 // Imprimir los valores de los flags
 fmt.Printf("Hello, %s!\n", *name)
 fmt.Printf("You are %d years old.\n", *age)

 // Imprimir los argumentos restantes
 fmt.Println("Remaining arguments:", flag.Args())
}
```

**Compilación y ejecución:**

```Bash
go build -o myprogram
./myprogram -name=Alice -age=30
```

**Salida esperada:**

```Bash
Hello, Alice!
You are 30 years old.
Remaining arguments: []
```

## Usando el paquete os

El paquete os proporciona acceso a las variables de entorno y a los argumentos de la línea de comandos. Es más adecuado para situaciones donde no se necesita una sintaxis de flags.

```go
package main

import (
 "fmt"
 "os"
)

func main() {
 // Obtener todos los argumentos de la línea de comandos
 args := os.Args

 // El primer argumento es el nombre del programa
 programName := args[0]
 fmt.Println("Program name:", programName)

 // Los siguientes argumentos son los argumentos de la línea de comandos
 for i, arg := range args[1:] {
  fmt.Printf("Argument %d: %s\n", i+1, arg)
 }
}
```

**Compilación y ejecución:**

```bash
go build -o myprogram
./myprogram arg1 arg2 arg3
```

**Salida esperada:**

```bash
Program name: ./myprogram
Argument 1: arg1
Argument 2: arg2
Argument 3: arg3
```
