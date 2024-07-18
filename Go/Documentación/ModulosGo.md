# Módulos en Golang

En Golang, el término "mod" se refiere al sistema de módulos para gestionar las dependencias y versiones de los proyectos Go. Proporciona una forma estructurada y organizada de manejar el código requerido por tus aplicaciones Go, facilitando su compartición, reutilización y actualización en diferentes proyectos.

## Características principales de los módulos Go

**Gestión de dependencias:** Elimina la necesidad de carpetas de proveedores y simplifica el proceso de agregar, actualizar y eliminar dependencias.

**Control de versiones:** Asegura que tu proyecto utilice las versiones correctas de las dependencias, previniendo problemas de compatibilidad y comportamientos inesperados.

**Reproducibilidad:** Facilita la construcción y ejecución de tu proyecto en diferentes máquinas, garantizando resultados consistentes en distintos entornos.

**Archivo go.mod:** Utiliza un archivo central llamado go.mod para definir la ruta del módulo, las dependencias y sus versiones.

**Herramientas Go:** Se integra con herramientas Go como go get, go build y go test para optimizar el proceso de gestión de dependencias.

## Beneficios de usar módulos Go

**Mejor organización del proyecto:** Los módulos mantienen las dependencias organizadas y separadas, lo que facilita la gestión y el mantenimiento de proyectos complejos.

**Compilaciones consistentes:** Los módulos aseguran que tu proyecto utilice las mismas dependencias y versiones en diferentes entornos, previniendo discrepancias.

**Actualizaciones de dependencias simplificadas:** La actualización de dependencias se vuelve más sencilla y menos propensa a errores con el sistema de módulos.

**Colaboración mejorada:** Los módulos facilitan la colaboración entre desarrolladores al garantizar que todos trabajen con las mismas dependencias y versiones.

### Ejemplo

**Inicializar un Módulo:**

```bash
go mod init <module-name>
```

**Agregar Dependencias:**

```bash
go get -u github.com/gorilla/mux
```

**Actualizar Dependencias:**

```bash
go get -u ./...
```

**Limpiar Dependencias No Usadas:**

```bash
go mod tidy
```
