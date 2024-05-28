# Paquetes en Go

En Go, los paquetes son una forma de organizar y reutilizar código. Cada archivo de código fuente pertenece a un paquete, y los paquetes agrupan lógicamente el código relacionado. Los nombres de los paquetes deben ser únicos dentro de un mismo workspace de Go.

## Estructura de Directorios

La estructura de directorios en Go refleja la estructura de los paquetes. Por ejemplo, si tienes un paquete llamado "db", su código fuente se organizaría en un directorio llamado "db". Dentro de este directorio, puedes tener varios archivos de código fuente que forman parte del paquete.

## Declaración del Paquete

Cada archivo de código fuente comienza con una declaración de paquete. La declaración de paquete indica a qué paquete pertenece el archivo. Por ejemplo, si tienes un archivo llamado "db.go" que forma parte del paquete "db", el primer línea del archivo sería package db.

## Importación de Paquetes

Para utilizar código de otros paquetes en Go, debes importar los paquetes necesarios en tu archivo de código. Esto se hace con la palabra clave import. Por ejemplo, si quieres utilizar el paquete "fmt" para imprimir en la consola, puedes importarlo con import "fmt".

## Importaciones Relativas

Cuando importas un paquete en Go, debes especificar su ruta completa desde la raíz del workspace de Go. Por ejemplo, si tienes un paquete "db" en el directorio "src/github.com/user/project/db", debes importarlo con import "github.com/user/project/db".

## Uso de Paquetes

Una vez que has importado un paquete en tu archivo de código, puedes utilizar sus funciones, tipos y variables en tu código. Por ejemplo, si has importado el paquete "fmt", puedes utilizar la función fmt.Println() para imprimir en la consola.

## Estructura de paquetes

```go
myproject/
│
├── cmd/
│   └── myapp/
│       └── main.go
│
├── internal/
│   └── pkgname/
│       └── mypackage/
│           └── ...
│
├── pkg/
│   └── mypackage/
│       └── ...
│
├── api/
│   └── ...
│
├── web/
│   └── ...
│
└── README.md

```

o

```go
GOPATH/
│
├── src/
│   ├── myproject/
│   │   ├── cmd/
│   │   │   └── myapp/
│   │   │       └── main.go
│   │   ├── internal/
│   │   │   └── pkgname/
│   │   │       └── mypackage/
│   │   │           └── ...
│   │   ├── pkg/
│   │   │   └── mypackage/
│   │   │       └── ...
│   │   ├── api/
│   │   │   └── ...
│   │   └── web/
│   │       └── ...
│   │
│   ├── otherproject/
│   │   └── ...
│   │
│   └── ...
│
├── pkg/
│   └── ...
│
└── bin/
    └── ...
```
