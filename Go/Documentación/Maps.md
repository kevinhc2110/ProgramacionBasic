# Mapas en Go: Almacenamiento Eficiente de Clave-Valor

En Go, los mapas (también conocidos como diccionarios) son estructuras de datos fundamentales para almacenar pares de clave-valor. Permiten asociar valores arbitrarios con claves únicas, proporcionando una forma eficiente de acceder y recuperar datos.

## Características de los Mapas en Go

**No ordenados:** Los mapas no mantienen un orden interno de los elementos.
**Acceso por clave:** Se accede a los valores de un mapa utilizando la clave correspondiente.
**Tipados:** Los mapas están tipados por el tipo de clave y el tipo de valor.
**Mutables:** Los valores de un mapa se pueden modificar después de su creación.
**Sin duplicados:** Las claves en un mapa deben ser únicas, no se permiten duplicados.

### Ejemplo de uso de maps

```go
package main

import "fmt"

func main() {

 // Crear un mapa usando make
 mapa := make(map[string]int)

 // Crear un map con valores

scrabbleValues := map[rune]int{
  'A': 1, 'B': 3, 'C': 3, 'D': 2, 'E': 1, 'F': 4, 'G': 2, 'H': 4,
  'I': 1, 'J': 8, 'K': 5, 'L': 1, 'M': 3, 'N': 1, 'O': 1, 'P': 3,
  'Q': 10, 'R': 1, 'S': 1, 'T': 1, 'U': 1, 'V': 4, 'W': 4, 'X': 8,
  'Y': 4, 'Z': 10,
 }

 // Insertar valores
 mapa["uno"] = 1
 mapa["dos"] = 2
 mapa["tres"] = 3

 // Acceder a un valor
 valor := mapa["dos"]
 fmt.Println("El valor de 'dos' es:", valor) // Output: El valor de 'dos' es: 2

 // Verificar si una clave existe
 if val, ok := mapa["cuatro"]; ok {
  fmt.Println("El valor de 'cuatro' es:", val)
 } else {
  fmt.Println("'cuatro' no se encuentra en el mapa")
 }

 // Eliminar un par clave-valor
 delete(mapa, "uno")

 // Iterar sobre el mapa
 for clave, valor := range mapa {
  fmt.Printf("Clave: %s, Valor: %d\n", clave, valor)
 }
}
```
