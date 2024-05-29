# Estructuras de control

```go
func main() {

  num1 := 1
  name := "Hola"

  // Condicionales

  if num1 == 5 {
  fmt.Println("El valor es 5")
  } else if num1 == 10 {
  fmt.Println("El valor es 10")
  } else {
  fmt.Println("El valor no es 5")
  }


  if (num1 == 7 && name == "Coco"){ // And
  fmt.Println("El valor es 5")
  } else if (num1 == 7 || name == "Pepe"){ // Or
  fmt.Println("El valor no es 5")
  }

  // Bucles

  var myArray [3]int

  // For normal

  for i := 0; i < len(myArray); i++ {
  fmt.Println(myArray[i])
  }

  myMap := make(map[string]int)
  myMap["Brais"] = 36
  myMap["Kevin"] = 26

  // Rango

  for key, value := range myMap {
  fmt.Println(key,value)
  }

  for index, value := range myArray {
  fmt.Println(index,value)
  }

  // While

  for numero < 10 {
    fmt.Println(numero)
  }

  // Switch

  option:= 1

  switch option {
    case 1:
    fmt.Println("Caso 1")
    case 2:
        fmt.Println("Caso 2")
      default:
        fmt.Println("Ningún caso")
  }
}

```
