# Comunicación en Sistemas Distribuidos

## 1. REST APIs

### HTTP Status Codes

Usa los códigos correctos para que el cliente sepa exactamente qué pasó.

| Código | Significado           | Cuándo usarlo                                                     |
| ------ | --------------------- | ----------------------------------------------------------------- |
| 100    | Continue              | El servidor acepta los headers; el cliente puede enviar el cuerpo |
| 200    | OK                    | Todo salió bien (GET, PUT, PATCH...)                              |
| 201    | Created               | Recurso creado con éxito (POST)                                   |
| 202    | Accepted              | Petición aceptada pero aún no procesada                           |
| 204    | No Content            | Éxito sin contenido de respuesta (DELETE, etc.)                   |
| 400    | Bad Request           | Datos mal enviados por el cliente                                 |
| 401    | Unauthorized          | No autenticado                                                    |
| 403    | Forbidden             | No tiene permisos                                                 |
| 404    | Not Found             | El recurso no existe                                              |
| 409    | Conflict              | Conflicto al procesar (ej. recurso duplicado)                     |
| 422    | Unprocessable Entity  | Entidad no procesable (validación compleja fallida)               |
| 429    | Too Many Requests     | Límite de peticiones excedido (rate limiting)                     |
| 500    | Internal Server Error | Falla general del backend                                         |
| 502    | Bad Gateway           | Error al comunicarse con otro servidor                            |
| 503    | Service Unavailable   | Servicio no disponible temporalmente                              |
| 504    | Gateway Timeout       | El servidor no respondió a tiempo                                 |

### HTTP Methods

Cada método representa una acción específica:

| Método  | Acción                                   | Ejemplo           |
| ------- | ---------------------------------------- | ----------------- |
| GET     | Obtener datos                            | `GET /users/1`    |
| POST    | Crear recurso nuevo                      | `POST /users`     |
| PUT     | Reemplazar completo                      | `PUT /users/1`    |
| PATCH   | Actualizar parcial                       | `PATCH /users/1`  |
| DELETE  | Borrar recurso                           | `DELETE /users/1` |
| OPTIONS | Consultar qué métodos acepta un endpoint | `OPTIONS /users`  |

### Idempotencia

Significa que **hacer la misma petición varias veces** no cambia el resultado final.

| Método | ¿Es idempotente? | Notas                                             |
| ------ | ---------------- | ------------------------------------------------- |
| GET    | ✅ Sí            | No cambia el estado                               |
| PUT    | ✅ Sí            | Reemplaza con el mismo contenido                  |
| DELETE | ✅ Sí            | Borrar el mismo recurso múltiples veces es válido |
| POST   | ❌ No            | Cada petición crea algo nuevo                     |
| PATCH  | ⚠ Depende        | Depende de qué campos actualizas                  |

### Query Parameters

Sirven para modificar cómo se recuperan los datos sin cambiar el recurso.

```http
GET /users?page=1&size=10&sort=name
```

**Tips para APIs eficientes:**

- Siempre soporta paginación (page, limit, offset)
- Soporta filtros por campos (GET /users?status=active)
- Permite ordenar (sort=createdAt,-name)

### Domain Model Driven Design

Diseña tus rutas como si fueran parte de tu modelo de negocio real.

```http
GET /products/{id}/reviews
```

**Tips:**

- Usa nombres plurales para colecciones (/users, /products)
- Evita acciones en URLs (no GET /getUser o POST /createUser)
- Usa rutas anidadas para relaciones (/orders/{id}/items)

### Respuestas Uniformes

Define un formato estándar con:

```json
{
  "data": { "id": 1, "name": "Juan" },
  "errors": [],
  "meta": { "requestId": "abc123", "timestamp": "2024-01-15T10:30:00Z" }
}
```

### Cacheo HTTP

El cacheo permite almacenar temporalmente respuestas para reducir carga y mejorar rendimiento.

#### Cache-Control

```http
Cache-Control: public, max-age=3600    # Cacheable por 1 hora
Cache-Control: private, max-age=600    # Solo cliente, 10 minutos
Cache-Control: no-cache               # Validar antes de usar
Cache-Control: no-store              # No cachear nunca
```

#### ETag (Entity Tag)

```http
# Servidor responde:
ETag: "abc123"

# Cliente pregunta:
If-None-Match: "abc123"

# Si no cambió:
HTTP 304 Not Modified
```

### Negociación de Contenido

```http
# Cliente pide formato específico
Accept: application/json
Accept: application/xml

# Servidor responde con:
Content-Type: application/json
```

## 2. GraphQL

