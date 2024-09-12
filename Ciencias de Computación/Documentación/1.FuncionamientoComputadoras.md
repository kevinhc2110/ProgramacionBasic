# Cómo Funcionan las Computadoras

Las computadoras son máquinas complejas que realizan una variedad de tareas mediante la ejecución de instrucciones programadas. A continuación, se presenta una descripción general de los componentes clave, el funcionamiento básico y la gestión de procesos y subprocesos en una computadora.

## Componentes Básicos de una Computadora

### Unidad Central de Procesamiento (CPU)

- **Descripción**: La CPU es el "cerebro" de la computadora, encargado de ejecutar instrucciones de programas. Realiza operaciones aritméticas, lógicas y de control.
- **Componentes**:
  - **Unidad Aritmético-Lógica (ALU)**: Realiza operaciones aritméticas y lógicas.
  - **Unidad de Control (CU)**: Dirige el flujo de datos entre la CPU y otros componentes.
  - **Registros**: Almacenan datos temporales y resultados de operaciones.

### Memoria

- **Memoria Principal (RAM)**: Almacena datos e instrucciones que la CPU está utilizando activamente. Es volátil, lo que significa que pierde su contenido cuando se apaga la computadora.
- **Memoria Secundaria**: Incluye discos duros (HDD), unidades de estado sólido (SSD) y otros dispositivos de almacenamiento que guardan datos permanentemente.

### Dispositivos de Entrada y Salida

- **Entrada**: Teclado, ratón, micrófono, etc.
- **Salida**: Monitor, impresora, altavoces, etc.

### Placa Base (Motherboard)

- **Descripción**: La placa base conecta todos los componentes de hardware de la computadora, incluyendo la CPU, la memoria, los dispositivos de entrada/salida y otros periféricos.

---

## Funcionamiento Básico

### Ciclo de Instrucción

El ciclo de instrucción es el proceso mediante el cual la CPU ejecuta instrucciones. Consiste en tres pasos principales:

1. **Búsqueda (Fetch)**: La CPU obtiene una instrucción de la memoria.
2. **Decodificación (Decode)**: La CPU interpreta la instrucción para entender qué operación debe realizar.
3. **Ejecución (Execute)**: La CPU lleva a cabo la operación especificada por la instrucción.

### Ejecución de Programas

- **Carga del Programa**: El sistema operativo carga el programa desde el almacenamiento secundario a la memoria RAM.
- **Ejecución**: La CPU ejecuta las instrucciones del programa siguiendo el ciclo de instrucción.
- **Almacenamiento de Resultados**: Los resultados se almacenan en la memoria o se envían a dispositivos de salida.

---

## Procesos y Subprocesos

### Procesos

- **Descripción**: Un proceso es una instancia en ejecución de un programa. Incluye el código del programa, su estado, y los recursos necesarios para su ejecución.
- **Estado de un Proceso**:
  - **Nuevo**: El proceso ha sido creado.
  - **Ejecutando**: El proceso está en ejecución.
  - **Esperando**: El proceso está esperando algún recurso o evento.
  - **Terminado**: La ejecución del proceso ha finalizado.

### Subprocesos (Threads)

- **Descripción**: Un subproceso es una unidad de ejecución dentro de un proceso. Permite a un proceso realizar múltiples tareas simultáneamente.
- **Ventajas**:
  - **Concurrencia**: Permite que múltiples tareas se realicen al mismo tiempo.
  - **Eficiencia**: Comparado con la creación de múltiples procesos, los subprocesos comparten el mismo espacio de memoria y recursos, lo que hace que sean más eficientes.
- **Modelo de Subprocesos**:
  - **Subprocesos en el Usuario**: Gestionados por la biblioteca de subprocesos del usuario.
  - **Subprocesos del Núcleo**: Gestionados por el sistema operativo, proporcionando soporte para la ejecución concurrente en el nivel del núcleo.

---

## Gestión de Procesos y Subprocesos

### Planificación de Procesos

- **Descripción**: La planificación de procesos es el mecanismo por el cual el sistema operativo decide qué proceso o subproceso debe ejecutarse en un momento dado.
- **Algoritmos de Planificación**:
  - **FIFO (First In, First Out)**: Los procesos se ejecutan en el orden en que llegan.
  - **Round Robin**: Los procesos reciben un tiempo de CPU fijo en ciclos rotativos.
  - **Prioridad**: Los procesos se ejecutan en función de su prioridad.

### Sincronización y Comunicación

- **Sincronización**: Coordina la ejecución de subprocesos para evitar conflictos y garantizar el acceso adecuado a los recursos compartidos.
- **Comunicación**: Los subprocesos y procesos pueden comunicarse entre sí utilizando mecanismos como colas de mensajes, semáforos y memoria compartida.
