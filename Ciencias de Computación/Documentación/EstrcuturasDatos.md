# Estructuras de Datos Más Importantes

## 1. Estructuras de Datos Lineales

- **Array (Arreglo)**

  - **Descripción**: Colección de elementos del mismo tipo almacenados en ubicaciones contiguas de memoria.
  - **Aplicación**: Almacenamiento de datos que se acceden por índice.

- **Lista Enlazada (Linked List)**

  - **Descripción**: Secuencia de nodos donde cada nodo contiene un valor y una referencia al siguiente nodo.
  - **Aplicación**: Inserciones y eliminaciones eficientes.

  - **Variantes**:
    - **Lista Enlazada Simple (Singly Linked List)**
    - **Lista Enlazada Doblemente (Doubly Linked List)**
    - **Lista Enlazada Circular (Circular Linked List)**

- **Pila (Stack)**

  - **Descripción**: Estructura de datos basada en el principio LIFO (Last In, First Out). Los elementos se añaden y eliminan desde el mismo extremo.
  - **Aplicación**: Manejo de operaciones recursivas, deshacer acciones.

- **Cola (Queue)**

  - **Descripción**: Estructura de datos basada en el principio FIFO (First In, First Out). Los elementos se añaden en un extremo y se eliminan del otro.
  - **Aplicación**: Manejo de tareas en orden de llegada, sistemas de impresión.

  - **Variantes**:
    - **Cola Circular (Circular Queue)**
    - **Cola de Prioridad (Priority Queue)**

## 2. Estructuras de Datos No Lineales

- **Árbol (Tree)**

  - **Descripción**: Estructura de datos jerárquica con un nodo raíz y nodos hijos. Cada nodo puede tener múltiples hijos.
  - **Aplicación**: Representación de estructuras jerárquicas.

  - **Variantes**:
    - **Árbol Binario (Binary Tree)**
    - **Árbol Binario de Búsqueda (Binary Search Tree)**
    - **Árbol AVL (AVL Tree)**
    - **Árbol Rojo-Negro (Red-Black Tree)**
    - **Árbol B (B-Tree)**
    - **Árbol Trie (Prefix Tree)**
    - **Aplicaciones de los Árboles K-D**

- **Grafo (Graph)**

  - **Descripción**: Conjunto de nodos (vértices) y conexiones (aristas) entre ellos. Los grafos pueden ser dirigidos o no dirigidos.
  - **Aplicación**: Modelado de relaciones y redes.

  - **Variantes**:
    - **Grafo Dirigido (Directed Graph)**
    - **Grafo No Dirigido (Undirected Graph)**
    - **Grafo Ponderado (Weighted Graph)**
    - **Grafo No Ponderado (Unweighted Graph)**
    - **Grafo Cíclico (Cyclic Graph)**
    - **Grafo Acíclico (Acyclic Graph)**

## 3. Estructuras de Datos Basadas en Tablas

- **Tabla de Hash (Hash Table)**

  - **Descripción**: Estructura que asocia claves con valores mediante una función hash para una búsqueda eficiente.
  - **Aplicación**: Implementación de diccionarios y conjuntos.

  - **Variantes**:
    - **Hashing con Encadenamiento (Chaining)**
    - **Hashing con Direccionamiento Abierto (Open Addressing)**

## 4. Estructuras de Datos Avanzadas

- **Conjunto (Set)**

  - **Descripción**: Colección de elementos únicos sin orden específico.
  - **Aplicación**: Eliminación de duplicados, operaciones de conjunto.

- **Heap (Montículo)**

  - **Descripción**: Estructura de datos completa en forma de árbol que satisface la propiedad de heap (max-heap o min-heap).
  - **Aplicación**: Implementación de colas de prioridad y algoritmos de heapsort.

  - **Variantes**:
    - **Max-Heap**
    - **Min-Heap**

- **Segment Tree (Árbol de Segmento)**

  - **Descripción**: Estructura de datos para responder a consultas de rango en arrays de forma eficiente.
  - **Aplicación**: Consultas y actualizaciones de intervalos.

- **Fenwick Tree (Binary Indexed Tree)**
  - **Descripción**: Estructura de datos para realizar consultas y actualizaciones de rangos en arrays.
  - **Aplicación**: Cálculo de prefijos y sumas acumulativas.

## 5. Estructuras de Datos de Caché

- **LRU Cache (Least Recently Used Cache)**

  - **Descripción**: Implementa un caché con la política de reemplazo LRU.
  - **Aplicación**: Gestión de cachés en sistemas de alto rendimiento.

- **FIFO Cache (First In, First Out Cache)**

  - **Descripción**: Implementa un caché con la política de reemplazo FIFO.
  - **Aplicación**: Sistemas simples de caché.

- **LFU Cache (Least Frequently Used Cache)**
  - **Descripción**: Implementa un caché con la política de reemplazo LFU.
  - **Aplicación**: Caché con patrones de acceso no uniformes.

Estas estructuras de datos son fundamentales en la informática y el desarrollo de software, cada una con sus propias aplicaciones y ventajas según el contexto del problema que se desea resolver.
