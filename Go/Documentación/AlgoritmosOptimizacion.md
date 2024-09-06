# Algoritmos de Optimización en Go

## ¡Absolutamente! Profundicemos en los algoritmos de optimización y grafos en Go

Algoritmos de Optimización en Go
Programación Dinámica
La programación dinámica es una técnica poderosa para resolver problemas que pueden descomponerse en subproblemas más pequeños y cuyas soluciones se pueden almacenar para evitar cálculos repetidos.

```go
package main

import "fmt"

func fibonacci(n int) int {
    if n <= 1 {
        return n
    }
    memo := make([]int, n+1)
    memo[0] = 0
    memo[1] = 1
    for i := 2; i <= n; i++ {
        memo[i] = memo[i-1] + memo[i-2]
    }
    return memo[n]
}

func main() {
    result := fibonacci(10)
    fmt.Println(result)
}
```

## Backtracking

El backtracking es una técnica de búsqueda exhaustiva que explora todas las posibles soluciones, abandonando ramas que no prometen una solución válida.

_Ejemplo:_ El problema de las N-Reinas consiste en colocar N reinas en un tablero de ajedrez de N x N de tal manera que ninguna reina pueda atacar a otra.

```go
package main

import (
        "fmt"
)

func solveNQueens(n int) [][]string {
        board := make([][]byte, n)
        for i := range board {
                board[i] = make([]byte, n)
                for j := range board[i] {
                        board[i][j] = '.'
                }
        }
        res := [][]string{}
        solveNQueensHelper(board, 0, &res)
        return res
}

func solveNQueensHelper(board [][]byte, row int, res *[][]string) {
        if row == len(board) {
                // Una solución encontrada, convertirla a una matriz de strings
                tmp := make([]string, len(board))
                for i := range board {
                        tmp[i] = string(board[i])
                }
                *res = append(*res, tmp)
                return
        }
        for col := 0; col < len(board); col++ {
                if isValid(board, row, col) {
                        board[row][col] = 'Q'
                        solveNQueensHelper(board, row+1, res)
                        board[row][col] = '.'
                }
        }
}

func isValid(board [][]byte, row, col int) bool {
        // Comprobar fila y columna
        for i := 0; i < row; i++ {
                if board[i][col] == 'Q' {
                        return false
                }
        }
        // Comprobar diagonal superior izquierda
        for i, j := row-1, col-1; i >= 0 && j >= 0; i, j = i-1, j-1 {
                if board[i][j] == 'Q' {
                        return false
                }
        }
        // Comprobar diagonal superior derecha
        for i, j := row-1, col+1; i >= 0 && j < len(board); i, j = i-1, j+1 {
                if board[i][j] == 'Q' {
                        return false
                }
        }
        return true
}

func main() {
        n := 8
        solutions := solveNQueens(n)
        for _, solution := range solutions {
                for _, row := range solution {
                        fmt.Println(row)
                }
                fmt.Println()
        }
}
```

## Algoritmo de Dijkstra

El algoritmo de Dijkstra encuentra el camino más corto desde un nodo fuente a todos los demás nodos en un grafo ponderado donde los pesos de los bordes son no negativos.

```go
package main

import (
        "fmt"
)

type Graph map[int]map[int]int

func dijkstra(graph Graph, start int) map[int]int {
        distances := make(map[int]int)
        for u := range graph {
                distances[u] = 1<<63 - 1
        }
        distances[start] = 0

        visited := make(map[int]bool)
        for len(visited) < len(graph) {
                u, minDistance := findMinDistance(distances, visited)
                visited[u] = true
                for v, weight := range graph[u] {
                        dist := distances[u] + weight
                        if dist < distances[v] {
                                distances[v] = dist
                        }
                }
        }
        return distances
}

// ... implementación de findMinDistance ...

func main() {
        // ... ejemplo de uso ...
}
```

## Algoritmos de Grafos en Go

**Caminos Mínimos:**

_Bellman-Ford:_ Maneja pesos negativos en los bordes.

