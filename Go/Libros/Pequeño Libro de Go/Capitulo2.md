# Capítulo 2: Trabajando con Estructuras en Go

## Definición y Uso de Estructuras

**Definición de la estructura Saiyan:**

```go
type Saiyan struct {
    Name string
    Power int
}
```

## Métodos Asociados a Estructuras

**Asociar un método con una estructura:**

```go
func (s *Saiyan) Super() {
    s.Power += 10000
}
```

**Ejemplo de uso del método Super:**

```go
func capitulo2() {
    goku := &Saiyan{"Goku", 9001}
    goku.Super()
    fmt.Println(goku.Power) // Mostrará 19001
}
```

## Declaración e Inicialización de Estructuras

**Inicialización con valores explícitos:**

```go
goku := Saiyan{
    Name:  "Goku",
    Power: 9000,
}
```

**nicialización sin valores explícitos:**

```go
goku := Saiyan{}
// o
goku := Saiyan{Name: "Goku"}
goku.Power = 9000
```

**Inicialización basada en el orden de los campos:**

```go
goku := Saiyan{"Goku", 9000}
```

## Trabajar con Punteros

**Pasar estructuras como punteros para modificar sus valores:**

```go
func main() {
    goku := &Saiyan{"Goku", 9000}
    Super(goku)
    fmt.Println(goku.Power) // Mostrará 19000
}

func Super(s *Saiyan) {
    s.Power += 10000
}
```

## Constructores en Go

**Crear una función constructora:**

```go
func NewSaiyan(name string, power int) *Saiyan {
    return &Saiyan{
        Name:  name,
        Power: power,
    }
}
```

**Constructor que devuelve un valor:**

```go
func NewSaiyan(name string, power int) Saiyan {
    return Saiyan{
        Name:  name,
        Power: power,
    }
}
```

## Uso de la Función new

**Uso de la función new para inicializar estructuras:**

```go
goku := new(Saiyan)
// es lo mismo que
goku := &Saiyan{}
```

**Inicialización con valores usando &:**

```go
goku := &Saiyan{
    Name:  "Goku",
    Power: 9000,
}
```

## Campos de una Estructura

**Agregar campos adicionales a una estructura:**

```go
type Saiyan struct {
    Name   string
    Power  int
    Father *Saiyan
}
```

**Inicializar estructuras anidadas:**

```go
gohan := &Saiyan{
    Name:  "Gohan",
    Power: 1000,
    Father: &Saiyan{
        Name:  "Goku",
        Power: 9001,
        Father: nil,
    },
}
```

## Composición de Estructuras

**Uso de composición para incluir una estructura dentro de otra:**

```go
type Person struct {
    Name string
}

func (p *Person) Introduce() {
    fmt.Printf("Hi, I'm %s\n", p.Name)
}

type Saiyan struct {
    *Person
    Power int
}

// Uso de la estructura compuesta
goku := &Saiyan{
    Person: &Person{"Goku"},
    Power:  9001,
}
goku.Introduce() // Llamada al método Introduce de Person
```

**Acceso implícito a campos y métodos de la estructura compuesta:**

```go
goku := &Saiyan{
    Person: &Person{"Goku"},
}
fmt.Println(goku.Name) // Acceso directo al campo Name de Person
fmt.Println(goku.Person.Name) // Acceso explícito al campo Name de Person
```

## Sobrecarga

**Go no soporta sobrecarga de funciones. En su lugar, se utilizan nombres específicos:**

```go
// No sobrecarga
func Load() {}
func LoadById() {}
func LoadByName() {}
```

**Definir un método específico para una estructura:**

```go
func (s *Saiyan) Introduce() {
    fmt.Printf("Hi, I'm %s. Ya!\n", s.Name)
}
```

**Llamada a la versión original del método:**

```go
goku.Person.Introduce()
```