GraphQL permite a los clientes solicitar exactamente los datos que necesitan, evitando over-fetching y under-fetching.

### Características principales de GraphQL

- **Flexibilidad**: El cliente define la estructura de la respuesta
- **Un solo endpoint**: No múltiples URLs como REST
- **Tipado fuerte**: Schema bien definido
- **Introspección**: El schema es autodocumentado

### Ejemplo básico

```graphql
type Query {
  user(id: ID!): User
  users(first: Int, after: String): UserConnection
}

type User {
  id: ID!
  name: String!
  email: String
  posts: [Post!]!
}

type Post {
  id: ID!
  title: String!
  content: String
  author: User!
}
```

### Consulta del cliente

```graphql
query GetUser($userId: ID!) {
  user(id: $userId) {
    id
    name
    email
    posts {
      id
      title
    }
  }
}
```

### Cuándo usar GraphQL vs REST

| Aspecto           | GraphQL            | REST                  |
| ----------------- | ------------------ | --------------------- |
| Flexibilidad      | ✅ Alta            | ⚠️ Limitada           |
| Cacheo            | ⚠️ Complejo        | ✅ Simple (HTTP)      |
| Curva aprendizaje | ⚠️ Más pronunciada | ✅ Familiar           |
| Over-fetching     | ✅ Evita           | ❌ Común              |
| Herramientas      | ⚠️ Menos maduras   | ✅ Ecosistema robusto |

## 3. gRPC

gRPC es un framework de comunicación que utiliza HTTP/2 y Protocol Buffers para transmisión eficiente de datos entre servicios.

### Características principales de gRPC

- **Alto rendimiento**: Binary protocol, HTTP/2
- **Contratos fuertes**: Definidos en archivos .proto
- **Streaming**: Unidireccional y bidireccional
- **Multiplataforma**: Soporte para múltiples lenguajes

### Definición del servicio (.proto)

```proto
syntax = "proto3";

service UserService {
  rpc GetUser (UserRequest) returns (UserResponse);
  rpc ListUsers (ListUsersRequest) returns (stream UserResponse);
  rpc CreateUser (CreateUserRequest) returns (UserResponse);
}

message UserRequest {
  string id = 1;
}

message UserResponse {
  string id = 1;
  string name = 2;
  string email = 3;
  int64 created_at = 4;
}

message ListUsersRequest {
  int32 page_size = 1;
  string page_token = 2;
}
```

### Implementación básica

```go
type server struct {
    pb.UnimplementedUserServiceServer
}

func (s *server) GetUser(ctx context.Context, req *pb.UserRequest) (*pb.UserResponse, error) {
    user, err := getUserFromDB(req.Id)
    if err != nil {
        return nil, status.Errorf(codes.NotFound, "usuario no encontrado: %v", err)
    }

    return &pb.UserResponse{
        Id:        user.ID,
        Name:      user.Name,
        Email:     user.Email,
        CreatedAt: user.CreatedAt.Unix(),
    }, nil
}
```

### Tipos de comunicación gRPC

1. **Unario**: Cliente envía una petición, servidor responde una vez
2. **Server Streaming**: Cliente envía una petición, servidor responde múltiples veces
3. **Client Streaming**: Cliente envía múltiples peticiones, servidor responde una vez
4. **Bidirectional Streaming**: Ambos pueden enviar múltiples mensajes

## 4. Webhooks

Un webhook es un "callback HTTP": una URL que tu aplicación expone y que otra aplicación llama automáticamente cuando algo sucede.

### Cómo funcionan

1. Tu app registra una URL para escuchar eventos
2. Otro sistema (Stripe, GitHub, WhatsApp, etc.) envía datos a esa URL cuando ocurre un evento
3. Tu app recibe los datos y ejecuta alguna acción

### Ejemplo de Webhook

```http
POST /webhook/pago HTTP/1.1
Host: tuapp.com
Content-Type: application/json
X-Signature: abc123hmac

{
  "id_pago": "xyz001",
  "estado": "aprobado",
  "monto": 25000,
  "timestamp": "2024-01-15T10:30:00Z"
}
```

### Implementación básica de Webhook

```go
func webhookHandler(w http.ResponseWriter, r *http.Request) {
    // Verificar signature
    signature := r.Header.Get("X-Signature")
    if !verificarSignature(r.Body, signature) {
        http.Error(w, "Signature inválida", http.StatusUnauthorized)
        return
    }

    // Procesar evento
    var evento Evento
    if err := json.NewDecoder(r.Body).Decode(&evento); err != nil {
        http.Error(w, "JSON inválido", http.StatusBadRequest)
        return
    }

    // Procesar de forma asíncrona
    go procesarEvento(evento)

    w.WriteHeader(http.StatusOK)
}
```

