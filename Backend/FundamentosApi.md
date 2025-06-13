# Fundamentos API / Microservicios

## 1. API Management

🔹 **Por qué:** Vas a construir APIs REST/GraphQL para tus microservicios.  
🔹 Debes entender cómo diseñarlas, documentarlas (Swagger/OpenAPI), versionarlas y protegerlas.  
🔹 **Herramientas:**

- Postman
- OpenAPI (Swagger)
- Mulesoft _(usado en grandes empresas)_
- Apigee (Google Cloud)
- AWS API Gateway

```yaml
# openapi.yaml
paths:
  /api/v1/users/{id}:
    get:
      summary: Get user by ID
      responses:
        "200":
          description: Successful response
```

## 2. Service Registration & Discovery

🔹 **Por qué:** En sistemas distribuidos, los servicios deben encontrarse entre sí dinámicamente.  
🔹 Es crucial en ambientes con _scaling dinámico_ o _serverless_.  
🔹 **Ejemplos:**

- Netflix Eureka _(legado)_
- HashiCorp Consul
- Kubernetes Service Discovery _(preferido actualmente)_

```yaml
# service.yaml (Kubernetes)
apiVersion: v1
kind: Service
metadata:
  name: auth-service
spec:
  selector:
    app: auth
  ports:
    - protocol: TCP
      port: 80
      targetPort: 8080
```

## 3. Application Gateway

🔹 **Por qué:** Es clave entender cómo el tráfico entra a tus servicios, cómo se enruta y cómo se aplican políticas de autenticación/autorización.  
🔹 **Ejemplos:**

- Ocelot
- Kong
- Istio
- NGINX (como reverse proxy)
- AWS API Gateway

```yaml
# Declaración en Kong (API declarativa)
routes:
  - name: user-route
    paths:
      - /users
    service:
      name: user-service
```

## 4. Load Balancer

🔹 **Por qué:** Necesitas garantizar alta disponibilidad y escalabilidad horizontal de tus servicios.  
🔹 **Ejemplos:**

- NGINX
- Traefik
- Kubernetes Services (con balanceo interno)

```yaml
# traefik-dynamic-config.yaml
http:
  routers:
    my-service:
      rule: "Host(`myapp.com`)"
      service: my-service

  services:
    my-service:
      loadBalancer:
        servers:
          - url: "http://10.0.0.1"
          - url: "http://10.0.0.2"
```

## 5. Distributed Tracing

🔹 **Por qué:** Entender el flujo completo de una solicitud entre servicios ayuda en debugging, optimización y visibilidad.  
🔹 **Herramientas:**

- OpenTelemetry
- Jaeger
- Zipkin

```go
// Instrumentación con OpenTelemetry en Go
import "go.opentelemetry.io/otel"

tracer := otel.Tracer("my-service")
ctx, span := tracer.Start(context.Background(), "handle-request")
defer span.End()
```

## 6. Monitoring & Alerting

🔹 **Por qué:** Aunque DevOps puede encargarse de esto, tú debes saber qué métricas exponer y cómo visualizar errores o cuellos de botella.  
🔹 **Herramientas:**

- Prometheus
- Grafana
- ELK Stack (Elasticsearch, Logstash, Kibana)

```go
// Exponer métricas en Go para Prometheus
import "github.com/prometheus/client_golang/prometheus"

var httpRequests = prometheus.NewCounter(
  prometheus.CounterOpts{
    Name: "http_requests_total",
    Help: "Número de solicitudes HTTP",
})

prometheus.MustRegister(httpRequests)

http.Handle("/metrics", promhttp.Handler())
```
