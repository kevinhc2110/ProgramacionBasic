# container/list

Este paquete ofrece una implementación de listas doblemente enlazadas, una estructura de datos útil para almacenar elementos en un orden secuencial.

## Características clave de container/list

**Estructura doblemente enlazada:** Cada elemento en la lista tiene referencias (punteros) hacia el siguiente y el anterior elemento, permitiendo una navegación eficiente en ambas direcciones.
**Operaciones basadas en elementos:** El paquete proporciona métodos para manipular elementos individuales, como insertar, eliminar y acceder a sus valores.
**Iteradores:** Ofrece iteradores para recorrer la lista en dirección hacia adelante y hacia atrás.

## Ventajas de container/list

**Administración eficiente de memoria:** Las listas doblemente enlazadas proporcionan una gestión de memoria óptima, especialmente cuando se realizan inserciones y eliminaciones frecuentes.
**Acceso flexible a elementos:** Se puede acceder a los elementos y modificarlos desde el principio y el final de la lista.
**Compatibilidad con iteración:** El paquete proporciona iteradores para recorrer la lista en ambas direcciones.

## Cuándo usar container/list

_Cuando necesitas una estructura de datos que admita la inserción, eliminación e iteración eficientes de elementos._
_Cuando el orden de los elementos es importante y necesitas acceder a ellos desde ambos extremos de la lista._
_Cuando trabajas con conjuntos de datos grandes donde se esperan modificaciones frecuentes._

### Ejemplo de uso de listas

```go
package main

import (
    "container/list"
    "fmt"
)

func main() {
    // Crear una nueva lista
    l := list.New()

    // Insertar elementos al frente y al final
    l.PushFront("Primero")
    l.PushBack("Último")

    // Insertar elementos antes y después de un elemento específico
    e := l.PushBack("Medio")
    l.InsertAfter("Después del Medio", e)
    l.InsertBefore("Antes del Medio", e)

    // Eliminar un elemento específico
    l.Remove(e)

    // Iterar sobre la lista
    fmt.Println("Elementos en la lista:")
    for e := l.Front(); e != nil; e = e.Next() {
        fmt.Println(e.Value)
    }
}
```
