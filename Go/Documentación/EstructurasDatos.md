# Estructuras de datos en Go

En Go, las estructuras de datos son fundamentales para organizar y manipular datos de manera eficiente. A continuación te presento algunas de las estructuras de datos más comunes en Go y cómo puedes utilizarlas.

## Arrays

Los arrays son estructuras de tamaño fijo que almacenan elementos del mismo tipo.

```go
var arr [5]int // Array de tamaño 5

arr[0] = 10
arr[1] = 20

fmt.Println(arr) // [10 20 0 0 0]
```

## Slices

Los slices son una capa sobre los arrays que permiten una mayor flexibilidad, ya que su tamaño puede cambiar dinámicamente.

```go
slice := []int{1, 2, 3} // Crear un slice
slice = append(slice, 4) // Agregar un elemento

fmt.Println(slice) // [1 2 3 4]
```

## Maps

Los mapas son colecciones desordenadas de pares clave-valor, donde las claves deben ser únicas.

```go
m := make(map[string]int) // Crear un mapa

m["a"] = 1
m["b"] = 2

fmt.Println(m["a"]) // 1
```

## Structs

Las estructuras son colecciones de campos que pueden contener diferentes tipos de datos. Se usan comúnmente para representar entidades.

```go
type Persona struct {
    Nombre string
    Edad   int
}

p := Persona{
    Nombre: "Juan",
    Edad:   30,
}

fmt.Println(p.Nombre) // Juan
```

## Colas

Go no tiene una estructura de cola (queue) incorporada, pero puedes implementarla usando slices.

```go
type Queue []int

func (q *Queue) Enqueue(val int) {
    *q = append(*q, val)
}

func (q *Queue) Dequeue() (int, bool) {
    if len(*q) == 0 {
        return 0, false
    }
    val := (*q)[0]
    *q = (*q)[1:]
    return val, true
}

queue := Queue{}
queue.Enqueue(10)
queue.Enqueue(20)

fmt.Println(queue.Dequeue()) // 10, true
```

## Pilas

Al igual que las colas, las pilas (stacks) pueden implementarse utilizando slices.

```go
type Stack []int

func (s *Stack) Push(val int) {
    *s = append(*s, val)
}

func (s *Stack) Pop() (int, bool) {
    if len(*s) == 0 {
        return 0, false
    }
    val := (*s)[len(*s)-1]
    *s = (*s)[:len(*s)-1]
    return val, true
}

stack := Stack{}
stack.Push(10)
stack.Push(20)

fmt.Println(stack.Pop()) // 20, true
```

## Lista Enlazada

Una lista enlazada se puede crear usando structs y punteros.

```go
type Nodo struct {
    Valor int
    Siguiente *Nodo
}

func (n *Nodo) Agregar(valor int) {
    nuevoNodo := &Nodo{Valor: valor}
    actual := n
    for actual.Siguiente != nil {
        actual = actual.Siguiente
    }
    actual.Siguiente = nuevoNodo
}

nodo := &Nodo{Valor: 1}
nodo.Agregar(2)
nodo.Agregar(3)

fmt.Println(nodo.Siguiente.Valor) // 2
```

## Conjuntos

Un conjunto es una colección de elementos únicos, donde no se permiten duplicados. En muchas implementaciones de lenguajes de programación, los conjuntos no tienen un orden definido entre sus elementos.

Go no tiene un tipo de conjunto (set) incorporado, pero puedes implementarlo usando mapas.

```go
type Set map[int]bool

func (s Set) Add(val int) {
    s[val] = true
}

func (s Set) Remove(val int) {
    delete(s, val)
}

func (s Set) Contains(val int) bool {
    return s[val]
}

set := make(Set)
set.Add(1)
set.Add(2)
set.Remove(1)

fmt.Println(set.Contains(1)) // false
```

## Arboles

Un árbol es una estructura de datos jerárquica que consiste en nodos conectados por aristas. Cada nodo puede tener un número variable de nodos hijos. Un árbol no tiene ciclos, lo que significa que no hay una forma de empezar desde un nodo y volver al mismo a través de las aristas.

Los árboles binarios pueden implementarse usando structs y punteros.

```go
type NodoArbol struct {
    Valor   int
    Izquierda, Derecha *NodoArbol
}

func (n *NodoArbol) Insertar(valor int) {
    if valor < n.Valor {
        if n.Izquierda == nil {
            n.Izquierda = &NodoArbol{Valor: valor}
        } else {
            n.Izquierda.Insertar(valor)
        }
    } else {
        if n.Derecha == nil {
            n.Derecha = &NodoArbol{Valor: valor}
        } else {
            n.Derecha.Insertar(valor)
        }
    }
}

arbol := &NodoArbol{Valor: 10}
arbol.Insertar(5)
arbol.Insertar(15)
```

## Grafos

En teoría de grafos, el grado de un nodo es el número de aristas (conexiones) que tiene con otros nodos:

**Grado de un nodo en un grafo no dirigido: Es el número de aristas que inciden en ese nodo.**
**Grado de un nodo en un grafo dirigido: Se divide en:**
Grado de entrada (in-degree): Número de aristas que llegan al nodo.
Grado de salida (out-degree): Número de aristas que salen del nodo.

Go no tiene una estructura de grafos incorporada, pero se puede implementar fácilmente utilizando maps o slices de listas enlazadas para representar un grafo.

Un grafo puede ser representado como una estructura de adyacencia, donde los nodos (o vértices) son las claves, y los valores son slices que contienen los nodos conectados (aristas).

### Grafo no dirigido

```go
type Grafo map[string][]string

// Agregar una conexión (arista) entre dos nodos
func (g Grafo) AgregarArista(nodo1, nodo2 string) {
    g[nodo1] = append(g[nodo1], nodo2)
    g[nodo2] = append(g[nodo2], nodo1)
}

grafo := make(Grafo)
grafo.AgregarArista("A", "B")
grafo.AgregarArista("A", "C")
grafo.AgregarArista("B", "C")

fmt.Println(grafo) // map[A:[B C] B:[A C] C:[A B]]
```

### Grafo dirigido

```go
type GrafoDirigido map[string][]string

func (g GrafoDirigido) AgregarArista(nodo1, nodo2 string) {
    g[nodo1] = append(g[nodo1], nodo2) // Solo agregar la conexión de nodo1 a nodo2
}

grafo := make(GrafoDirigido)
grafo.AgregarArista("A", "B")
grafo.AgregarArista("A", "C")
grafo.AgregarArista("B", "C")

fmt.Println(grafo) // map[A:[B C] B:[C]]
```
