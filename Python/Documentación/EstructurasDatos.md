# Estructuras de datos

## Arreglos (arrays)

**Unidimensionales:** Se pueden implementar utilizando listas de Python.

```py
array = [1, 2, 3, 4, 5]
```

_Multidimensionales:_ También con listas, pero anidadas.

```py
array_2d = [[1, 2, 3], [4, 5, 6], [7, 8, 9]]
```

**Listas dinámicas:** Las listas de Python ya son dinámicas, puedes agregar o eliminar elementos fácilmente.

```py
lista = [1, 2, 3]
lista.append(4)  # Agrega un elemento
lista.remove(2)  # Elimina un elemento
```

## Listas enlazadas

**Lista enlazada simple:**

```py
class Nodo:
    def __init__(self, data=None):
        self.data = data
        self.next = None

class ListaEnlazada:
    def __init__(self):
        self.head = None

    def agregar(self, data):
        nuevo_nodo = Nodo(data)
        nuevo_nodo.next = self.head
        self.head = nuevo_nodo
```

**Lista doblemente enlazada:**

```py
class Nodo:
    def __init__(self, data=None):
        self.data = data
        self.prev = None
        self.next = None

class ListaDoble:
    def __init__(self):
        self.head = None

    def agregar(self, data):
        nuevo_nodo = Nodo(data)
        nuevo_nodo.next = self.head
        if self.head is not None:
            self.head.prev = nuevo_nodo
        self.head = nuevo_nodo
```

**Lista circular:**

```py
class Nodo:
    def __init__(self, data=None):
        self.data = data
        self.next = None

class ListaCircular:
    def __init__(self):
        self.head = None

    def agregar(self, data):
        nuevo_nodo = Nodo(data)
        if not self.head:
            self.head = nuevo_nodo
            self.head.next = self.head
        else:
            temp = self.head
            while temp.next != self.head:
                temp = temp.next
            temp.next = nuevo_nodo
            nuevo_nodo.next = self.head
```

## Tuplas

Las tuplas en Python son estructuras inmutables que permiten almacenar una secuencia de elementos. Son similares a las listas, pero una vez creadas, no se pueden modificar.

```py
# Definir una tupla
tupla = (1, 2, 3)

# Acceder a un elemento
elemento = tupla[0]

# Intentar modificar una tupla dará error
# tupla[0] = 4  # Esto generaría un error
```

## Pilas (stacks)

Implementación con listas:

```py
pila = []
pila.append(1)  # Push
pila.append(2)
pila.pop()  # Pop
```

## Colas (queues)

**Colas simples:** Usando collections.deque.

```py
from collections import deque

cola = deque()
cola.append(1)  # Enqueue
cola.popleft()  # Dequeue
```

**Colas dobles (deque):**

```py
from collections import deque

deque_doble = deque()
deque_doble.append(1)        # Agrega al final
deque_doble.appendleft(2)    # Agrega al inicio
deque_doble.pop()            # Elimina del final
deque_doble.popleft()        # Elimina del inicio
```

**Colas de prioridad:** Usando heapq.

```py
import heapq

cola_prioridad = []
heapq.heappush(cola_prioridad, (1, 'tarea 1'))
heapq.heappush(cola_prioridad, (3, 'tarea 3'))
heapq.heappush(cola_prioridad, (2, 'tarea 2'))
tarea = heapq.heappop(cola_prioridad)
```

## Conjuntos (sets)

**Conjuntos matemáticos:**

```py
conjunto = {1, 2, 3}
conjunto.add(4)
conjunto.remove(2)
```

## Diccionarios o mapas (hashmaps)

Implementación de tablas hash con diccionarios nativos:

```py
diccionario = {'clave1': 'valor1', 'clave2': 'valor2'}
diccionario['clave3'] = 'valor3'
valor = diccionario['clave1']
```

## Colecciones (collections)

El módulo collections en Python ofrece varias estructuras de datos adicionales que extienden las funcionalidades de las estructuras básicas como listas, diccionarios y conjuntos. Algunas de las más comunes son:

**namedtuple:** Similar a una tupla, pero los campos tienen nombres, lo que hace el código más legible.

