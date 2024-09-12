# Memoria en Programación

La **memoria** en una computadora juega un papel crucial en el almacenamiento temporal y la manipulación de datos mientras un programa está en ejecución. Esta memoria está organizada en varias capas jerárquicas para equilibrar la velocidad, el costo y la capacidad de almacenamiento. En este documento, exploraremos cómo se organiza la memoria, cómo los programas acceden a ella y cómo los punteros nos permiten manipular direcciones de memoria.

---

## Jerarquía de Memoria

La **jerarquía de memoria** es un concepto fundamental en la arquitectura de computadoras que organiza diferentes tipos de memoria en función de su velocidad, tamaño y proximidad al procesador. El diseño de la jerarquía busca optimizar el rendimiento al hacer que los datos más frecuentemente utilizados estén disponibles en memorias rápidas y pequeñas.

### Niveles de la Jerarquía de Memoria

#### Registros del Procesador

- Son la forma más rápida de memoria y se encuentran dentro del propio CPU.
- Su capacidad es extremadamente limitada, pero son cruciales para operaciones rápidas como cálculos y manipulación de datos inmediatos.

#### Caché

- Es una memoria intermedia rápida entre el procesador y la memoria principal.
- Existen varios niveles (L1, L2, L3), siendo L1 la más rápida y cercana al procesador, pero con menor capacidad.
- Almacena datos que el CPU usa con frecuencia para evitar acceder a la memoria RAM más lenta.

#### Memoria Principal (RAM)

- Es la memoria de acceso aleatorio que almacena temporalmente datos e instrucciones mientras un programa está en ejecución.
- Su capacidad es mayor que la caché, pero es más lenta en comparación.
- Los programas cargan sus datos en la RAM durante la ejecución, lo que permite acceso rápido.

#### Memoria Secundaria (Almacenamiento)

- Incluye discos duros (HDD), unidades de estado sólido (SSD) y otros medios de almacenamiento no volátil.
- Aunque tiene una capacidad mucho mayor que la RAM, es significativamente más lenta.
- Almacena permanentemente los datos cuando el programa no está en ejecución o la computadora está apagada.

---

## Numeración de Memoria en Hexadecimal

En programación, las direcciones de memoria suelen representarse en **hexadecimal** (base 16) debido a su conveniencia en sistemas binarios. Cada dirección de memoria se traduce a una forma hexadecimal para facilitar su manejo, especialmente cuando tratamos con sistemas a bajo nivel.

### ¿Por qué Hexadecimal?

#### Compacidad

- El sistema hexadecimal reduce la longitud de los números que representan direcciones de memoria. Por ejemplo, un número binario largo puede ser representado de forma más compacta en hexadecimal.
- Un número binario de 32 bits, como `11110010101111000011100111011011`, se representa en hexadecimal como **0xF2BC39DB**.

#### Distinción entre Valor y Dirección

- Los números en memoria pueden ser interpretados como valores o direcciones. Para evitar confusión, los valores hexadecimales se prefijan con **0x**, indicando que son direcciones de memoria y no simples valores numéricos.

---

## Endianess

**Endianess** se refiere al orden en el que los bytes de una palabra de datos se almacenan en memoria o se transmiten entre sistemas. Existen dos tipos principales de endianess:

### 1. Big-Endian

- **Descripción**: En un sistema big-endian, el byte más significativo (MSB - Most Significant Byte) se almacena en la dirección de memoria más baja. Es decir, los bytes se almacenan de forma que el primer byte es el más importante y el último byte es el menos importante.
- **Ejemplo**: Si se almacena el número hexadecimal `0x12345678`, en un sistema big-endian, los bytes se almacenarán como `12 34 56 78` en la memoria.

### 2. Little-Endian

- **Descripción**: En un sistema little-endian, el byte menos significativo (LSB - Least Significant Byte) se almacena en la dirección de memoria más baja. Es decir, los bytes se almacenan de forma que el primer byte es el menos importante y el último byte es el más importante.
- **Ejemplo**: Si se almacena el número hexadecimal `0x12345678`, en un sistema little-endian, los bytes se almacenarán como `78 56 34 12` en la memoria.

### Relevancia

- **Interoperabilidad**: La endianess afecta la interoperabilidad entre sistemas con diferentes representaciones de bytes. Es importante tener en cuenta la endianess al leer o escribir datos binarios entre sistemas.
- **Conversión**: Al intercambiar datos entre sistemas con diferentes endianess, es necesario convertir los datos para mantener la coherencia.
