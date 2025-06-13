# Microservicios

La arquitectura de microservicios divide una aplicación en servicios pequeños, independientes y desplegables de manera autónoma. Go es una excelente elección para construir microservicios debido a su eficiencia, soporte de concurrencia y facilidad para crear servicios de alto rendimiento.

## Ventajas de los Microservicios

- **Escalabilidad:** Cada microservicio puede escalarse de forma independiente según la demanda.
- **Mantenibilidad:** Código más modular y fácil de mantener.
- **Despliegue Independiente**: Permite actualizaciones y despliegues sin afectar todo el sistema.
- **Tecnologías Heterogéneas:** Diferentes microservicios pueden estar escritos en distintos lenguajes o usar diferentes tecnologías.

## Comunicación entre Microservicios

En una arquitectura de microservicios, los servicios deben comunicarse de manera eficiente. Esta sección describe los principales mecanismos utilizados: REST, gRPC, mensajería asincrónica y Redis Pub/Sub.

### 🌐 RESTful APIs

La comunicación mediante REST utiliza el protocolo HTTP. Es ampliamente adoptada y fácil de integrar desde casi cualquier cliente.

#### Ventajas de RESTful APIs

- Simplicidad y legibilidad
- Basado en estándares
- Fácil de testear con herramientas como Postman o cURL

```go
e.GET("/usuarios/:id", obtenerUsuario)

func obtenerUsuario(c echo.Context) error {
    id := c.Param("id")
    usuario := buscarUsuarioPorID(id)
    return c.JSON(http.StatusOK, usuario)
}
```

### ⚡ gRPC

gRPC es un sistema de comunicación basado en HTTP/2 y Protocol Buffers. Ideal para comunicación entre servicios internos donde el rendimiento y la eficiencia son críticos.

#### Ventajas de gRPC

- Alta eficiencia y bajo consumo de ancho de banda
- Contratos fuertes con `.proto`
- Streaming bidireccional

```proto
  service UsuarioService {
      rpc ObtenerUsuario(UsuarioRequest) returns (UsuarioResponse);
  }

  message UsuarioRequest {
      string id = 1;
  }

  message UsuarioResponse {
      string nombre = 1;
      string correo = 2;
  }
```

### Mensajería Asíncrona

Permite desacoplar servicios mediante el uso de eventos y colas de mensajes. Los productores envían eventos a un sistema intermedio y los consumidores los procesan de forma independiente.

#### Ventajas de Mensajería Asíncrona

- Alta escalabilidad
- Tolerancia a fallos
- Procesamiento distribuido

#### Tecnologías comunes

- Kafka
- RabbitMQ
- NATS

```go
nc, _ := nats.Connect(nats.DefaultURL)
nc.Subscribe("orden.creada", func(m *nats.Msg) {
    fmt.Printf("Orden recibida: %s\n", string(m.Data))
})
```

### Redis Pub/Sub

Redis permite publicar y suscribirse a canales de mensajes. Es útil para sistemas en tiempo real o notificaciones internas rápidas.

### Ventajas de Redis Pub/Sub

- Baja latencia
- Fácil de implementar
- Ligero para notificaciones en tiempo real

```go
// Publicador
rdb.Publish(ctx, "notificaciones", "Nuevo usuario registrado")

// Suscriptor
sub := rdb.Subscribe(ctx, "notificaciones")
ch := sub.Channel()

for msg := range ch {
    fmt.Println("Mensaje recibido:", msg.Payload)
}
```

### Cuándo usar cada uno

| Mecanismo      | Sincronía | Ideal para                          |
| -------------- | --------- | ----------------------------------- |
| REST           | ✔️        | Interfaces públicas, simple consumo |
| gRPC           | ✔️        | Comunicación interna eficiente      |
| Kafka/RabbitMQ | ❌        | Eventos, colas, desacoplamiento     |
| Redis Pub/Sub  | ❌        | Notificaciones internas rápidas     |