```go
package main

import "fmt"

type Graph map[int]map[int]int

func bellmanFord(graph Graph, source int) map[int]int {
    dist := make(map[int]int)
    for u := range graph {
        dist[u] = 1<<63 - 1 // Inicializar distancias a infinito
    }
    dist[source] = 0

    // Relajar las aristas V-1 veces
    for i := 0; i < len(graph)-1; i++ {
        for u, neighbors := range graph {
            for v, weight := range neighbors {
                if dist[u]+weight < dist[v] {
                    dist[v] = dist[u] + weight
                }
            }
        }
    }

    // Detectar ciclos negativos
    for u, neighbors := range graph {
        for v, weight := range neighbors {
            if dist[u]+weight < dist[v] {
                fmt.Println("Grafo contiene un ciclo negativo")
                return nil
            }
        }
    }
    return dist
}

func main() {
    // ... ejemplo de uso ...
}
```

_Floyd-Warshall:_ Encuentra la distancia más corta entre todos los pares de nodos.

```go
package main

import "fmt"

type Graph map[int]map[int]int

func floydWarshall(graph Graph) [][]int {
    dist := make([][]int, len(graph))
    for i := range dist {
        dist[i] = make([]int, len(graph))
        for j := range dist[i] {
            if i == j {
                dist[i][j] = 0
            } else if _, ok := graph[i][j]; ok {
                dist[i][j] = graph[i][j]
            } else {
                dist[i][j] = 1<<63 - 1
            }
        }
    }

    for k := range graph {
        for i := range graph {
            for j := range graph {
                dist[i][j] = min(dist[i][j], dist[i][k]+dist[k][j])
            }
        }
    }

    return dist
}

func min(a, b int) int {
    if a < b {
        return a
    }
    return b
}

func main() {
    // ... ejemplo de uso ...
}
```

_Estructuras de Datos para Grafos en Go:_

_Lista de adyacencia:_ Representa un grafo como una lista de vecinos para cada nodo.

La lista de adyacencia es una estructura de datos muy eficiente para representar grafos esparsos, es decir, aquellos donde el número de aristas es significativamente menor que el número máximo posible de aristas (N\*(N-1)/2).

```go
type Graph map[int][]int

func createGraph() Graph {
    graph := make(Graph)
    // Agregar aristas aquí, por ejemplo:
    graph[0] = []int{1, 2}
    graph[1] = []int{2}
    graph[2] = []int{3}
    return graph
}
```

_Matriz de adyacencia:_ Representa un grafo como una matriz donde el elemento (i, j) indica si existe una arista entre los nodos i y j.

La matriz de adyacencia es una estructura de datos útil para representar grafos densos, donde el número de aristas es cercano al número máximo posible.

```go
type Graph [][]bool

func createGraph(n int) Graph {
    graph := make(Graph, n)
    for i := range graph {
        graph[i] = make([]bool, n)
    }
    // Agregar aristas aquí, por ejemplo:
    graph[0][1] = true
    graph[0][2] = true
    // ...
    return graph
}
```

## Algoritmos de Recorrido

Topological Sort: Ordena los nodos de un grafo dirigido acíclico en un orden lineal.

```go
package main

import (
        "fmt"
)

type Graph map[int][]int

func topologicalSort(graph Graph) []int {
    // Calcular el grado de entrada de cada vértice
    indegree := make(map[int]int)
    for _, neighbors := range graph {
        for neighbor := range neighbors {
            indegree[neighbor]++
        }
    }

    // Encontrar vértices con grado de entrada 0
    queue := []int{}
    for u, degree := range indegree {
        if degree == 0 {
            queue = append(queue, u)
        }
    }

    // Realizar un BFS modificado
    result := []int{}
    for len(queue) > 0 {
        u := queue[0]
        queue = queue[1:]
        result = append(result, u)
        for _, v := range graph[u] {
            indegree[v]--
            if indegree[v] == 0 {
                queue = append(queue, v)
            }
        }
    }

    // Si el resultado tiene menos elementos que el número de vértices, hay un ciclo
    if len(result) != len(graph) {
        return nil
    }
    return result
}

func main() {
    // ... ejemplo de uso ...
}
```