### Mejores practicas para webhooks

- **Idempotencia**: Procesa eventos duplicados sin efectos secundarios
- **Verificación**: Siempre verifica signatures/tokens
- **Procesamiento asíncrono**: No bloquees la respuesta HTTP
- **Retry logic**: Implementa reintentos en el lado emisor
- **Logging**: Registra todos los eventos recibidos

## 5. Comunicación en Tiempo Real

Para aplicaciones que requieren actualizaciones instantáneas, comunicación bidireccional o notificaciones en vivo.

### WebSockets

WebSockets proporcionan comunicación bidireccional full-duplex sobre una conexión TCP persistente.

#### Características principales de WebSockets

- **Bidireccional**: Cliente y servidor pueden enviar mensajes en cualquier momento
- **Baja latencia**: No hay overhead de HTTP headers en cada mensaje
- **Persistente**: Conexión se mantiene abierta hasta que se cierre explícitamente
- **Real-time**: Ideal para chat, juegos, trading, colaboración

#### Implementación básica de WebSockets

```go
package main

import (
    "log"
    "net/http"
    "github.com/gorilla/websocket"
)

var upgrader = websocket.Upgrader{
    CheckOrigin: func(r *http.Request) bool {
        return true // En producción, validar origen
    },
}

type Hub struct {
    clients    map[*websocket.Conn]bool
    broadcast  chan []byte
    register   chan *websocket.Conn
    unregister chan *websocket.Conn
}

func (h *Hub) run() {
    for {
        select {
        case conn := <-h.register:
            h.clients[conn] = true
            log.Println("Cliente conectado")

        case conn := <-h.unregister:
            if _, ok := h.clients[conn]; ok {
                delete(h.clients, conn)
                conn.Close()
                log.Println("Cliente desconectado")
            }

        case message := <-h.broadcast:
            for conn := range h.clients {
                err := conn.WriteMessage(websocket.TextMessage, message)
                if err != nil {
                    conn.Close()
                    delete(h.clients, conn)
                }
            }
        }
    }
}

func handleWebSocket(hub *Hub, w http.ResponseWriter, r *http.Request) {
    conn, err := upgrader.Upgrade(w, r, nil)
    if err != nil {
        log.Println("Error upgrading:", err)
        return
    }
    defer conn.Close()

    hub.register <- conn

    for {
        _, message, err := conn.ReadMessage()
        if err != nil {
            hub.unregister <- conn
            break
        }

        // Reenviar mensaje a todos los clientes
        hub.broadcast <- message
    }
}

func main() {
    hub := &Hub{
        clients:    make(map[*websocket.Conn]bool),
        broadcast:  make(chan []byte),
        register:   make(chan *websocket.Conn),
        unregister: make(chan *websocket.Conn),
    }

    go hub.run()

    http.HandleFunc("/ws", func(w http.ResponseWriter, r *http.Request) {
        handleWebSocket(hub, w, r)
    })

    log.Println("Servidor WebSocket en :8080")
    log.Fatal(http.ListenAndServe(":8080", nil))
}
```

#### Cliente JavaScript en WebSockets

```javascript
const ws = new WebSocket("ws://localhost:8080/ws");

ws.onopen = function (event) {
  console.log("Conectado al WebSocket");
  ws.send("Hola servidor!");
};

ws.onmessage = function (event) {
  console.log("Mensaje recibido:", event.data);
  // Actualizar UI con el mensaje
};

ws.onclose = function (event) {
  console.log("Conexión cerrada");
};

ws.onerror = function (error) {
  console.error("Error WebSocket:", error);
};

// Enviar mensaje
function enviarMensaje(mensaje) {
  if (ws.readyState === WebSocket.OPEN) {
    ws.send(mensaje);
  }
}
```

### Server-Sent Events (SSE)

SSE permite que el servidor envíe datos al cliente de forma unidireccional sobre HTTP.

#### Características principales SSE

- **Unidireccional**: Solo servidor → cliente
- **HTTP estándar**: No requiere protocolo especial
- **Reconexión automática**: El navegador reconecta automáticamente
- **Simple**: Más fácil de implementar que WebSockets para notificaciones

#### Implementación basica de SSE

