# Creando un servidor básico en Go

## Estructura basica

```go
package main

import (
    "fmt"
    "net/http"
)

func main() {
    // Definir la función manejadora para la ruta "/"
    http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
        fmt.Fprintf(w, "Hola desde mi servidor Go!")
    })

    // Iniciar el servidor en el puerto 8080
    fmt.Println("Iniciando servidor en http://localhost:8080")
    http.ListenAndServe(":8080", nil)
}
```

### Explicación

_package main:_ Indica que el archivo contiene el punto de entrada del programa.
_import:_ Se importan los paquetes necesarios: fmt para formatear el texto y net/http para trabajar con el protocolo HTTP.
_func main():_ Función principal donde se ejecuta el código del programa.
_http.HandleFunc:_ Registra una función manejadora para la ruta /. La función manejadora recibe dos argumentos: w (objeto ResponseWriter para escribir la respuesta) y r (objeto Request que contiene la información de la solicitud).
_fmt.Fprintf:_ Escribe el texto "Hola desde mi servidor Go!" en la respuesta.
http.ListenAndServe: Inicia el servidor HTTP en el puerto 8080.

### Ejecutando el servidor

_Guarda el código como server.go._
_Abre una terminal y navega hasta el directorio donde guardaste el archivo._
_Ejecuta el comando: go run server.go_
_Deberías ver el mensaje "Iniciando servidor en_ //localhost:8080" _en la terminal._
_Abre un navegador web y ve a_ //localhost:8080. _Deberías ver el texto "Hola desde mi servidor Go!"._

### Mejoras y extensiones

_Puedes agregar más rutas y funciones manejadoras para manejar diferentes solicitudes HTTP (GET, POST, PUT, DELETE)._
_Puedes utilizar un framework web como Gorilla Mux o Echo para facilitar la organización y el manejo de las rutas y las funciones manejadoras._
_Puedes conectar el servidor a una base de datos para almacenar y recuperar datos._
_Puedes implementar autenticación y autorización para proteger el acceso a tu servidor._
