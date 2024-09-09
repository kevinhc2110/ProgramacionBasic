# Introducción a la Programación de Computadoras

La **programación de computadoras** se basa en recibir entradas, procesarlas y generar una salida que resuelva un problema. El proceso que ocurre entre la entrada y la salida es conocido como una **caja negra**. Este curso se centra en comprender cómo funciona dicha caja negra y cómo las computadoras realizan tareas básicas como contar, almacenar información y comunicarse.

---

## Sistema de Numeración Binario

Las computadoras utilizan el **sistema binario** para contar. A diferencia de los humanos, que usamos el sistema decimal (base 10), las computadoras usan **base 2**, donde solo hay dos posibles valores: **0** (apagado) y **1** (encendido). Un solo valor de 0 o 1 se llama **bit**.

### Ejemplo de Contar con Bombillas

Imaginemos que usamos bombillas para representar números:

- Tres bombillas apagadas (**0 0 0**) representan el número **0**.
- Si encendemos la última bombilla (**0 0 1**), representamos el número **1**.
- Encendiendo otras bombillas, podemos representar números mayores:
  - **0 1 0** → 2
  - **0 1 1** → 3
  - **1 0 0** → 4
  - **1 1 1** → 7

Así, con solo tres bombillas (o bits), podemos contar de **0** a **7**.

#### Relación con las Potencias de Dos

Cada posición en un número binario tiene un valor que corresponde a una potencia de 2:

- **2^2** → 4
- **2^1** → 2
- **2^0** → 1

Por ejemplo, el número binario **101** se puede descomponer como:

- \(1 \times 2^2 = 4\)
- \(0 \times 2^1 = 0\)
- \(1 \times 2^0 = 1\)

El valor final es **4 + 0 + 1 = 5**.

---

## Bits y Bytes

Las computadoras usualmente agrupan los bits en conjuntos de **8 bits**, conocidos como **bytes**. Un byte puede representar números del 0 al 255. Por ejemplo:

- **00000000** representa el número **0**.
- **11111111** representa el número **255**.

Esto se utiliza comúnmente en la representación de datos como colores y caracteres.

---

## ASCII: Representación de Caracteres

El sistema **ASCII** (American Standard Code for Information Interchange) fue creado para asignar letras y símbolos a números. Esto es esencial para que las computadoras representen texto.

Por ejemplo:

- La letra **A** está asignada al número **65** en ASCII.
- El número **65** en binario es **01000001**.

Cuando recibes un mensaje de texto, lo que la computadora realmente ve son números binarios, que luego convierte a letras usando ASCII.

Ejemplo de mensaje:

- **H** → 72
- **I** → 73
- **!** → 33

Este mensaje en ASCII sería: **HI!**.

### Mapa ASCII

El estándar ASCII asigna un valor a cada letra, número y símbolo. Por ejemplo:

| Caracter | Código ASCII | Representación Binaria |
| -------- | ------------ | ---------------------- |
| A        | 65           | 01000001               |
| B        | 66           | 01000010               |
| H        | 72           | 01001000               |
| I        | 73           | 01001001               |
| !        | 33           | 00100001               |

---

## Arte de Píxeles

Un **píxel** es el bloque más pequeño que compone una imagen digital. Las imágenes están formadas por una cuadrícula de píxeles, donde cada uno tiene un color específico.

En imágenes **blanco y negro**, los **0s** y **1s** pueden representar colores:

- **0** → negro
- **1** → blanco

Esto forma la base del arte de píxeles, donde imágenes completas pueden ser generadas usando matrices de números binarios.

---

## Colores y el Sistema RGB

Los colores en la computadora se representan mediante el sistema **RGB** (Red, Green, Blue). Cada color se forma mezclando diferentes cantidades de rojo, verde y azul.

### Ejemplo en Photoshop

En programas como Photoshop, puedes ver la combinación de colores RGB. Por ejemplo:

- **Rojo:** (255, 0, 0)
- **Verde:** (0, 255, 0)
- **Azul:** (0, 0, 255)

Además del sistema RGB, los colores también pueden representarse en **hexadecimal**.

---

## Sistema Hexadecimal

El **hexadecimal** es un sistema numérico en **base 16**, que incluye los dígitos del 0 al 9, y las letras **a** a **f** para representar los valores del 10 al 15.

### Tabla de Hexadecimal

| Decimal | Hexadecimal |
| ------- | ----------- |
| 10      | a           |
| 11      | b           |
| 12      | c           |
| 13      | d           |
| 14      | e           |
| 15      | f           |

#### Ejemplo de Contar en Hexadecimal

Al contar en hexadecimal:

- **0** en decimal es **0** en hexadecimal.
- **10** en decimal es **a** en hexadecimal.
- **255** en decimal es **ff** en hexadecimal.

### Relación con el Binario

El hexadecimal es útil para representar valores binarios de forma compacta. Por ejemplo:

- El binario **1111** es **f** en hexadecimal.
- El binario **0000 1111 1111** es **0ff** en hexadecimal.

Por eso, los colores en formato hexadecimal usan 6 dígitos, como **#ff0000** para el rojo, lo que representa la máxima cantidad de rojo y ninguna cantidad de verde o azul.

---
