# Operadores

Los operadores en Python son símbolos especiales que se utilizan para realizar operaciones en valores y variables. Estos operadores nos permiten realizar cálculos, comparaciones, asignaciones y más.

## Tipos de Operadores en Python

**Operadores Aritméticos**
Estos operadores se utilizan para realizar operaciones matemáticas básicas.

_Suma:_ + (Ejemplo: x + y)
_Resta:_ - (Ejemplo: x - y)
_Multiplicación:_ \* (Ejemplo: x \* y)
_División:_ / (Ejemplo: x / y)
_División entera:_ // (Ejemplo: x // y, devuelve el cociente entero de la división)
_Módulo:_ % (Ejemplo: x % y, devuelve el resto de la división)
_Exponenciación:_ \*\* (Ejemplo: x \*\* y, eleva x a la potencia y)

**Operadores de Comparación**
Estos operadores se utilizan para comparar valores y devolver un valor booleano (True o False).

_Igual:_ == (Ejemplo: x == y)
_Diferente:_ != (Ejemplo: x != y)
_Mayor que:_ > (Ejemplo: x > y)
_Menor que:_ < (Ejemplo: x < y)
_Mayor o igual que:_ >= (Ejemplo: x >= y)
_Menor o igual que:_ <= (Ejemplo: x <= y)

**Operadores Lógicos**
Estos operadores se utilizan para combinar expresiones booleanas.

_Y:_ and (Devuelve True si ambas expresiones son True)
_O:_ or (Devuelve True si al menos una de las expresiones es True)
_No:_ not (Niega una expresión booleana)

**Operadores de Asignación**
Estos operadores se utilizan para asignar valores a variables.

_Asignación simple:_ = (Ejemplo: x = 5)
_Asignación compuesta:_ +=, -=, \*=, /=, %=, //= (Ejemplo: x += 5 es equivalente a x = x + 5)

**Operadores de Identidad y Pertenencia:**

_Es:_ is (Compara si dos objetos son el mismo)
_No es:_ is not (Compara si dos objetos no son el mismo)
_En:_ in (Comprueba si un elemento está presente en una secuencia)
_No en:_ not in (Comprueba si un elemento no está presente en una secuencia)

```py
x = 10
y = 5

# Operaciones aritméticas
suma = x + y
resta = x - y
multiplicacion = x * y
division = x / y
resto = x % y
potencia = x ** y

# Comparaciones
es_igual = x == y
es_mayor = x > y

# Lógica
condicion = (x > 5) and (y < 10)

# Asignación
x += 2  # Equivalente a x = x + 2

# Pertenencia
lista = [1, 2, 3]
esta_en_lista = 2 in lista

print(suma, resta, multiplicacion, division, resto, potencia, es_igual, es_mayor, condicion, esta_en_lista)
```

**Operadores Bit a Bit**
Estos operadores realizan operaciones a nivel de bits sobre números enteros.

_Y bit a bit:_ &
_O bit a bit:_ |
_XOR bit a bit:_ ^
_Negación bit a bit:_ ~
_Desplazamiento a la izquierda:_ <<
_Desplazamiento a la derecha:_ >>

Nota: Los operadores bit a bit son más avanzados y se utilizan en situaciones específicas, como en programación a bajo nivel o en algoritmos de optimización.
