# Valor vs. Referencia en Go: Entendiendo la diferencia fundamental

En Go, la distinción entre valor y referencia es crucial para comprender el comportamiento de los datos y las variables. Esta diferenciación tiene un impacto significativo en cómo se pasan y manipulan los datos en tu programa.

## Valor

Un valor representa la representación directa de un dato en memoria. Al declarar una variable y asignarle un valor, se crea una copia independiente del dato en la memoria. Las operaciones realizadas sobre la variable solo afectan a su propia copia, sin modificar el valor original.

```go
var numero int = 10
otraVariable := numero // Asignación por valor

numero = 20 // Modificar el valor original

fmt.Println(numero)  // Imprime 20
fmt.Println(otraVariable) // Imprime 10 (valor original sin modificar)
```

## Referencia

Una referencia no almacena el dato en sí, sino que guarda la dirección de memoria donde se encuentra el dato original. Al pasar una referencia como argumento o asignarla a otra variable, se crea un alias que apunta al mismo dato en memoria. Cualquier modificación realizada a través de la referencia afecta directamente al valor original.

```go
var numero int = 10
otraVariable := &numero // Asignación por referencia

numero = 20 // Modificar el valor original

fmt.Println(numero)  // Imprime 20
fmt.Println(otraVariable) // Imprime 20 (valor original modificado)
```
