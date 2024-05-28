# Peticiones HTTP en Go: Enviando y recibiendo datos desde la web

En Go, el paquete net/http proporciona un conjunto completo de herramientas para realizar peticiones HTTP a servidores web y procesar las respuestas. Esto te permite crear clientes HTTP que pueden interactuar con APIs, descargar contenido web o enviar datos a servidores remotos.

## Componentes principales

**http.Client:** Representa un cliente HTTP que se utiliza para realizar peticiones.
**http.Request:** Representa una petición HTTP que se envía al servidor.
**http.Response:** Representa la respuesta HTTP recibida del servidor.

### Ejemplo de uso de Http

```go
package main

import (
 "encoding/json"
 "fmt"
 "io/ioutil"
 "net/http"
)

// Petición a web

func main() {

 // URL de la página web a la que queremos hacer la petición

 url := "https://www.wikipedia.org/"

 // Realizamos la petición GET

 resp, err := http.Get(url)
 if err != nil {
  fmt.Printf("Error realizando la petición: %v\n", err)
  return
 }
 defer resp.Body.Close()

 // Verificamos que la petición fue exitosa (código de estado 200)

 if resp.StatusCode != http.StatusOK {
  fmt.Printf("Error: estado de respuesta %d\n", resp.StatusCode)
  return
 }

 // Leemos el contenido de la respuesta

 body, err := ioutil.ReadAll(resp.Body)
 if err != nil {
  fmt.Printf("Error leyendo el cuerpo de la respuesta: %v\n", err)
  return
 }

 // Mostramos el contenido de la página web en la consola

 fmt.Println(string(body))
}

// Petición API JSON

// Definimos las estructuras de datos en Go que coinciden con la estructura de datos JSON esperada.

type AlmacenesInterface struct {
 IsSuccess bool            `json:"isSuccess"`
 Result    int             `json:"result"`
 Data      []DatosAlmacenes `json:"data"`
 Message   string          `json:"message"`
}

type DatosAlmacenes struct {
 Documento string `json:"documento"`
 Nombre    string `json:"nombre"`
 Zona      Zona   `json:"zona"`
 Bodega    string `json:"bodega"`
}

type Zona string

// Función principal

func PeticiónAPI() {

 // URL de la API

 url := "http://200.110.169.7/incoco.Api/api/Logistica/listaClientesSeparadoVo5"

 // Realizamos la petición GET

 resp, err := http.Get(url)
 if err != nil {
  fmt.Printf("Error realizando la petición: %v\n", err)
  return
 }
 // Cerrar el cuerpo de la respuesta
 defer resp.Body.Close()

 // Verificamos que la petición fue exitosa (código de estado 200)

 if resp.StatusCode != http.StatusOK {
  fmt.Printf("Error: estado de respuesta %d\n", resp.StatusCode)
  return
 }

 // Decodificamos el contenido JSON de la respuesta en la estructura de datos AlmacenesInterface

 var almacenes AlmacenesInterface
 err = json.NewDecoder(resp.Body).Decode(&almacenes)
 if err != nil {
  fmt.Printf("Error decodificando JSON: %v\n", err)
  return
 }

 // Mostramos la información obtenida

 fmt.Println("IsSuccess:", almacenes.IsSuccess)
 fmt.Println("Result:", almacenes.Result)
 fmt.Println("Message:", almacenes.Message)
 fmt.Println("Data:")

 // Iteramos sobre los datos y los mostramos

 for _, dato := range almacenes.Data {
  fmt.Println("Documento:", dato.Documento)
  fmt.Println("Nombre:", dato.Nombre)
  fmt.Println("Zona:", dato.Zona)
  fmt.Println("Bodega:", dato.Bodega)
  fmt.Println()
 }
}
```
