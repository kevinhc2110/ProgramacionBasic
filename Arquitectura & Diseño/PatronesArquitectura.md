# Patrones de arquitectura de software

Los patrones de arquitectura de software son soluciones reutilizables y probadas para estructurar sistemas de software. No son código, sino esquemas o plantillas que guían cómo organizar los componentes del software, cómo se comunican entre sí y cómo se distribuyen las responsabilidades.

## 1. Clean Architecture (Arquitectura Limpia)

**Ideal para:** Backend sólido, mantenible y testeable.

**Ventajas:**

- Código desacoplado.
- Fácil de testear.
- Independencia de frameworks, bases de datos, y detalles externos.

**Aplicable en:** Go, Python (FastAPI), TypeScript (NestJS).

```cssharp
project-root/
│
├── cmd/                    # Entrada principal (Go)
│   └── main.go
│
├── internal/               # Lógica interna (no expuesta)
│   ├── domain/             # Entidades del negocio
│   ├── usecases/           # Casos de uso / lógica de negocio
│   ├── interfaces/         # Interfaces de repositorios/servicios
│   └── infra/              # Implementaciones concretas (DB, APIs)
│       ├── repository/
│       └── external/
│
├── api/                    # Adaptadores HTTP, gRPC, CLI
│   ├── handlers/
│   ├── routes/
│   └── middleware/
│
├── config/                 # Configuración de app/env
├── tests/                  # Pruebas unitarias e integración
├── go.mod / pyproject.toml / package.json
└── README.md
```

## 2. Hexagonal Architecture (Ports and Adapters)

**Ideal para:** Aplicaciones que interactúan con múltiples servicios externos (bases de datos, APIs, etc).

**Ventajas:**

- Desacoplamiento entre lógica de negocio y servicios externos.
- Facilita las pruebas unitarias.
- Flexible ante cambios de infraestructura.

**Muy popular en:** Go.

```csharp
project-root/
│
├── app/                    # Lógica de negocio (core)
│   ├── domain/             # Entidades, modelos
│   └── service/            # Casos de uso
│
├── ports/                  # Interfaces (puertos) que necesita el core
│   ├── inbound/            # Interfaces de entrada (controller, CLI, etc.)
│   └── outbound/           # Interfaces de salida (DB, APIs externas)
│
├── adapters/               # Adaptadores concretos
│   ├── http/               # Servidor HTTP
│   ├── db/                 # Repositorio de base de datos
│   └── external/           # APIs externas
│
├── config/
├── tests/
└── main.ts / main.go / main.py
```

## 3. Microservices Architecture

**Ideal para:** Sistemas distribuidos que necesitan escalar o evolucionar de forma independiente.

**Ventajas:**

- Servicios independientes.
- Posibilidad de usar múltiples tecnologías.
- Escalabilidad horizontal.

**Requiere conocimientos de:** Docker, Kubernetes, comunicación por APIs/gRPC, observabilidad.

```csharp
project-root/
│
├── services/
│   ├── users/
│   │   ├── src/
│   │   │   ├── controllers/
│   │   │   ├── services/
│   │   │   ├── models/
│   │   │   ├── routes/
│   │   │   └── index.ts
│   │   └── Dockerfile
│
│   ├── orders/
│   ├── auth/
│   └── payments/
│
├── gateway/                # API Gateway (opcional)
│   ├── routes/
│   └── index.ts
│
├── docker-compose.yml
├── infra/                  # Infraestructura, deploy scripts
└── README.md
```

## 4. Event-Driven Architecture

**Ideal para:** Sistemas que responden a eventos en tiempo real o flujos asíncronos.

**Ventajas:**

- Alta escalabilidad.
- Bajo acoplamiento entre componentes.
- Ideal para flujos de procesamiento de datos o IA.

**Tecnologías comunes:** Kafka, RabbitMQ, Redis Streams, NATS.

```csharp
project-root/
│
├── producers/              # Publicadores de eventos
│   ├── order_created_producer/
│   └── email_notifier/
│
├── consumers/              # Consumidores de eventos
│   ├── order_handler/
│   └── inventory_updater/
│
├── events/                 # Definiciones de eventos
│   ├── order_created.ts
│   └── product_reserved.ts
│
├── shared/                 # Utilidades comunes (config, logger, etc.)
├── infra/                  # Kafka/RabbitMQ/Redis setup
└── README.md
```

## 5. Serverless Architecture

**Ideal para:** Tareas asíncronas, funciones IA, APIs ligeras, jobs programados.

**Ventajas:**

- No necesitas gestionar servidores.
- Escalabilidad automática.
- Pago por uso.

**Plataformas:** AWS Lambda, Google Cloud Functions, Azure Functions.

