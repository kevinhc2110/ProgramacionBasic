# YAML

Una guía exhaustiva sobre YAML (YAML Ain't Markup Language), desde sintaxis básica hasta casos de uso avanzados en DevOps, configuración y CI/CD.

## 1. Fundamentos de YAML

### ¿Qué es YAML?

YAML es un formato de serialización de datos legible por humanos, comúnmente usado para:

- **Archivos de configuración** (Docker Compose, Kubernetes, Ansible)
- **CI/CD pipelines** (GitHub Actions, GitLab CI, Jenkins)
- **APIs y intercambio de datos** (alternativa a JSON/XML)
- **Documentación estructurada** (OpenAPI, Swagger)

### Características principales

| Característica | Descripción                                 | Ejemplo                |
| -------------- | ------------------------------------------- | ---------------------- |
| Legible        | Sintaxis clara y fácil de leer              | `name: "Juan Pérez"`   |
| Indentación    | Usa espacios para jerarquía (NO tabs)       | `items:`               |
| Case-sensitive | Distingue mayúsculas y minúsculas           | `Name ≠ name`          |
| Unicode        | Soporte completo para caracteres especiales | `título: "Niño con ñ"` |

### YAML vs otros formatos

| Aspecto     | YAML            | JSON           | XML         |
| ----------- | --------------- | -------------- | ----------- |
| Legibilidad | ✅ Muy alta     | ⚠️ Media       | ❌ Baja     |
| Comentarios | ✅ Soporta      | ❌ No soporta  | ✅ Soporta  |
| Multilinea  | ✅ Nativo       | ⚠️ Con escapes | ✅ Soporta  |
| Parsing     | ⚠️ Más complejo | ✅ Simple      | ⚠️ Complejo |
| Tamaño      | ✅ Compacto     | ✅ Compacto    | ❌ Verboso  |

## 2. Sintaxis Básica

### Reglas fundamentales

```yaml
# Esto es un comentario
# YAML es case-sensitive y usa indentación con ESPACIOS (no tabs)

# Clave-valor básico
nombre: Juan
edad: 30
activo: true

# Los dos puntos DEBEN tener un espacio después
correcto: valor
# incorrecto:valor  # ❌ Error de sintaxis
```

### Indentación y estructura

```yaml
# La indentación define la jerarquía
padre:
  hijo1: valor1
  hijo2: valor2
  hijo_con_hijos:
    nieto1: valor_nieto1
    nieto2: valor_nieto2

# Todos los elementos al mismo nivel deben tener la misma indentación
personas:
  - nombre: Ana
    edad: 25
  - nombre: Carlos
    edad: 32
```

### Comentarios

```yaml
# Comentario de línea completa

nombre: Juan # Comentario al final de línea

# Los comentarios pueden estar en cualquier lugar
# y son ignorados completamente por el parser

# Comentario multilinea:
# Se puede hacer usando múltiples líneas
# con # al inicio de cada una
```

### Valores especiales

```yaml
# Valores nulos
valor_nulo: null
valor_vacio: ~
sin_valor:

# Booleanos (case-insensitive)
verdadero1: true
verdadero2: True
verdadero3: TRUE
verdadero4: yes
verdadero5: on

falso1: false
falso2: False
falso3: FALSE
falso4: no
falso5: off
```

## 3. Tipos de Datos

### Escalares (valores simples)

```yaml
# Strings (cadenas de texto)
nombre_simple: Juan
nombre_con_espacios: Juan Pérez
nombre_entre_comillas: "Juan Pérez"
nombre_comillas_simples: "Juan Pérez"

# Números
entero: 42
flotante: 3.14159
notacion_cientifica: 1.2e+6
octal: 0o755
hexadecimal: 0xFF

# Fechas y timestamps
fecha: 2024-12-31
fecha_con_hora: 2024-12-31T23:59:59Z
timestamp: 2024-12-31 23:59:59.999 +02:00
```

### Strings multilinea

```yaml
# Literal (preserva saltos de línea) - usar |
descripcion_literal: |
  Esta es una descripción
  que mantiene los saltos de línea
  exactamente como están escritos.

  Incluso respeta líneas vacías.

# Folded (convierte saltos en espacios) - usar >
descripcion_folded: >
  Esta es una descripción
  que convierte los saltos de línea
  en espacios, creando un párrafo
  continuo.

# Con indicadores de comportamiento
script_con_newline: |+
  #!/bin/bash
  echo "Hola mundo"

# El + mantiene el salto de línea final
texto_sin_newline: |-
  Primera línea
  Segunda línea

# El - elimina el salto de línea final
```

### Listas (arrays)

```yaml
# Lista simple
frutas:
  - manzana
  - banana
  - naranja

# Lista en línea
colores: [rojo, verde, azul]

# Lista de objetos
empleados:
  - nombre: Ana
    puesto: Desarrolladora
    salario: 50000
  - nombre: Carlos
    puesto: Designer
    salario: 45000

# Lista anidada
departamentos:
  - nombre: IT
    empleados:
      - Ana
      - Carlos
  - nombre: Marketing
    empleados:
      - Diana
      - Eduardo
```

### Objetos (mapas/diccionarios)

```yaml
# Objeto simple
persona:
  nombre: Juan
  edad: 30
  email: juan@email.com

# Objeto en línea
coordenadas: { x: 10, y: 20, z: 30 }

# Objetos anidados
empresa:
  nombre: "Tech Corp"
  direccion:
    calle: "Av. Principal 123"
    ciudad: "Ciudad"
    codigo_postal: "12345"
  empleados:
    - nombre: Ana
      departamento: IT
    - nombre: Carlos
      departamento: Marketing
```

## 4. Estructuras Complejas

### Anclas y referencias (&, \*)

```yaml
# Definir ancla con &
defaults: &default_settings
  timeout: 30
  retries: 3
  debug: false

# Usar referencia con *
desarrollo:
  <<: *default_settings # Merge
  debug: true # Override

produccion:
  <<: *default_settings
  timeout: 60 # Override

# Resultado efectivo:
# desarrollo: { timeout: 30, retries: 3, debug: true }
# produccion: { timeout: 60, retries: 3, debug: false }
```

### Merge keys (<<)

```yaml
# Template base
base_config: &base
  memoria: "512Mi"
  cpu: "100m"
  replicas: 1

# Servicios que heredan y modifican
api_service:
  <<: *base
  replicas: 3
  puerto: 8080

worker_service:
  <<: *base
  memoria: "1Gi"
  cpu: "500m"

# Múltiples merges
frontend:
  <<: [*base, *ssl_config]  # Merge múltiples anclas
  puerto: 3000
```

### Tipos de datos complejos

```yaml
# Sets (conjuntos únicos)
etiquetas: !!set
  ? tag1
  ? tag2
  ? tag3

# Pairs ordenados
conexiones: !!pairs
  - input: output1
  - input: output2

# Timestamp explícito
created_at: !!timestamp 2024-01-15T10:30:00Z

# Binary data
imagen: !!binary |
  R0lGODdhDQAIAIAAAAAAANn
  Z2dmttqmxs6u4uqKuqLa4uKqfr
  1BKCtqmxs6u4uqKuqLa4uKqfr
```

### Documentos múltiples

```yaml
# Primer documento
apiVersion: v1
kind: ConfigMap
metadata:
  name: config1
data:
  key1: value1


# Segundo documento
apiVersion: v1
kind: Secret
metadata:
  name: secret1
data:
  password: cGFzc3dvcmQ=


# Tercer documento
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-app
spec:
  replicas: 3
```

## 5. Mejores prácticas

### Estructura y organización

```yaml
# ✅ Buenas prácticas de estructura
apiVersion: v1
kind: ConfigMap
metadata:
  # Nombres descriptivos y consistentes
  name: web-app-config
  namespace: production
  labels:
    app: web-app
    component: config
    version: "1.0"
  annotations:
    description: "Configuración para la aplicación web"
    last-updated: "2024-01-15"

data:
  # Agrupar configuraciones relacionadas
  database.yaml: |
    host: postgres.database.svc.cluster.local
    port: 5432
    pool:
      min: 5
      max: 20
      timeout: 30s

  cache.yaml: |
    redis:
      host: redis.cache.svc.cluster.local
      port: 6379
      ttl: 3600
```

### Manejo de secretos

```yaml
# ❌ Nunca hagas esto
database:
  password: "mi_password_secreto"  # Nunca en texto plano

# ✅ Usa referencias a secretos
database:
  password:
    valueFrom:
      secretKeyRef:
        name: db-secret
        key: password

# ✅ O variables de entorno
database:
  password: ${DATABASE_PASSWORD}

# ✅ Para Docker Compose
database:
  environment:
    - POSTGRES_PASSWORD_FILE=/run/secrets/db_password
  secrets:
    - db_password
```

### Reutilización con anclas

```yaml
# ✅ Define templates reutilizables
x-logging: &default-logging
  driver: "json-file"
  options:
    max-size: "10m"
    max-file: "3"

x-healthcheck: &default-healthcheck
  interval: 30s
  timeout: 10s
  retries: 3
  start_period: 40s

x-deploy: &default-deploy
  restart_policy:
    condition: on-failure
    delay: 5s
    max_attempts: 3

# ✅ Aplica templates consistentemente
services:
  api:
    image: myapp/api:latest
    logging: *default-logging
    healthcheck:
      <<: *default-healthcheck
      test: ["CMD", "curl", "-f", "http://localhost:3000/health"]
    deploy: *default-deploy

  worker:
    image: myapp/worker:latest
    logging: *default-logging
    healthcheck:
      <<: *default-healthcheck
      test:
        [
          "CMD",
          "python",
          "-c",
          "import requests; requests.get('http://localhost:5000/health')",
        ]
    deploy: *default-deploy
```

### Documentación y comentarios

```yaml
# ✅ Documenta configuraciones complejas
services:
  database:
    image: postgres:15
    environment:
      # Configuración de base de datos para producción
      # Nota: pool_size debe ajustarse según la carga esperada
      POSTGRES_DB: ${DB_NAME}
      POSTGRES_USER: ${DB_USER}
      POSTGRES_PASSWORD_FILE: /run/secrets/db_password
    volumes:
      # Datos persistentes
      - postgres_data:/var/lib/postgresql/data
      # Scripts de inicialización
      - ./migrations:/docker-entrypoint-initdb.d/
    command: |
      postgres
      -c max_connections=100
      -c shared_buffers=256MB
      -c effective_cache_size=1GB
      -c maintenance_work_mem=64MB
      -c checkpoint_completion_target=0.9
      -c wal_buffers=16MB
      -c default_statistics_target=100
```

### Validación y tipos

```yaml
# ✅ Usa tipos explícitos cuando sea necesario
metadata:
  labels:
    # Fuerza string para valores numéricos que deben ser strings
    version: "1.0"
    port: "8080"
    # Bool explícito
    enabled: !!bool "true"
  annotations:
    # Timestamp explícito
    created: !!timestamp "2024-01-15T10:30:00Z"
    # Integer explícito
    replicas: !!int "3"

# ✅ Valida ranges y constraints
resources:
  requests:
    memory: "256Mi" # Usa unidades explícitas
    cpu: "100m" # Usa millicores
  limits:
    memory: "512Mi" # Siempre mayor que requests
    cpu: "500m"
```

### Performance y optimización

```yaml
# ✅ Optimiza para performance
services:
  app:
    image: myapp:latest
    # Usa init para manejo correcto de señales
    init: true
    # Configura límites de recursos apropiados
    deploy:
      resources:
        limits:
          memory: 512M
          cpus: "0.5"
        reservations:
          memory: 256M
          cpus: "0.25"
    # Usa restart policies inteligentes
    restart: unless-stopped
    # Configura healthchecks eficientes
    healthcheck:
      test: ["CMD", "curl", "-f", "http://localhost:3000/health"]
      interval: 30s
      timeout: 10s
      retries: 3
      start_period: 40s
```

## 6. Herramientas y Validación

### Herramientas de línea de comandos

```bash
# yamllint - Linter para YAML
pip install yamllint
yamllint config.yml

# yq - Procesador de YAML como jq para JSON
# Instalar: https://github.com/mikefarah/yq
yq eval '.services.web.ports[0]' docker-compose.yml

# Validación con schemas
pip install pykwalify
pykwalify -d docker-compose.yml -s docker
```
