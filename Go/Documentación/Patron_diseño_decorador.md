# Patrón de diseño "decorador"

El patrón de diseño "decorador" permite añadir comportamiento a objetos individuales, ya sea de forma estática o dinámica, sin afectar el comportamiento de otros objetos del mismo tipo. Este patrón es especialmente útil cuando se necesita extender las funcionalidades de clases de una manera flexible y reusable.

## Ejemplo Genérico del Patrón Decorador

Supongamos que tenemos una interfaz Notifier que tiene un método Send para enviar notificaciones. Queremos decorar esta funcionalidad para añadir comportamiento adicional, como enviar notificaciones a través de diferentes canales (por ejemplo, correo electrónico y SMS).

**Paso 1: Definir la interfaz base:**

```go
package main

import "fmt"

// Notifier es la interfaz base
type Notifier interface {
    Send(message string)
}
```

**Paso 2: Implementar la estructura base:**

```go
// SimpleNotifier es una implementación concreta de Notifier
type SimpleNotifier struct{}

func (sn *SimpleNotifier) Send(message string) {
    fmt.Println("Sending notification:", message)
}
```

**Paso 3: Crear los decoradores:**

```go
// EmailNotifier es un decorador que añade funcionalidad de correo electrónico
type EmailNotifier struct {
    notifier Notifier
}

func (en *EmailNotifier) Send(message string) {
    en.notifier.Send(message)
    fmt.Println("Sending email with message:", message)
}

// SMSNotifier es un decorador que añade funcionalidad de SMS
type SMSNotifier struct {
    notifier Notifier
}

func (sn *SMSNotifier) Send(message string) {
    sn.notifier.Send(message)
    fmt.Println("Sending SMS with message:", message)
}
```

**Paso 4: Utilizar los decoradores:**

```go
func main() {
    // Crear un notificador simple
    notifier := &SimpleNotifier{}

    // Decorar el notificador simple con funcionalidad de correo electrónico
    emailNotifier := &EmailNotifier{notifier: notifier}

    // Decorar el notificador de correo electrónico con funcionalidad de SMS
    smsNotifier := &SMSNotifier{notifier: emailNotifier}

    // Usar el notificador decorado
    smsNotifier.Send("Hello, this is a test message!")
}
```

Este patrón permite flexibilidad al añadir o modificar comportamientos sin cambiar el código original de los objetos. Cada decorador es responsable de añadir una pequeña pieza de funcionalidad, manteniendo el código modular y fácil de mantener.