```csharp
project-root/
│
├── functions/
│   ├── createUser/
│   │   └── handler.ts
│   ├── processPayment/
│   └── sendNotification/
│
├── shared/                 # Utils, middlewares
├── config/                 # Environment settings
├── tests/
├── serverless.yml / func.yaml
└── package.json / requirements.txt
```

## 6. Data-centric / ML Pipeline Architecture

**Ideal para:** Proyectos de IA y ciencia de datos en producción.

**Componentes:**

- Ingesta de datos.
- Preprocesamiento.
- Entrenamiento de modelos.
- Inferencia (serving).
- Monitoreo.

**Herramientas comunes:** MLFlow, Airflow, DVC, FastAPI, Kubeflow.

```csharp
project-root/
│
├── data/
│   ├── raw/                # Datos sin procesar
│   ├── processed/          # Datos limpios y transformados
│   └── external/           # Datos importados de fuentes externas
│
├── notebooks/              # Jupyter notebooks (EDA, experimentos)
│
├── src/
│   ├── data_ingestion/     # Scripts para recolectar datos
│   ├── data_preprocessing/ # Limpieza, normalización, feature eng.
│   ├── model_training/     # Entrenamiento del modelo
│   ├── model_evaluation/   # Evaluación de métricas
│   ├── model_serving/      # Deploy del modelo (FastAPI, Flask, etc.)
│   └── utils/              # Funciones auxiliares
│
├── models/                 # Modelos serializados (.pkl, .h5, etc.)
├── reports/                # Resultados, gráficos, logs
├── config/                 # Parámetros, experiment tracking
├── requirements.txt / pyproject.toml
└── README.md
```

## 7. Layered Architecture (Arquitectura por Capas)

**Ideal para:** Aplicaciones pequeñas, CRUDs o aprendizaje inicial.

**Capas típicas:**

- Controlador (Controller)
- Servicio (Service)
- Repositorio (Repository)
- Base de datos (DB)

**Ventajas:**

- Buena separación lógica.
- Base para aprender patrones de diseño comunes.

```csharp
project-root/
│
├── presentation/           # Capa de presentación (API, HTTP handlers)
│   └── controllers/
│
├── application/            # Lógica de aplicación / servicios
│   └── services/
│
├── domain/                 # Entidades del dominio (negocio)
│   ├── models/
│   └── interfaces/
│
├── infrastructure/         # Infraestructura (ORM, DB, Redis, etc.)
│   ├── repositories/
│   ├── database/
│   └── external_services/
│
├── config/                 # Configuraciones y constantes
├── tests/                  # Unitarios e integración
├── main.go / app.ts / app.py
└── README.md
```

## 8. Modular Architecture (Arquitectura Modular)

**Ideal para:** Aplicaciones medianas a grandes, equipos escalables, microservicios o dominios bien definidos.

**Organización:** Por módulo o feature (usuarios, productos, órdenes, etc.), cada uno con su lógica encapsulada.

**Ventajas:**

- Alta cohesión y bajo acoplamiento.
- Escalable, fácil de mantener y probar por separado.
- Posible evolución hacia microservicios.

```csharp
project-root/
│
├── modules/                      # Todos los módulos del sistema
│   ├── users/                    # Módulo de usuarios
│   │   ├── controller.ts         # Capa de presentación del módulo
│   │   ├── service.ts            # Lógica de negocio del módulo
│   │   ├── repository.ts         # Interacción con DB
│   │   ├── model.ts              # Entidad o esquema
│   │   └── routes.ts             # Rutas específicas del módulo
│   │
│   ├── products/                 # Otro módulo (productos)
│   │   ├── controller.ts
│   │   ├── service.ts
│   │   ├── repository.ts
│   │   ├── model.ts
│   │   └── routes.ts
│   │
│   └── ...                       # Más módulos
│
├── shared/                       # Código compartido (utils, middlewares, constantes)
│   ├── middleware/
│   ├── utils/
│   └── types/
│
├── config/                       # Configuración global
│   └── env.ts / env.py / env.go
│
├── database/                     # Conexiones, migraciones, seeds
│
├── tests/                        # Pruebas unitarias e integración
│
├── main.ts / main.go / app.py    # Entry point
└── README.md
```

## Recomendación por Nivel

| Prioridad | Arquitectura                  | ¿Por qué?                                      |
| --------- | ----------------------------- | ---------------------------------------------- |
| ⭐⭐⭐    | **Clean Architecture**        | Base sólida, separa lógica de infraestructura. |
| ⭐⭐      | **Hexagonal**                 | Te prepara para testing e integración real.    |
| ⭐⭐      | **Event-Driven**              | Escalable y común en IA/backend modernos.      |
| ⭐⭐      | **ML Pipelines / Serverless** | Útil en producción de IA y backend moderno.    |
| ⭐        | **Microservicios**            | Apréndelo una vez domines las bases.           |
