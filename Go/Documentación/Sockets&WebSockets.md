# Sockets

Los sockets son una interfaz de programación de aplicaciones (API) que permite la comunicación entre procesos en una red. Pueden ser TCP (Transmission Control Protocol) o UDP (User Datagram Protocol).

```go
package main

import (
        "fmt"
        "net"
)

func main() {
        ln, err := net.Listen("tcp", ":8080")
        if err != nil {
                // Manejar el error
        }
        defer ln.Close()

        for {
                conn, err := ln.Accept()
                if err != nil {
                    // Manejar el error
                }
                go handleConnection(conn)
        }
}

func handleConnection(conn net.Conn) {
        // Manejar la conexión
        defer conn.Close()
        // ...
}
```

## WebSockets

WebSockets son una tecnología que permite una comunicación bidireccional en tiempo real entre un cliente y un servidor a través de una única conexión TCP. Se utilizan principalmente para aplicaciones que requieren actualizaciones constantes de datos, como chat en tiempo real, juegos en línea y aplicaciones de colaboración.

_Conexión persistente:_ Una vez establecida la conexión, se mantiene abierta hasta que se cierra explícitamente.
_Comunicación bidireccional:_ Tanto el cliente como el servidor pueden enviar y recibir mensajes.
_Mensajes de texto:_ Los mensajes se transmiten en formato de texto.
_Protocolo sobre HTTP:_ Se establece inicialmente a través de una solicitud HTTP, pero luego se cambia a un protocolo de WebSocket.

```go
import (
        "fmt"
        "log"
        "net/http"

        "github.com/gorilla/websocket"
)

var upgrader = websocket.Upgrader{
        ReadBufferSize:  1024,
        WriteBufferSize: 1024,
}

func  
 main() {
        http.HandleFunc("/ws",  
 wsHandler)
        log.Fatal(http.ListenAndServe(":8080", nil))
}

func wsHandler(w http.ResponseWriter, r *http.Request) {
        // ...
}
```

Este fragmento de código Go establece un servidor WebSocket básico. Un servidor WebSocket permite una comunicación bidireccional en tiempo real entre un cliente (por ejemplo, un navegador web) y un servidor. Es decir, los datos pueden fluir en ambas direcciones de manera continua, sin que el cliente tenga que enviar nuevas solicitudes constantemente.
