# Notaciones Asintóticas y Tiempos de Ejecución

## 1. Notación Big O (O)

Describe el peor escenario para la complejidad temporal de un algoritmo.

- **Ejemplo**: `O(n)` - Complejidad lineal.
- **Ejemplos de Tiempo de Ejecución**:
  - Constante: `O(1)` - Acceso a un elemento de un array.
  - Logarítmico: `O(log n)` - Búsqueda binaria.
  - Lineal: `O(n)` - Bucle simple a través de un array.
  - Cuadrático: `O(n^2)` - Bucles anidados.

## 2. Notación Big Omega (Ω)

Representa el mejor caso.

- **Ejemplo**: `Ω(n)` - Complejidad lineal.
- **Tiempo de Ejecución**: En un array ordenado, el mejor caso para la búsqueda lineal es `Ω(1)`.

## 3. Notación Theta (Θ)

Describe el caso promedio con los límites superior e inferior.

- **Ejemplo**: `Θ(n log n)` - Ordenamiento por fusión.
- **Tiempo de Ejecución**: Algoritmos balanceados como el quicksort en el caso promedio.

## 4. Notación Little o (o)

Representa un límite superior que no es ajustado.

- **Ejemplo**: `o(n^2)` - Crece más lentamente que `n^2`.

## 5. Notación Little Omega (ω)

Representa un límite inferior que no es ajustado.

- **Ejemplo**: `ω(n)` - Crece más rápido que `n`.

---

## Complejidades de Tiempo Comunes y Ejemplos

| Complejidad de Tiempo | Nombre       | Ejemplo                                             |
| --------------------- | ------------ | --------------------------------------------------- |
| O(1)                  | Constante    | Acceso a un elemento en un array                    |
| O(log n)              | Logarítmica  | Búsqueda binaria                                    |
| O(n)                  | Lineal       | Recorrer un array                                   |
| O(n log n)            | Linealítmica | Ordenamiento por fusión, heapsort                   |
| O(n^2)                | Cuadrática   | Bucles anidados (por ejemplo, ordenamiento burbuja) |
| O(2^n)                | Exponencial  | Algoritmos recursivos como la Torre de Hanoi        |
| O(n!)                 | Factorial    | Algoritmos de generación de permutaciones           |

---

## Tipos de Algoritmos

### 1. **Algoritmos de Tiempo Constante (O(1))**

- El tiempo de ejecución es fijo y no crece con el tamaño de la entrada.
- **Ejemplo**: Acceso a un elemento en un array.

### 2. **Algoritmos de Tiempo Logarítmico (O(log n))**

- El tiempo de ejecución crece de manera logarítmica. Eficiente para conjuntos de datos grandes.
- **Ejemplo**: Búsqueda binaria.

### 3. **Algoritmos de Tiempo Lineal (O(n))**

- El tiempo de ejecución crece directamente proporcional al tamaño de la entrada.
- **Ejemplo**: Recorrer un array.

### 4. **Algoritmos de Tiempo Linealítmico (O(n log n))**

- Una combinación de crecimiento lineal y logarítmico.
- **Ejemplo**: Ordenamiento por fusión, quicksort (caso promedio).

### 5. **Algoritmos de Tiempo Cuadrático (O(n^2))**

- El tiempo de ejecución crece cuadráticamente, a menudo debido a bucles anidados.
- **Ejemplo**: Ordenamiento burbuja, ordenamiento por inserción.

### 6. **Algoritmos de Tiempo Exponencial (O(2^n))**

- El crecimiento se duplica con cada elemento adicional de entrada.
- **Ejemplo**: Algoritmos recursivos como la resolución de la Torre de Hanoi.

### 7. **Algoritmos de Tiempo Factorial (O(n!))**

- La complejidad temporal crece factorialmente con el tamaño de la entrada.
- **Ejemplo**: Algoritmos de permutación o soluciones de fuerza bruta para el problema del vendedor viajero.
