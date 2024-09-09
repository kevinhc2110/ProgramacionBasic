# El Principio de Abierto-Cerrado (Open-Close Principle, OCP)

El Principio de Abierto-Cerrado establece que una entidad (como una clase, módulo o función) debe estar abierta para extensión, pero cerrada para modificación. Esto significa que el comportamiento de una entidad debe poder ser extendido sin modificar su código fuente original.

## Ejemplo Incorrecto

```go
package main

import "fmt"

// PaymentProcessor procesa pagos
type PaymentProcessor struct{}

func (p *PaymentProcessor) ProcessPayment(method string, amount float64) {
 if method == "credit_card" {
  fmt.Println("Processing credit card payment of", amount)
 } else if method == "paypal" {
  fmt.Println("Processing PayPal payment of", amount)
 } else {
  fmt.Println("Unknown payment method")
 }
}

func main() {
 processor := &PaymentProcessor{}
 processor.ProcessPayment("credit_card", 100.0)
 processor.ProcessPayment("paypal", 50.0)
}
```

**Problema del Ejemplo Incorrecto:**

En este ejemplo, cada vez que se añade un nuevo método de pago, se debe modificar la clase PaymentProcessor. Esto viola el principio de abierto-cerrado, ya que la clase no está cerrada para modificaciones.

## Ejemplo Correcto

Ahora, veamos cómo podemos cumplir con el OCP utilizando interfaces y polimorfismo. Aquí, en lugar de modificar la clase PaymentProcessor, añadimos nuevas implementaciones de una interfaz PaymentMethod.

```go
package main

import "fmt"

// PaymentMethod define una interfaz para métodos de pago
type PaymentMethod interface {
 Process(amount float64)
}

// CreditCardPayment implementa el método de pago con tarjeta de crédito
type CreditCardPayment struct{}

func (c *CreditCardPayment) Process(amount float64) {
 fmt.Println("Processing credit card payment of", amount)
}

// PayPalPayment implementa el método de pago con PayPal
type PayPalPayment struct{}

func (p *PayPalPayment) Process(amount float64) {
 fmt.Println("Processing PayPal payment of", amount)
}

// PaymentProcessor procesa pagos utilizando el método de pago
type PaymentProcessor struct{}

func (p *PaymentProcessor) ProcessPayment(method PaymentMethod, amount float64) {
 method.Process(amount)
}

func main() {
 processor := &PaymentProcessor{}

 creditCard := &CreditCardPayment{}
 paypal := &PayPalPayment{}

 processor.ProcessPayment(creditCard, 100.0)
 processor.ProcessPayment(paypal, 50.0)
}
```

En este ejemplo, la clase PaymentProcessor no necesita ser modificada para soportar nuevos métodos de pago. En su lugar, podemos añadir nuevas implementaciones de la interfaz PaymentMethod sin cambiar el código existente de PaymentProcessor, cumpliendo así con el principio de abierto-cerrado.
