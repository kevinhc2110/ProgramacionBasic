# Control de flujo

_break:_ Sale del bucle más interno.
_continue:_ Salta a la siguiente iteración del bucle.
_return:_ Sale de la función actual.
_goto:_ Aunque existe, su uso es altamente desaconsejado debido a la dificultad en seguir el flujo del programa.

```go
package main

import "fmt"

func main() {
    // Condicionales
    x := 15
    if x > 10 {
        fmt.Println("x es mayor que 10")
    }

    // Bucles
    for i := 0; i < 5; i++ {
        if i == 3 {
            break
        }
        fmt.Println(i)
    }

    // Switch
    switch day := "Sunday"; day {
    case "Saturday", "Sunday":
        fmt.Println("Weekend")
    default:
        fmt.Println("Weekday")
    }
}
```
