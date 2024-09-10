# Endianess y Diagramas UML

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
