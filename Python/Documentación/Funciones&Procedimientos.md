# Funciones y Procedimientos en Python

## Definición de Funciones

Una función en Python es un bloque de código reutilizable que realiza una tarea específica. Se define utilizando la palabra clave def, seguida del nombre de la función, paréntesis que contienen los parámetros (si los hay) y dos puntos.

```py
def saludar(nombre):
    print("Hola,", nombre + "!")
```

_Parámetros:_ Son las variables que se pasan a la función cuando se llama.
_Tipo de retorno:_ Una función puede devolver un valor utilizando la palabra clave return. Si no se especifica un valor de retorno, la función devuelve None.
_Valores por defecto:_ Se pueden asignar valores por defecto a los parámetros, lo que permite llamar a la función sin pasar todos los argumentos.

```py
def potencia(base, exponente=2):
    return base ** exponente
```

## Ámbito de Funciones

_Alcance local:_ Las variables declaradas dentro de una función tienen alcance local y solo son accesibles dentro de esa función.
_Alcance global:_ Las variables declaradas fuera de cualquier función tienen alcance global y son accesibles desde cualquier parte del programa.
_Variables estáticas:_ Las variables estáticas conservan su valor entre llamadas sucesivas a una función. Se declaran utilizando la palabra clave nonlocal (para variables no globales) o global (para variables globales).

```py
contador = 0  # Variable global

def incrementar():
    global contador
    contador += 1
```

## Recursividad

La recursividad es la técnica de definir una función que se llama a sí misma. Es útil para resolver problemas que pueden descomponerse en subproblemas más pequeños del mismo tipo.

```py
def factorial(n):
    if n == 0:
        return 1
    else:
        return n * factorial(n - 1)
```

## Sobrecarga de Funciones

Python no admite sobrecarga de funciones en el sentido tradicional. Sin embargo, se puede simular utilizando argumentos variables o funciones con nombres diferentes pero funcionalidad similar.

```py
def sumar(*args):
    suma = 0
    for num in args:
        suma += num
    return suma
```

## Funciones Anónimas (Lambda)

Las funciones lambda son funciones pequeñas y anónimas definidas en una sola línea. Se utilizan comúnmente como argumentos para otras funciones, como map, filter y reduce.

```py
doble = lambda x: x * 2
```

## Closures

Un closure es una función que recuerda su entorno léxico, es decir, las variables que estaban en el ámbito cuando se definió la función.

```py
def crear_contador():
    contador = 0
    def incrementar():
        nonlocal contador
        contador += 1
        return contador
    return incrementar

mi_contador = crear_contador()
print(mi_contador())  # Imprime 1
print(mi_contador())  # Imprime 2
```
