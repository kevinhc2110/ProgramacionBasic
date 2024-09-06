# Buscar en Go

En Golang, existen diferentes métodos para realizar búsquedas en distintos tipos de datos:

**Búsqueda lineal:**

Recorrer el slice elemento a elemento comparando cada uno con el valor buscado.

```go
package main

import "fmt"

func main() {
    // Slice de enteros que contiene los números a buscar
    numeros := []int{20, 500, 10, 5, 100, 1, 50}

    // Valor a buscar
    valor := 100

    // Variable para indicar si el valor se encuentra en el slice
    encontrado := false

    // Bucle `for range` que recorre el slice `numeros`
    for _, numero := range numeros {
        // Se compara cada elemento del slice con el valor a buscar
        if numero == valor {
            // Si se encuentra el valor, se establece la variable `encontrado` en `true`
            encontrado = true

            // Se utiliza `break` para salir del bucle al encontrar el valor
            break
        }
    }

    // Si la variable `encontrado` es `true`, se imprime un mensaje indicando que el valor se encontró
    if encontrado {
        fmt.Println("El valor", valor, "se encuentra en el slice")
    } else {
        // Si la variable `encontrado` es `false`, se imprime un mensaje indicando que el valor no se encontró
        fmt.Println("El valor", valor, "no se encuentra en el slice")
    }
}
```

**Búsqueda binaria:**

Utilizar un algoritmo de búsqueda binaria para encontrar un elemento en un slice ordenado.

```go
package main

import (
    "fmt"
    "sort"
)

func main() {
    // Slice de enteros
    numeros := []int{20, 500, 10, 5, 100, 1, 50}

    // Ordenar el slice antes de la búsqueda binaria
    sort.Sort(numeros)

    // Valor a buscar
    valor := 100

    // Variables para los límites de búsqueda
    izquierda := 0
    derecha := len(numeros) - 1

    // Variable para indicar si el valor se encuentra
    encontrado := false

    // Bucle de búsqueda binaria
    for izquierda <= derecha {
        // Calcular el índice del punto medio
        medio := (izquierda + derecha) / 2

        // Si el elemento del medio es el valor buscado
        if numeros[medio] == valor {
            encontrado = true
            break
        } else if numeros[medio] < valor {
            // Buscar en la mitad superior del slice
            izquierda = medio + 1
        } else {
            // Buscar en la mitad inferior del slice
            derecha = medio - 1
        }
    }

    // Imprimir el resultado de la búsqueda
    if encontrado {
        fmt.Println("El valor", valor, "se encuentra en el slice")
    } else {
        fmt.Println("El valor", valor, "no se encuentra en el slice")
    }
}
```

**Búsqueda en mapas:**

Utilizar la clave para obtener el valor asociado en un mapa.

```go
package main

import "fmt"

func main() {
    // Mapa de string a string que representa países y sus capitales
    paises := map[string]string{
        "Colombia": "Bogotá",
        "Argentina": "Buenos Aires",
        "Chile": "Santiago",
    }

    // Clave a buscar (nombre del país)
    pais := "Chile"

    // Buscar la capital correspondiente al país en el mapa
    capital, encontrado := paises[pais]

    // Verificar si se encontró la capital
    if encontrado {
        fmt.Println("La capital de", pais, "es", capital)
    } else {
        fmt.Println("El país", pais, "no se encuentra en el mapa")
    }
}
```

**Búsqueda en cadenas de texto:**

_Subcadenas:_ Buscar la ocurrencia de una subcadena dentro de una cadena de texto.

```go
package main

import (
    "fmt"
    "strings"
)

func main() {
    // Cadena de texto a analizar
    texto := "Hola, mundo! Este es un mensaje más largo para probar la búsqueda de subcadenas."

    // Array de subcadenas a buscar
    subcadenas := []string{
        "mundo",
        "Hola",
        "mensaje",
        "no existe",
    }

    // Recorrer las subcadenas del array
    for _, subcadena := range subcadenas {
        // Buscar la subcadena en el texto utilizando la función `strings.Contains`
        if strings.Contains(texto, subcadena) {
            // Si se encuentra la subcadena, imprimir un mensaje indicando que sí está presente
            fmt.Println("La subcadena", subcadena, "se encuentra en el texto")
        } else {
            // Si no se encuentra la subcadena, imprimir un mensaje indicando que no está presente
            fmt.Println("La subcadena", subcadena, "no se encuentra en el texto")
        }
    }
}
```

