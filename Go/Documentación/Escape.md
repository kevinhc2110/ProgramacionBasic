# Caracteres de Escape

Los caracteres de escape son secuencias de caracteres que no se representan directamente en el texto, sino que tienen un significado especial cuando se interpretan en contextos específicos, como en cadenas de texto en lenguajes de programación, sistemas de archivos, y formatos de datos.

## Ejemplo de diferentes caracteres de escape

```go
package main

import "fmt"

func main() {
 fmt.Println(
  "\n: Nueva línea",
  "\t: Tabulador horizontal",
  "\v: Tabulador vertical",
  "\\: Barra invertida literal ",
  "\": Comilla doble literal",
  "'Comilla simple literal'",
  "\r: Retorno de carro",
  "\f: Salto de página",
  "\b: Retroceso",
  "\x00: Caracter nulo",
  "\a: Alerta",
  "\x0A: Representación hexadecimal del carácter hexadecimal de un byte 'A'",
  "\u20AC: Representación Unicode del carácter 4 dígitos hexadecimal '€'",
  "\U0001F497: Representación Unicode del emoji de corazón 8 dígitos hexadecimal (❤️)",
  "\U0001F60A: Representación Unicode del emoji de sonrisa Unicode de longitud variable (UTF-8) (😊)",
 )
}
```
