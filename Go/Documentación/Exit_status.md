# Estado de salida (Exit Status) en Go

En Go, el estado de salida se utiliza principalmente para indicar el éxito o el fracaso de la ejecución de un programa al sistema operativo o a otros programas que puedan llamarlo. Sirve como una forma de comunicar el resultado del programa al entorno externo.

**os.Exit(0): Indica la terminación exitosa del programa.**
**os.Exit(código): Donde código es cualquier entero distinto de cero, significa una terminación anormal.**

## ¿Cuándo se utiliza el estado de salida en Go?

**Indicar la terminación exitosa.**
**Informar de errores y terminaciones anormales.**
**Diferenciar tipos de errores.**
**Integración con la automatización y los scripts.**

### Ejemplo de uso del estado de salida

```go
package main

import (
    "fmt"
    "os"
)

func main() {
    // Simular un escenario de error (archivo no encontrado)
    if _, err := os.Open("missing_file.txt"); err != nil {
        fmt.Println("Error:", err)
        os.Exit(1)  // Indicar error saliendo con código distinto de cero
    }

    fmt.Println("Archivo procesado correctamente")
    os.Exit(0)  // Indicar ejecución exitosa
}
```

### **Se puede usar con el Manejo de Errores**

_Usando `echo $?` podemos ver el ultimo código de status_
