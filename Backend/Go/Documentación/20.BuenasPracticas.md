# 20. Buenas Prácticas y Principios de Programación en Go

## 20.1. Principio DRY (Don’t Repeat Yourself)

En Go, se debe evitar la duplicación de código manteniendo funciones reutilizables y módulos bien definidos. Esto mejora la mantenibilidad y reduce la probabilidad de errores.

```go
func calculateSum(a, b int) int {
  return a + b
}

result := calculateSum(5, 10)

```

---

## 20.2. KISS (Keep It Simple, Stupid)

El lenguaje Go, por diseño, promueve la simplicidad. Mantener el código limpio y evitar la sobrecomplicación es una práctica esencial. Estructuras simples y el uso de funciones cortas y claras son claves.

```go
package main

import (
    "fmt"
    "net/http"
)

func handler(w http.ResponseWriter, r *http.Request) {
    fmt.Fprintf(w, "Hello, World!")
}

func main() {
    http.HandleFunc("/", handler)
    http.ListenAndServe(":8080", nil)
}

```

---

## 20.3. Principios SOLID

Aunque Go no es puramente orientado a objetos, muchos de estos principios pueden aplicarse para mantener un código bien estructurado.

- **Single Responsibility:** Cada función, paquete o estructura en Go debería tener una única responsabilidad.
- **Open/Closed:** El código debe estar abierto a extensiones, pero cerrado a modificaciones. Se puede lograr extendiendo comportamientos a través de interfaces.
- **Liskov Substitution:** Las estructuras que implementen interfaces deben poder ser reemplazadas sin alterar el comportamiento esperado del programa.
- **Interface Segregation:** En Go, es preferible definir interfaces pequeñas y específicas en lugar de interfaces grandes y genéricas.
- **Dependency Inversion:** Los componentes de alto nivel no deben depender de los de bajo nivel. En Go, esto se implementa utilizando interfaces para inyectar dependencias.

  - **Ejemplo en Go utilizando el principio de Dependency Inversion con interfaces:**

    ```go
    type Notifier interface {
        SendNotification(message string) error
    }

    type EmailNotifier struct{}

    func (e EmailNotifier) SendNotification(message string) error {
        fmt.Println("Sending email:", message)
        return nil
    }

    func notifyUser(n Notifier, message string) {
        n.SendNotification(message)
    }

    func main() {
        notifier := EmailNotifier{}
        notifyUser(notifier, "Hello, Go!")
    }

    ```

---

## Refactorización

Refactorizar en Go implica reestructurar el código para mejorar su legibilidad, eficiencia y reducir la complejidad sin cambiar su funcionalidad. Esto puede implicar dividir funciones largas, renombrar variables para mayor claridad, o extraer funciones reutilizables.

- **Técnicas:** Renombrar variables, extraer funciones, simplificar expresiones, eliminar código duplicado, modularizar componentes, y reducir la complejidad ciclomática.

---

## Documentación

Go fomenta la creación de comentarios útiles antes de funciones y estructuras para generar documentación automáticamente con herramientas como godoc. Los comentarios deben ser concisos y explicar claramente la función del código.

- **Tipos:** Comentarios en el código, documentación de funciones, tipos y paquetes, así como documentación general del proyecto (README, documentación autogenerada con godoc).

  ```go
  // calculateSum returns the sum of two integers.
  func calculateSum(a, b int) int {
      return a + b
  }

  ```

---

## Otras Buenas Practicas

- ### Pruebas Unitarias

  - **Objetivo:** Verificar que cada parte del código funcione correctamente de forma aislada.
  - **Beneficios:** Facilita el mantenimiento y la refactorización, detecta errores tempranos y asegura la estabilidad del código.

    ```go
    func TestCalculateSum(t *testing.T) {
        result := calculateSum(5)
        expected := 10
        if result != expected {
            t.Errorf("calculateSum(5) = %d; expected %d", result, expected)
        }
    }

    ```

- ### Code Review

  - **Objetivo:** Realizar revisiones colaborativas del código para identificar posibles errores, mejorar la calidad del código y mantener un estilo de codificación consistente.
    En Go, se recomienda realizar code reviews antes de fusionar cambios en ramas principales, utilizando herramientas como GitHub, GitLab o Gerrit.

- ### Versionamiento

  - **Objetivo:** Controlar los cambios en el código, rastrear versiones y facilitar la colaboración.
  - **Herramientas:** Git es la más comúnmente utilizada, y Go promueve la modularización del código con el uso de go.mod para gestionar dependencias y versiones.

- **Ejemplo de go.mod:**

  ```go
  module github.com/user/project

  go 1.20

  require github.com/some/package v1.2.3

  ```

---

## Otras Consideraciones

- ### Legibilidad

  Utiliza nombres de variables y funciones descriptivos, indenta correctamente el código y sigue las convenciones establecidas por la comunidad de Go, como el uso de gofmt para formatear el código y golint para seguir las mejores prácticas de estilo.

- ### Eficiencia

  Go está diseñado para ser eficiente en el uso de memoria y CPU. Es recomendable evitar asignaciones innecesarias de memoria y utilizar concurrencia (goroutines) cuando sea adecuado.

- ### Mantenibilidad

  El código debe ser modular y fácil de extender. Los paquetes bien definidos y el uso de interfaces son fundamentales en Go para garantizar la mantenibilidad del software a largo plazo.

- ### Seguridad

  Protege tu aplicación de vulnerabilidades comunes como inyección SQL, ataques de Cross-Site Scripting (XSS) y Cross-Site Request Forgery (CSRF). Go tiene herramientas integradas como html/template para evitar XSS, y paquetes como crypto para cifrado y autenticación.