**Búsqueda en estructuras:**

_Búsqueda por campos:_ Buscar un elemento en una estructura comparando sus campos.

```go
package main

import "fmt"

type Persona struct {
    Nombre string
    Edad   int
}

func main() {
    // Slice de personas que contiene objetos de tipo Persona
    personas := []Persona{
        {"Juan", 30},
        {"Maria", 25},
        {"Pedro", 40},
    }

    // Persona a buscar
    personaABuscar := Persona{Nombre: "Pedro", Edad: 40}

    // Variable para indicar si la persona se encuentra en el slice
    encontrado := false

    // Bucle `for range` para recorrer el slice `personas`
    for _, persona := range personas {
        // Comparar la persona actual del slice con la persona a buscar
        if persona == personaABuscar {
            // Si se encuentra la persona, establecer `encontrado` en `true`
            encontrado = true

            // Salir del bucle con la instrucción `break`
            break
        }
    }

    // Imprimir el resultado de la búsqueda
    if encontrado {
        fmt.Println("La persona", personaABuscar, "se encuentra en el slice")
    } else {
        fmt.Println("La persona", personaABuscar, "no se encuentra en el slice")
    }
}
```

**Búsqueda en archivos:**

_Leer y buscar en archivos:_ Leer el contenido de un archivo y buscar un patrón específico.

```go
package main

import (
    "bufio"
    "fmt"
    "os"
    "strings"
)

func main() {
    // Archivo a leer
    archivo := "archivo.txt"

    // Patrón a buscar
    patron := "palabraABuscar"

    // Variable para indicar si el patrón se encuentra
    encontrado := false

    // Abrir el archivo
    f, err := os.Open(archivo)
    if err != nil {
        fmt.Println("Error al abrir el archivo:", err)
        return
    }
    defer f.Close() // Cerrar el archivo al finalizar la función

    // Crear un escáner para leer el archivo línea por línea
    scanner := bufio.NewScanner(f)

    // Recorrer el archivo línea por línea
    for scanner.Scan() {
        // Obtener la línea actual
        linea := scanner.Text()

        // Buscar el patrón en la línea actual
        if strings.Contains(linea, patron) {
            // Si se encuentra el patrón:
            encontrado = true
            fmt.Println("La línea:", linea, "contiene el patrón", patron)
            break // Salir del bucle si se encuentra el patrón
        }
    }

    // Verificar si hubo errores al leer el archivo
    if err := scanner.Err(); err != nil {
        fmt.Println("Error al leer el archivo:", err)
        return
    }

    // Imprimir el resultado de la búsqueda
    if encontrado {
        fmt.Println("El patrón", patron, "se encontró en el archivo")
    } else {
        fmt.Println("El patrón", patron, "no se encontró en el archivo")
    }
}
```

**Búsqueda en bases de datos:**

_Conexiones a bases de datos:_ Utilizar paquetes como database/sql para conectarse a bases de datos y realizar consultas.

```go
package main

import (
    "database/sql"
    "fmt"
    "log"
)

func main() {
    // Conexión a la base de datos
    dsn := "usuario:contraseña@tcp(localhost:3306)/nombreBD" // Data Source Name
    db, err := sql.Open("mysql", dsn)
    if err != nil {
        log.Fatal(err)
    }
    defer db.Close()

    // Consulta SQL con LIKE para búsqueda parcial
    consulta := "SELECT * FROM productos WHERE nombre LIKE '%productoABuscar%'"

    // Preparar la consulta para evitar inyección SQL
    stmt, err := db.Prepare(consulta)
    if err != nil {
        log.Fatal(err)
    }
    defer stmt.Close()

    // Ejecutar la consulta
    rows, err := stmt.Query()
    if err != nil {
        log.Fatal(err)
    }
    defer rows.Close()

    // Recorrer los resultados
    for rows.Next() {
        var id int
        var nombre string
        var precio float64

        // Escanear los resultados de la fila actual
        err := rows.Scan(&id, &nombre, &precio)
        if err != nil {
            log.Fatal(err)
        }

        // Imprimir los datos del producto
        fmt.Println("ID:", id, "Nombre:", nombre, "Precio:", precio)
    }

    // Verificar errores al final de la lectura
    if err := rows.Err(); err != nil {
        log.Fatal(err)
    }
}
```
