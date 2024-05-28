# Pilas y colas en Go: Estructuras de datos esenciales

Las pilas y colas son estructuras de datos fundamentales en la programación, utilizadas para organizar y procesar elementos de manera eficiente. Go proporciona herramientas para implementarlas y aprovechar sus beneficios en tus aplicaciones.

## Pilas (LIFO)

**Concepto:** Las pilas siguen el principio Last In, First Out (LIFO), donde el último elemento agregado es el primero en ser eliminado.
**Operaciones básicas:**
_push(elemento): Agrega un elemento a la pila._
_pop(): Elimina y devuelve el último elemento agregado._
_top(): Devuelve el último elemento agregado sin eliminarlo._
_empty(): Indica si la pila está vacía._
**Aplicaciones:**
_Deshacer/Rehacer acciones en editores de texto._
_Evaluación de expresiones matemáticas._
_Implementación de algoritmos de retroceso._

### Ejemplo de Pilas

```go
package main

import "fmt"

// Definición de la estructura Stack

type Stack []string

// Función para añadir un elemento a la pila (push)

func (stack *Stack) Push(val string) {
 *stack = append(*stack, val)
}

// Función para eliminar y devolver el elemento superior de la pila (pop)

func (stack *Stack) Pop() string {
 if len(*stack) == 0 {
  panic("La pila está vacía")
 }
 top := (*stack)[len(*stack)-1]
 *stack = (*stack)[:len(*stack)-1]
 return top
}

// Mas métodos utilizados

// Peek devuelve el elemento superior de la pila sin eliminarlo

func (stack *Stack) Peek() string {
 if len(*stack) == 0 {
  return ""
 }
 return (*stack)[len(*stack)-1]
}

// IsEmpty verifica si la pila está vacía

func (stack *Stack) IsEmpty() bool {
 return len(*stack) == 0
}

// Size devuelve el tamaño de la pila

func (stack *Stack) Size() int {
 return len(*stack)
}

// Clear elimina todos los elementos de la pila

func (stack *Stack) Clear() {
 *stack = Stack{}
}

// Contains verifica si un elemento está presente en la pila

func (stack *Stack) Contains(page string) bool {
 for _, item := range *stack {
  if item == page {
   return true
  }
 }
 return false
}

// Copy crea una copia de la pila

func (stack *Stack) Copy() Stack {
 copyStack := make(Stack, len(*stack))
 copy(copyStack, *stack)
 return copyStack
}

// Reverse invierte el orden de los elementos en la pila

func (stack *Stack) Reverse() {
 for i, j := 0, len(*stack)-1; i < j; i, j = i+1, j-1 {
  (*stack)[i], (*stack)[j] = (*stack)[j], (*stack)[i]
 }
}

// Search devuelve la posición de un elemento en la pila (0-indexed desde el top)

func (stack *Stack) Search(page string) int {
 for i := len(*stack) - 1; i >= 0; i-- {
  if (*stack)[i] == page {
   return len(*stack) - 1 - i
  }
 }
 return -1
}

// Método para obtener el último elemento de la pila sin eliminarlo

func (stack *Stack) Top() string {
 if len(*stack) == 0 {
   return "" // Manejar pila vacía
 }

 return (*stack)[len(*stack)-1]
}


func main() {

 // Crear una pila vacía

 var pila Stack

 // Añadir elementos a la pila

 pila.Push("Perro")
 pila.Push("Gato")
 pila.Push("Conejo")

 // Eliminar y mostrar los elementos de la pila

 for len(pila) > 0 {
  fmt.Println("Elemento extraído:", pila.Pop())
 }
}
```

## Colas (FIFO)

**Concepto:** Las colas siguen el principio First In, First Out (FIFO), donde el primer elemento agregado es el primero en ser eliminado.
**Operaciones básicas:**
_enqueue(elemento): Agrega un elemento a la cola._
_dequeue(): Elimina y devuelve el primer elemento agregado._
_front(): Devuelve el primer elemento agregado sin eliminarlo._
_empty(): Indica si la cola está vacía._
**Aplicaciones:**
_Sistemas de gestión de colas (por ejemplo, atención al cliente)._
_Algoritmos de planificación de tareas._
_Buffering de datos en redes._

### Ejemplo de Colas

```go
package main

import "fmt"

// Definición de cola

type Queue []string

// Función para añadir un elemento a la cola (enqueue)

func (queue *Queue) Enqueue(val string) {
 *queue = append(*queue, val)
}

// Función para eliminar y devolver el primer elemento de la cola (dequeue)

func (queue *Queue) Dequeue() string {
 if len(*queue) == 0 {
  panic("La cola está vacía")
 }
 first := (*queue)[0]
 *queue = (*queue)[1:]
 return first
}

// Mas métodos utilizados

// Peek devuelve el elemento al frente de la cola sin eliminarlo

func (queue *Queue) Peek() string {
 if len(*queue) == 0 {
  return ""
 }
 return (*queue)[0]
}

// IsEmpty verifica si la cola está vacía

func (queue *Queue) IsEmpty() bool {
 return len(*queue) == 0
}

// Size devuelve el tamaño de la cola

func (queue *Queue) Size() int {
 return len(*queue)
}

// Clear elimina todos los elementos de la cola

func (queue *Queue) Clear() {
 *queue = Queue{}
}

// Contains verifica si un elemento está presente en la cola

func (queue *Queue) Contains(element string) bool {
 for _, item := range *queue {
  if item == element {
   return true
  }
 }
 return false
}

// Copy crea una copia de la cola

func (queue *Queue) Copy() Queue {
 copyQueue := make(Queue, len(*queue))
 copy(copyQueue, *queue)
 return copyQueue
}

// Reverse invierte el orden de los elementos en la cola

func (queue *Queue) Reverse() {
 for i, j := 0, len(*queue)-1; i < j; i, j = i+1, j-1 {
  (*queue)[i], (*queue)[j] = (*queue)[j], (*queue)[i]
 }
}

// Search devuelve la posición de un elemento en la cola (0-indexed desde el front)

func (queue *Queue) Search(element string) int {
 for i, item := range *queue {
  if item == element {
   return i
  }
 }
 return -1
}

// Método para obtener el primer elemento de la cola sin eliminarlo

func (queue *Queue) Front() string {
 if len(*queue) == 0 {
   return "" // Handle empty queue
 }

 return (*queue)[0]
}

func main() {

 // Crear una cola vacía

 var cola Queue

 // Añadir elementos a la cola

 cola.Enqueue("Perro")
 cola.Enqueue("Gato")
 cola.Enqueue("Conejo")

 // Eliminar y mostrar los elementos de la cola

 for len(cola) > 0 {
  fmt.Println("Elemento extraído:", cola.Dequeue())
 }
}
```
