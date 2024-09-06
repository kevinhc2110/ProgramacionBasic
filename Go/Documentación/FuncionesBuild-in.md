# Funciones Built-in en Go: Tus Herramientas Esenciales

Go, ofrece un conjunto robusto de funciones integradas que simplifican significativamente la programación. Estas funciones son parte del lenguaje y están siempre disponibles para su uso directo.

## ¿Qué son las funciones built-in en Go?

Son funciones predefinidas que realizan tareas comunes y están optimizadas para el rendimiento. Cubren un amplio espectro de operaciones, desde operaciones matemáticas básicas hasta manipulación de cadenas, manejo de errores y más.

## ¿Por qué son útiles?

_Eficiencia:_ Están implementadas de manera eficiente, lo que se traduce en un código más rápido.
_Consistencia:_ Proporcionan una interfaz unificada para realizar tareas comunes.
_Legibilidad:_ Al utilizar funciones estándar, tu código se vuelve más fácil de entender y mantener.

## Algunas funciones built-in comunes en Go

**Conversión de tipos**
_int(x):_ Convierte x a un entero.
_float64(x):_ Convierte x a un número de punto flotante de 64 bits.
_string(x):_ Convierte x a una cadena.
_byte(x):_ Convierte x a un byte (un entero de 8 bits).

**Matemáticas**
_math.Abs(x):_ Devuelve el valor absoluto de x.
_math.Sqrt(x):_ Calcula la raíz cuadrada de x.
_math.Pow(x, y):_ Calcula x elevado a la potencia y.
_math.Sin(x), math.Cos(x), math.Tan(x):_ Funciones trigonométricas.

**Cadenas**
_len(s):_ Devuelve la longitud de una cadena s.
_strings.ToUpper(s):_ Convierte una cadena a mayúsculas.
_strings.ToLower(s):_ Convierte una cadena a minúsculas.
_strings.Contains(s, substr):_ Comprueba si una cadena contiene una subcadena.

**Tipos de datos básicos**
_append(slice, elements...):_ Agrega elementos a un slice.
_make(T, size):_ Crea un slice, mapa o canal de tipo T con el tamaño especificado.
_cap(s):_ Devuelve la capacidad de un slice.
_len(s):_ Devuelve la longitud de un slice, mapa o cadena.

**Entrada y salida**
_fmt.Println(...):_ Imprime valores en la consola, seguido de un salto de línea.
_fmt.Printf(format, values):_ Imprime valores formateados.
_bufio.NewReader(reader):_ Crea un lector de búfer para leer texto de un lector.
