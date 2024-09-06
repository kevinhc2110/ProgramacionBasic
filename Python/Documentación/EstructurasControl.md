# Estructuras de Control en Python

Las estructuras de control son fundamentales en cualquier lenguaje de programación, ya que permiten que un programa tome decisiones y ejecute diferentes bloques de código según ciertas condiciones. Python ofrece una variedad de estructuras de control que facilitan la creación de programas más complejos y flexibles.

## Condicionales

Los condicionales permiten ejecutar diferentes bloques de código dependiendo de si una condición se cumple o no.

**if:** Ejecuta un bloque de código si la condición es verdadera.

```py
if edad >= 18:
    print("Eres mayor de edad.")
```

**else:** Se ejecuta si la condición del if es falsa.

```py
if edad >= 18:
    print("Eres mayor de edad.")
else:
    print("Eres menor de edad.")
```

**elif:** Permite evaluar múltiples condiciones de forma secuencial.

```py
if edad < 13:
    print("Eres un niño.")
elif edad < 18:
    print("Eres un adolescente.")
else:
    print("Eres un adulto.")
```

## Bucles

Los bucles permiten repetir un bloque de código varias veces.

**for:** Se utiliza para iterar sobre una secuencia (listas, tuplas, cadenas, etc.).

```py
for i in range(5):
    print(i)
```

**while:** Se ejecuta un bloque de código mientras una condición sea verdadera.

```py
contador = 0
while contador < 5:
    print(contador)
    contador += 1
```

## Control de Flujo

**break:** Sale de un bucle inmediatamente.

```py
for i in range(10):
    if i == 5:
        break
    print(i)
```

**continue:** Salta a la siguiente iteración de un bucle.

```py
for i in range(10):
    if i % 2 == 0:
        continue
    print(i)
```

**return:** Sale de una función y devuelve un valor.

```py
def factorial(n):
    if n == 0:
        return 1
    else:
        return n * factorial(n - 1)
```

## Iteradores

Los iteradores son objetos que permiten recorrer elementos de una colección de forma secuencial. Se utilizan comúnmente con bucles for.

```py
mi_lista = [1, 2, 3]
iterador = iter(mi_lista)
while True:
    try:
        elemento = next(iterador)
        print(elemento)
    except StopIteration:
        break
```
