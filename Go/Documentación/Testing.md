# Testing: Pruebas unitarias

Go proporciona un marco de testing integrado que facilita la creación de pruebas unitarias, pruebas de integración y pruebas de aceptación. Las pruebas unitarias se utilizan para verificar el comportamiento individual de las unidades de código, como funciones o estructuras. Las pruebas de integración se utilizan para verificar la interacción entre diferentes componentes del sistema. Las pruebas de aceptación se utilizan para verificar que la aplicación cumple con los requisitos funcionales y no funcionales.

## Características del testing en Go

**Sencillo y fácil de usar:** El marco de testing de Go es intuitivo y fácil de aprender, lo que permite a los desarrolladores escribir pruebas de manera rápida y eficiente.
**Potente y flexible:** El marco de testing admite una amplia gama de aserciones y mocks, lo que permite a los desarrolladores crear pruebas completas y exhaustivas.
**Integración con el build:** Las pruebas se pueden ejecutar automáticamente como parte del proceso de compilación, lo que garantiza que el código se prueba cada vez que se realiza un cambio.

## Beneficios del testing en Go

**Mejora la calidad del código:** Las pruebas ayudan a identificar y corregir errores en el código de manera temprana, lo que reduce la cantidad de errores en producción.
**Aumenta la confianza en el código:** Las pruebas proporcionan evidencia de que el código funciona correctamente, lo que aumenta la confianza de los desarrolladores y usuarios en la aplicación.
**Facilita el mantenimiento del código:** Las pruebas ayudan a comprender mejor el código, lo que facilita su mantenimiento y actualización.

### Ejemplo de uso de testing

```go
package main

import "fmt"

func Sumar(a, b int) int {
 return a + b
}

func main() {

 resultado := Sumar(3, 4)
 fmt.Println("La suma de 3 y 4 es:", resultado)
}
```

```go
package main

import "testing"

// TestSumar verifica que la función Sumar retorne el resultado correcto.
func TestSumar(t *testing.T) {
    // Define una lista de casos de prueba con entradas a, b y el resultado esperado.
    tests := []struct {
        a, b, expected int
    }{
        {1, 1, 2},
        {2, 2, 4},
        {0, 0, 0},
        {-1, -1, -2},
        {-1, 1, 0},
    }

    // Itera sobre los casos de prueba y llama a la función Sumar con las entradas.
    for _, tt := range tests {
        result := Sumar(tt.a, tt.b)
        // Verifica si el resultado coincide con el esperado.
        if result != tt.expected {
            // Si no coincide, reporta un error con detalles del caso fallido.
            t.Errorf("Sumar(%d, %d) = %d; expected %d", tt.a, tt.b, result, tt.expected)
        }
    }
}
```

## Benchmarking en Go

El benchmarking es una técnica para medir el rendimiento de una aplicación. En Go, el paquete testing proporciona herramientas para crear benchmarks que miden el tiempo que tarda una función o bloque de código en ejecutarse.

## Características del benchmarking en Go

**Sencillo y fácil de usar:** El marco de benchmarking de Go es intuitivo y fácil de aprender, lo que permite a los desarrolladores crear benchmarks de manera rápida y eficiente.
**Potente y flexible:** El marco de benchmarking admite una amplia gama de opciones para medir el rendimiento, como el tiempo de ejecución, el uso de CPU y la memoria.
**Integración con el build:** Los benchmarks se pueden ejecutar automáticamente como parte del proceso de compilación, lo que permite a los desarrolladores monitorear el rendimiento del código a lo largo del tiempo.

## Beneficios del benchmarking en Go

**Identifica cuellos de botella de rendimiento:** Los benchmarks ayudan a identificar partes del código que son lentas o ineficientes, lo que permite optimizar el rendimiento.
**Guía la toma de decisiones**: Los datos de benchmarking pueden guiar la toma de decisiones sobre el diseño y la implementación del código.
**Asegura un rendimiento constante:** Los benchmarks ayudan a garantizar que el rendimiento de la aplicación se mantenga constante a lo largo del tiempo.

### Ejemplo de uso de benchmarking

```go
package main

import "testing"

func BenchmarkSumar(b *testing.B) {
    for i := 0; i < b.N; i++ {
        // Llama a la función Sumar repetidamente para medir su rendimiento.
        _ = Sumar(3, 7)
    }
}
```