```go
func sseHandler(w http.ResponseWriter, r *http.Request) {
    // Headers para SSE
    w.Header().Set("Content-Type", "text/event-stream")
    w.Header().Set("Cache-Control", "no-cache")
    w.Header().Set("Connection", "keep-alive")
    w.Header().Set("Access-Control-Allow-Origin", "*")

    // Crear flusher para enviar datos inmediatamente
    flusher, ok := w.(http.Flusher)
    if !ok {
        http.Error(w, "Streaming no soportado", http.StatusInternalServerError)
        return
    }

    // Canal para detectar si el cliente se desconecta
    notify := r.Context().Done()

    for {
        select {
        case <-notify:
            log.Println("Cliente desconectado")
            return
        case <-time.After(5 * time.Second):
            // Enviar evento cada 5 segundos
            evento := fmt.Sprintf("data: Timestamp: %s\n\n", time.Now().Format(time.RFC3339))
            fmt.Fprint(w, evento)
            flusher.Flush()
        }
    }
}

// Enviar evento personalizado
func enviarEvento(w http.ResponseWriter, eventType, data string) {
    fmt.Fprintf(w, "event: %s\n", eventType)
    fmt.Fprintf(w, "data: %s\n\n", data)
    if f, ok := w.(http.Flusher); ok {
        f.Flush()
    }
}
```

#### Cliente JavaScript en SSE

```javascript
const eventSource = new EventSource("/events");

eventSource.onopen = function (event) {
  console.log("Conexión SSE abierta");
};

eventSource.onmessage = function (event) {
  console.log("Mensaje recibido:", event.data);
  // Actualizar UI
};

// Escuchar eventos personalizados
eventSource.addEventListener("notification", function (event) {
  console.log("Notificación:", event.data);
});

eventSource.onerror = function (event) {
  console.error("Error SSE:", event);
};

// Cerrar conexión
// eventSource.close();
```

### Socket.IO (Abstracción de WebSockets)

Socket.IO es una biblioteca que abstrae WebSockets con fallbacks automáticos.

#### Características principales DE Socket.IO

- **Fallbacks automáticos**: Long polling si WebSockets no está disponible
- **Rooms y namespaces**: Organización lógica de conexiones
- **Reconexión automática**: Manejo robusto de desconexiones
- **Broadcasting**: Envío a múltiples clientes fácilmente

#### Ejemplo conceptual

```go
type Room struct {
    name    string
    clients map[string]*websocket.Conn
}

type SocketServer struct {
    rooms map[string]*Room
}

func (s *SocketServer) JoinRoom(clientID, roomName string, conn *websocket.Conn) {
    if s.rooms[roomName] == nil {
        s.rooms[roomName] = &Room{
            name:    roomName,
            clients: make(map[string]*websocket.Conn),
        }
    }
    s.rooms[roomName].clients[clientID] = conn
}

func (s *SocketServer) BroadcastToRoom(roomName string, message []byte) {
    if room, exists := s.rooms[roomName]; exists {
        for _, conn := range room.clients {
            conn.WriteMessage(websocket.TextMessage, message)
        }
    }
}
```

### WebRTC (Comunicación Peer-to-Peer)

Para comunicación directa entre navegadores sin pasar por el servidor.

#### Características

- **P2P directo**: Comunicación cliente a cliente
- **Multimedia**: Audio, video, datos
- **Baja latencia**: No hay servidor intermedio
- **NAT traversal**: Manejo automático de firewalls/NAT

#### Casos de uso

- Videollamadas
- Juegos P2P
- Transferencia de archivos
- Streaming de pantalla

### Comparación de tecnologías en tiempo real

| Tecnología   | Dirección        | Complejidad | Casos de uso ideales                   |
| ------------ | ---------------- | ----------- | -------------------------------------- |
| WebSockets   | Bidireccional    | Media       | Chat, juegos, colaboración tiempo real |
| SSE          | Servidor→Cliente | Baja        | Notificaciones, feeds, dashboards      |
| Socket.IO    | Bidireccional    | Media       | Aplicaciones complejas, fallbacks      |
| WebRTC       | P2P              | Alta        | Videollamadas, juegos P2P              |
| Long Polling | Cliente→Servidor | Baja        | Fallback para navegadores antiguos     |

### Cuándo usar cada tecnología

- **WebSockets**

  - ✅ Chat en tiempo real
  - ✅ Juegos multijugador
  - ✅ Editores colaborativos
  - ✅ Trading/bolsa de valores
  - ❌ Notificaciones simples (usar SSE)

- **Server-Sent Events**

  - ✅ Feeds de noticias
  - ✅ Notificaciones push
  - ✅ Dashboards en vivo
  - ✅ Progreso de tareas
  - ❌ Comunicación bidireccional (usar WebSockets)