```py
from collections import namedtuple

Punto = namedtuple('Punto', ['x', 'y'])
p = Punto(2, 3)
print(p.x, p.y)  # Salida: 2 3
```

**deque (double-ended queue):** Es una cola de doble extremo que permite insertar y eliminar elementos por ambos extremos de forma eficiente.

```py
from collections import deque

d = deque([1, 2, 3])
d.append(4)         # Agrega al final
d.appendleft(0)     # Agrega al inicio
d.pop()             # Elimina del final
d.popleft()         # Elimina del inicio
```

**Counter:** Una subclase de diccionario que cuenta la frecuencia de los elementos.

```py
from collections import Counter

conteo = Counter('abracadabra')
print(conteo)  # Salida: Counter({'a': 5, 'b': 2, 'r': 2, 'c': 1, 'd': 1})
```

**defaultdict:** Similar a un diccionario normal, pero proporciona un valor predeterminado si una clave no existe.

```py
from collections import defaultdict

d = defaultdict(int)
d['a'] += 1
print(d)  # Salida: defaultdict(<class 'int'>, {'a': 1})
```

## Casting

El casting en Python se refiere a convertir un tipo de datos en otro. Python proporciona funciones integradas para hacer conversiones.

**Convertir a entero:**

```py
num = int("10") # Convierte la cadena "10" a un entero

```

**Convertir a flotante:**

```py
flotante = float("3.14") # Convierte la cadena "3.14" a un número flotante
```

**Convertir a cadena:**

```py
cadena = str(100) # Convierte el entero 100 a una cadena
```

**Convertir a lista:**

```py
lista = list((1, 2, 3)) # Convierte una tupla en una lista
```

**Convertir a tupla:**

```py
tupla = tuple([1, 2, 3]) # Convierte una lista en una tupla
```

## frozenset

Un frozenset es una versión inmutable de un conjunto (set). Una vez creado, no puedes agregar ni eliminar elementos de un frozenset. Es útil cuando necesitas un conjunto que no cambie y que se pueda usar como clave en un diccionario o almacenarse en otros conjuntos.

```py
# Crear un frozenset
fs = frozenset([1, 2, 3])

# Los frozensets son inmutables, por lo tanto, no puedes hacer fs.add(4)

# Puedes realizar operaciones de conjuntos como intersección, unión, etc.
fs2 = frozenset([2, 3, 4])
union = fs | fs2        # Unión: frozenset({1, 2, 3, 4})
interseccion = fs & fs2  # Intersección: frozenset({2, 3})

```

## Arboles

**Árbol binario:**

```py
class Nodo:
    def __init__(self, data):
        self.data = data
        self.izquierda = None
        self.derecha = None

class ArbolBinario:
    def __init__(self):
        self.raiz = None

    def agregar(self, data):
        if self.raiz is None:
            self.raiz = Nodo(data)
        else:
            self._agregar(data, self.raiz)

    def _agregar(self, data, nodo_actual):
        if data < nodo_actual.data:
            if nodo_actual.izquierda is None:
                nodo_actual.izquierda = Nodo(data)
            else:
                self._agregar(data, nodo_actual.izquierda)
        elif data > nodo_actual.data:
            if nodo_actual.derecha is None:
                nodo_actual.derecha = Nodo(data)
            else:
                self._agregar(data, nodo_actual.derecha)

```

**Árboles AVL, B, rojo-negro:** Puedes usar bibliotecas especializadas como binarytree para árboles binarios. Para AVL, B, y rojo-negro, se suelen utilizar implementaciones más avanzadas.

## Grafos

**Grafos dirigidos y no dirigidos:**

```py
class Grafo:
    def __init__(self):
        self.grafo = {}

    def agregar_vertice(self, v):
        if v not in self.grafo:
            self.grafo[v] = []

    def agregar_arista(self, v1, v2):
        if v1 in self.grafo:
            self.grafo[v1].append(v2)
        if v2 in self.grafo:
            self.grafo[v2].append(v1)  # Para grafos no dirigidos
```

**Matriz de adyacencia:**

```py
grafo = [[0, 1, 0], [1, 0, 1], [0, 1, 0]]
```

**Lista de adyacencia:**

```py
grafo = {0: [1], 1: [0, 2], 2: [1]}
```
