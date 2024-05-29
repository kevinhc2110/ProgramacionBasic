# Capítulo 1: Introducción y Fundamentos en Go

## Ejecución de un Programa

**Ejecutar programa con fichero temporal:**

```bash
go run main.go
```

**Compilar explícitamente (generar binario):**

```bash
go build main.go
```

**inicializar un módulo Go:**

```bash
go mod init
```

## Declaración de Variables

**Declaración de una variable con var:**

```go
var power int = 9000
```

**Declaración e inicialización de una variable con :=:**

```go
power := 9000
```

**Uso de variables en funciones:**

```go
power := getPower()

func getPower() int {
    return 9001
}
```

## Funciones en Go

**Función sin retorno:**

```go
func log(message string) {
    // código de la función
}
```

**Función con retorno:**

```go
func add(a int, b int) int {
    return a + b
}
```

**Función con dos retornos:**

```go
func power(name string) (int, bool) {
    // código de la función
}
```

**Ejemplo de uso de funciones con múltiples retornos:**

```go
func funciones() {
    value, exists := power("goku")
    if !exists {
        // manejar esta situación de error
    }

    // O en el caso que solo estemos interesados en uno de los retornos
    _, exists := power("goku")
    if !exists {
        // manejar esta situación de error
    }
}
```
