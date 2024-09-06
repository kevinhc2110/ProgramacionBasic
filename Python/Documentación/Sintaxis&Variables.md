# Sintaxis y Variables

## Sintaxis básica

**Sintaxis Básica**
Python se destaca por su sintaxis clara y concisa, lo que lo hace un lenguaje muy legible. Algunos de sus elementos clave son:

_Indentación:_ A diferencia de otros lenguajes, Python utiliza la indentación para definir bloques de código. Esto mejora la legibilidad y evita el uso de llaves o palabras clave para delimitar bloques.
_Palabras clave:_ Son palabras reservadas con un significado especial en Python, como if, else, for, while, def, etc.
_Operadores:_ Se utilizan para realizar operaciones matemáticas, lógicas y de comparación. Los operadores más comunes son +, -, \*, /, ==, !=, <, >, and, or, not.
_Comentarios:_ Se utilizan para explicar el código y se inician con el símbolo #.

**Declaración de Variables**
En Python, no es necesario declarar el tipo de una variable antes de usarla. El tipo se infiere automáticamente del valor asignado.

```py
# Declaración de variables
nombre = "Juan"  # String
edad = 30        # Entero
altura = 1.75   # Flotante
es_estudiante = True  # Booleano
```

**Tipos de datos básicos:**

_int:_ Números enteros (ej: 42, -10)
_float:_ Números de punto flotante (ej: 3.14, -2.5)
_str:_ Cadenas de texto (ej: "Hola", 'Python')
_bool:_ Valores booleanos (True o False)
_None:_ Representa la ausencia de un valor

**Mutabilidad:**

_Inmutables:_ Los objetos de tipo int, float, bool y str son inmutables, es decir, una vez creados, su valor no puede ser modificado.
_Mutables:_ Las listas, diccionarios y conjuntos son mutables, lo que significa que sus elementos pueden ser modificados después de su creación.

**Ámbito de las Variables**
El ámbito de una variable determina dónde puede ser utilizada.

_Variables globales:_ Declaradas fuera de cualquier función y son accesibles desde cualquier parte del programa.
_Variables locales:_ Declaradas dentro de una función y solo son accesibles dentro de esa función.

```py
x = 10  # Variable global

def mi_funcion():
    y = 5  # Variable local
    print(x)  # Accediendo a la variable global
    print(y)  # Accediendo a la variable local

mi_funcion()
```

**Conversión de Tipos:**

_Implícita:_ Python realiza conversiones de tipo automáticamente en algunas situaciones, como cuando se suman un entero y un flotante.
_Explícita:_ Se utiliza la función int(), float(), str(), etc. para convertir un valor de un tipo a otro.

```py
num1 = 10
num2 = 3.14
resultado = num1 + num2  # Conversión implícita a float
print(resultado)

cadena = "100"
numero = int(cadena)  # Conversión explícita a entero
print(numero)
```

**Constantes**
Aunque Python no tiene un tipo de dato específico para constantes, se recomienda utilizar nombres de variables en mayúsculas para indicar que su valor no debe cambiar.

```py
PI = 3.14159
```

**Diferencias entre variables y constantes:**

_Convención:_ Las constantes se escriben en mayúsculas para distinguirlas de las variables.
_Modificación:_ Aunque no hay una restricción estricta, se espera que el valor de una constante no sea modificado después de su inicialización.