- **WebRTC**

  - ✅ Videollamadas
  - ✅ Compartir pantalla
  - ✅ Juegos P2P
  - ✅ Transferencia directa de archivos
  - ❌ Comunicación con servidor (usar WebSockets)

## 6. Comunicación en Microservicios

En arquitecturas de microservicios, los servicios deben comunicarse de manera eficiente y resiliente.

### Patrones de comunicación

#### Síncrona

- **REST APIs**: Simple, basado en HTTP
- **gRPC**: Alto rendimiento, tipado fuerte
- **GraphQL**: Flexibilidad en consultas

#### Asíncrona

- **Message Queues**: RabbitMQ, Apache Kafka
- **Event Streaming**: Apache Kafka, AWS Kinesis
- **Pub/Sub**: Redis, Google Pub/Sub

### Cuándo usar cada patrón

| Patrón          | Sincronía | Ideal para                             | Ejemplo de uso                     |
| --------------- | --------- | -------------------------------------- | ---------------------------------- |
| REST            | ✔️        | Interfaces públicas, simple consumo    | API pública, operaciones CRUD      |
| gRPC            | ✔️        | Comunicación interna eficiente         | Microservicios internos            |
| GraphQL         | ✔️        | Clientes diversos, consultas flexibles | Apps móviles, SPAs                 |
| Message Queues  | ❌        | Procesamiento en background            | Envío emails, procesamiento imgs   |
| Event Streaming | ❌        | Eventos en tiempo real                 | Logs, métricas, analytics          |
| Redis Pub/Sub   | ❌        | Notificaciones internas rápidas        | Cache invalidation, notificaciones |

---

## 6. Patrones de Mensajería

### Message Queues (Colas de Mensajes)

Ideal para desacoplar servicios y garantizar procesamiento de tareas.

#### RabbitMQ

```go
// Publicar mensaje
ch.Publish(
    "",     // exchange
    "cola_email", // routing key
    false,  // mandatory
    false,  // immediate
    amqp.Publishing{
        ContentType: "application/json",
        Body:        []byte(`{"email": "user@example.com", "template": "welcome"}`),
    })

// Consumir mensajes
msgs, _ := ch.Consume(
    "cola_email", // queue
    "",          // consumer
    true,        // auto-ack
    false,       // exclusive
    false,       // no-local
    false,       // no-wait
    nil,         // args
)

for msg := range msgs {
    enviarEmail(msg.Body)
}
```

### Event Streaming

Para procesamiento de eventos en tiempo real y analytics.

#### Apache Kafka

```go
// Productor
producer := kafka.NewWriter(kafka.WriterConfig{
    Brokers: []string{"localhost:9092"},
    Topic:   "user-events",
})

producer.WriteMessages(context.Background(),
    kafka.Message{
        Key:   []byte("user-123"),
        Value: []byte(`{"event": "user_registered", "user_id": "123"}`),
    },
)

// Consumidor
reader := kafka.NewReader(kafka.ReaderConfig{
    Brokers: []string{"localhost:9092"},
    Topic:   "user-events",
    GroupID: "email-service",
})

for {
    msg, err := reader.ReadMessage(context.Background())
    if err != nil {
        continue
    }
    procesarEvento(msg.Value)
}
```

### Redis Pub/Sub

Para notificaciones ligeras y comunicación en tiempo real.

```go
// Publicador
rdb.Publish(ctx, "notificaciones", "Nuevo usuario registrado")

// Suscriptor
sub := rdb.Subscribe(ctx, "notificaciones")
ch := sub.Channel()

for msg := range ch {
    fmt.Println("Mensaje recibido:", msg.Payload)
    notificarUsuarios(msg.Payload)
}
```

## 🎯 Resumen de Recomendaciones

### Para APIs públicas

- **REST** con OpenAPI/Swagger para documentación
- Implementa cacheo HTTP, paginación y filtros
- Usa códigos de estado HTTP correctos

### Para comunicación entre microservicios

- **gRPC** para comunicación interna eficiente
- **Event streaming** (Kafka) para eventos importantes
- **Redis Pub/Sub** para notificaciones rápidas

### Para aplicaciones en tiempo real

- **WebSockets** para conexiones persistentes
- **Server-Sent Events** para notificaciones unidireccionales
- **GraphQL subscriptions** para actualizaciones reactivas

### Monitoreo y observabilidad

- Implementa logging estructurado
- Usa distributed tracing (Jaeger, Zipkin)
- Métricas de latencia, throughput y errores
- Health checks para todos los servicios
