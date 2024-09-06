# Estructuras de control

## Condicionales

```go
func main() {

  if x > 10 {
    fmt.Println("x es mayor que 10")
  }

  if x > 10 {
    fmt.Println("x es mayor que 10")
  } else if x < 10 {
    fmt.Println("x es menor que 10")
  } else {
    fmt.Println("x es igual a 10")
  }
}
```

## Switch

```go
switch day {
case "Monday":
    fmt.Println("Lunes")
case "Tuesday":
    fmt.Println("Martes")
default:
    fmt.Println("Otro día")
}
```

## Bucles

### For

```go
// Bucle con contador
for i := 0; i < 10; i++ {
    fmt.Println(i)
}

// Bucle sobre un slice
for index, value := range mySlice {
    fmt.Println(index, value)
}
```

### While

```go
i := 0
for i < 10 {
    fmt.Println(i)
    i++
}
```
