# Capítulo 3: Trabajando con Rebanadas (Slices) y Arrays en Go

## Crear y Manejar Rebanadas

### Crear una rebanada de enteros para almacenar puntuaciones

```go
scores := make([]int, 100)
```

### Llenar la rebanada con puntuaciones aleatorias entre 0 y 999

```go
for i := 0; i < 100; i++ {
    scores[i] = int(rand.Int31n(1000))
}
```

### Ordenar las puntuaciones en orden ascendente

```go
sort.Ints(scores)
```

### Crear una rebanada para almacenar las 5 peores puntuaciones

```go
worst := make([]int, 5)
copy(worst, scores[:5])
fmt.Println(worst)
```

## Arrays en Go

**Los arrays tienen un tamaño fijo y se definen con una longitud específica:**

```go
var scores [10]int
scores[0] = 339
```

**También pueden ser inicializados con valores:**

```go
scores := [4]int{9001, 9333, 212, 33}
```

**Utiliza len para obtener la longitud del array y range para iterar sobre él:**

```go
for index, value := range scores {
    // Operaciones con index y value
}
```

## Slices en Go

**Un slice es una estructura que representa una porción de un array:**

```go
scores := []int{1, 4, 293, 4, 9}
```

**Crear un slice con make:**

```go
scores := make([]int, 10)
```

**Especificar longitud y capacidad al crear un slice:**

```go
scores := make([]int, 0, 10)
```

### Trabajar con Slices

**Expandir un slice con append:**

```go
scores := make([]int, 0, 10)
scores = append(scores, 5)
fmt.Println(scores) // Muestra [5]
```

**Redimensionar un slice:**

```go
scores := make([]int, 0, 10)
scores = scores[0:6]
scores[5] = 9033
fmt.Println(scores) // Muestra [0 0 0 0 0 9033]

```

**Crecimiento dinámico del array subyacente:**

```go
scores := make([]int, 0, 5)
c := cap(scores)
fmt.Println(c)
for i := 0; i < 25; i++ {
    scores = append(scores, i)
    if cap(scores) != c {
        c = cap(scores)
        fmt.Println(c)
    }
}
```

### Inicializar un Slice

**Varias formas de inicializar un slice:**

```go
names := []string{"leto", "jessica", "paul"}
checks := make([]bool, 10)
var names []string
scores := make([]int, 0, 20)
```

**Uso de Slices como Wrappers de Arrays**
_Modificar un array a través de un slice:_

```go
scores := []int{1, 2, 3, 4, 5}
slice := scores[2:4]
slice[0] = 999
fmt.Println(scores) // Muestra [1, 2, 999, 4, 5]
```

**Borrar un Valor de un Slice sin Ordenar**
_Función para eliminar un valor de un slice sin mantener el orden:_

```go
func main() {
    scores := []int{1, 2, 3, 4, 5}
    scores = removeAtIndex(scores, 2)
    fmt.Println(scores) // Muestra [1, 2, 5, 4]
}

func removeAtIndex(source []int, index int) []int {
    lastIndex := len(source) - 1
    source[index], source[lastIndex] = source[lastIndex], source[index]
    return source[:lastIndex]
}
```

## Trabajando con Mapas (Maps) en Go

**Crear y manipular mapas:**

```go
func main() {
    lookup := make(map[string]int)
    lookup["goku"] = 9001
    power, exists := lookup["vegeta"]
    fmt.Println(power, exists) // Muestra 0, false
}
```

**Obtener la longitud del mapa y borrar elementos:**

```go
total := len(lookup)
delete(lookup, "goku")
```

**Especificar un tamaño inicial para el mapa:**

```go
lookup := make(map[string]int, 100)
```

**Mapas como campos en estructuras:**

```go
type Saiyan struct {
    Name string
    Friends map[string]*Saiyan
}
goku := &Saiyan{
    Name: "Goku",
    Friends: make(map[string]*Saiyan),
}
goku.Friends["krillin"] = &Saiyan{Name: "Krillin"}
```

**Inicializar un mapa con valores:**

```go
lookup := map[string]int{
    "goku": 9001,
    "gohan": 2044,
}
```

**Iterar sobre un mapa:**

```go
for key, value := range lookup {
    fmt.Println(key, value)
}
```

## Punteros versus Valores

**Decisión entre arrays de punteros o valores depende del uso:**

```go
a := make([]Saiyan, 10)
b := make([]*Saiyan, 10)
```
