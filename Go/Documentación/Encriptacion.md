# Encriptación en Go

La encriptación en Go (Golang) se puede realizar utilizando el paquete crypto. Aquí te mostraré cómo hacer encriptación y desencriptación simétrica utilizando el algoritmo AES (Advanced Encryption Standard), que es uno de los más utilizados.

## Ejemplo de encriptación y desencriptación en Go

**Generar una clave (key): La clave debe ser de 16, 24 o 32 bytes para AES-128, AES-192 o AES-256, respectivamente.**
**Encriptar un mensaje**
**Desencriptar el mensaje encriptado**

## Importar paquetes necesarios

```go
import (
    "crypto/aes"
    "crypto/cipher"
    "crypto/rand"
    "encoding/base64"
    "errors"
    "fmt"
    "io"
)
```

_crypto/aes:_ Proporciona funciones para cifrado AES.
_crypto/cipher:_ Contiene interfaces y funciones para operaciones de cifrado de alto nivel, como GCM.
_crypto/rand:_ Para generar números aleatorios criptográficamente seguros.
_encoding/base64:_ Para codificar y decodificar en base64.
_fmt:_ Para imprimir mensajes en la consola.
_io:_ Proporciona interfaces básicas para IO, en este caso, para leer bytes aleatorios.

## Función para generar una clave aleatoria

```go
func generateKey() ([]byte, error) {
    key := make([]byte, 32) // 32 bytes for AES-256
    if _, err := io.ReadFull(rand.Reader, key); err != nil {
        return nil, err
    }
    return key, nil
}

func main() {
    key, err := generateKey()
    if err != nil {
        panic(err)
    }
    fmt.Printf("Generated key: %x\n", key)
}
```

## Función para encriptar un archivo

```go
func encrypt(plaintext string, key []byte) (string, error) {
    // Crea un nuevo bloque de cifrado AES usando la clave proporcionada.
    block, err := aes.NewCipher(key)
    if err != nil {
        return "", err
    }

    // Crea un nuevo GCM (Galois/Counter Mode) a partir del bloque.
    aesGCM, err := cipher.NewGCM(block)
    if err != nil {
        return "", err
    }

    // Genera un nonce (número único de uso) aleatorio del tamaño requerido.
    nonce := make([]byte, aesGCM.NonceSize())
    if _, err := io.ReadFull(rand.Reader, nonce); err != nil {
        return "", err
    }

    // Cifra el texto plano, incluyendo el nonce al inicio del texto cifrado.
    ciphertext := aesGCM.Seal(nonce, nonce, []byte(plaintext), nil)

    // Codifica el resultado en base64 para facilitar su manejo.
    return base64.StdEncoding.EncodeToString(ciphertext), nil
}
```

_aes.NewCipher(key):_ Crea un nuevo bloque de cifrado AES usando la clave proporcionada.
*cipher.NewGCM(block):*Crea un nuevo modo GCM a partir del bloque de cifrado.
_make([]byte, aesGCM.NonceSize()):_ Crea un slice de bytes para el nonce con el tamaño adecuado.
_io.ReadFull(rand.Reader, nonce):_ Llena el nonce con bytes aleatorios seguros.
_aesGCM.Seal(nonce, nonce, []byte(plaintext), nil):_ Cifra el texto plano. El nonce se incluye al inicio del texto cifrado.
_base64.StdEncoding.EncodeToString(ciphertext):_ Codifica el texto cifrado en base64.

## Función para desencriptar un archivo

```go
func decrypt(ciphertext string, key []byte) (string, error) {
    // Decodifica el texto cifrado de base64.
    data, err := base64.StdEncoding.DecodeString(ciphertext)
    if err != nil {
        return "", err
    }

    // Crea un nuevo bloque de cifrado AES usando la clave proporcionada.
    block, err := aes.NewCipher(key)
    if err != nil {
        return "", err
    }

    // Crea un nuevo GCM (Galois/Counter Mode) a partir del bloque.
    aesGCM, err := cipher.NewGCM(block)
    if err != nil {
        return "", err
    }

    // Extrae el nonce del texto cifrado.
    nonceSize := aesGCM.NonceSize()
    nonce, ciphertext := data[:nonceSize], data[nonceSize:]

    // Descifra el texto usando el nonce y la clave.
    plaintext, err := aesGCM.Open(nil, nonce, ciphertext, nil)
    if err != nil {
        return "", err
    }

    // Devuelve el texto descifrado como una cadena.
    return string(plaintext), nil
}
```

_base64.StdEncoding.DecodeString(ciphertext):_ Decodifica el texto cifrado de base64.
_aes.NewCipher(key):_ Crea un nuevo bloque de cifrado AES usando la clave proporcionada.
_cipher.NewGCM(block):_ Crea un nuevo modo GCM a partir del bloque de cifrado.
_data[:nonceSize], data[nonceSize:]:_ Divide los datos en el nonce y el texto cifrado.
_aesGCM.Open(nil, nonce, ciphertext, nil):_ Descifra el texto cifrado.

## Uso de las funciones para archivos

```go
func main() {
    // Define una clave (debe ser de 32 bytes para AES-256).
    key := []byte("myverystrongpasswordo32bitlength")

    // Mensaje a cifrar.
    plaintext := "Hello, World!"
    fmt.Println("Original text:", plaintext)

    // Cifra el mensaje.
    encrypted, err := encrypt(plaintext, key)
    if err != nil {
        panic(err)
    }
    fmt.Println("Encrypted text:", encrypted)

    // Descifra el mensaje.
    decrypted, err := decrypt(encrypted, key)
    if err != nil {
        panic(err)
    }
    fmt.Println("Decrypted text:", decrypted)
}
```

_Define una clave de 32 bytes para AES-256._
_Define el mensaje a cifrar._
_Llama a encrypt para cifrar el mensaje._
_Llama a decrypt para descifrar el mensaje._
