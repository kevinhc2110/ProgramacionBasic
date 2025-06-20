# Seguridad en Programación Go

La seguridad en la programación es un aspecto fundamental que debe ser considerado en todas las fases del ciclo de desarrollo de software. Proteger las aplicaciones de ataques y vulnerabilidades es crucial para garantizar la integridad, confidencialidad y disponibilidad de los sistemas. A continuación, se abordan los principales aspectos de seguridad en programación, aplicables a múltiples entornos y lenguajes de desarrollo.

## Autenticación y Autorización

- Autenticación se refiere a la verificación de la identidad de los usuarios, asegurándose de que sean quienes dicen ser.
- Autorización se enfoca en verificar si un usuario autenticado tiene permiso para realizar una acción o acceder a un recurso.

- ### JSON Web Tokens (JWT)

  JWT es una forma común de autenticar usuarios en sistemas distribuidos. Un token JWT contiene una firma que garantiza la integridad de los datos y es utilizado para la autenticación sin estado (stateless) en APIs.

  - **Estructura de un JWT**

    - **Header:** Contiene el tipo de token (JWT) y el algoritmo de cifrado (HS256).
    - **Payload:** Contiene la información del usuario y cualquier otro dato relevante.
    - **Signature:** Firma generada usando el header, el payload y una clave secreta.

      ```json
      {
          "alg": "HS256",
          "typ": "JWT"
      }
      {
          "sub": "1234567890",
          "name": "John Doe",
          "admin": true
      }

      ```

  - **implementación en Go:**

    ```go
    import (
        "github.com/golang-jwt/jwt"
        "time"
    )

    var jwtKey = []byte("mi_clave_secreta")

    // Generar un JWT
    func generarJWT() (string, error) {
        claims := &jwt.StandardClaims{
            ExpiresAt: time.Now().Add(time.Hour * 1).Unix(),
            Subject:   "usuario123",
        }

        token := jwt.NewWithClaims(jwt.SigningMethodHS256, claims)
        return token.SignedString(jwtKey)
    }

    ```

- ### OAuth 2.0

  OAuth 2.0 es un protocolo de autorización utilizado para permitir que aplicaciones de terceros accedan a los recursos de un usuario en otro sistema sin compartir las credenciales del usuario. Se utiliza ampliamente para integraciones con servicios como Google, Facebook y GitHub.

  - **Flujos principales**

    - **Authorization Code Grant:** Utilizado por aplicaciones web.
    - **Implicit Grant:** Para aplicaciones móviles o basadas en JavaScript.
    - **Client Credentials Grant:** Para autenticación entre servidores.
    - **Resource Owner Password Credentials:** Utilizado cuando el usuario confía completamente en la aplicación.

## Cifrado de Datos

El cifrado es una técnica clave para proteger la información sensible, tanto en tránsito como en reposo.

- ### Cifrado Simétrico

  En el cifrado simétrico, la misma clave se utiliza tanto para cifrar como para descifrar los datos. Un ejemplo común es el uso del algoritmo AES (Advanced Encryption Standard).

  - **Cifrado simétrico en Go usando AES**

    ```go
    import (
        "crypto/aes"
        "crypto/cipher"
    )

    func cifrarAES(key, text []byte) ([]byte, error) {
        block, err := aes.NewCipher(key)
        if err != nil {
            return nil, err
        }
        ciphertext := make([]byte, aes.BlockSize+len(text))
        iv := ciphertext[:aes.BlockSize]
        stream := cipher.NewCFBEncrypter(block, iv)
        stream.XORKeyStream(ciphertext[aes.BlockSize:], text)
        return ciphertext, nil
    }

    ```

- ### Cifrado Asimétrico

  El cifrado asimétrico utiliza un par de claves: una pública y una privada. La clave pública cifra los datos y la clave privada los descifra. Un ejemplo común es el algoritmo RSA.

  - **Generación de claves RSA en Go**

    ```go
    import (
        "crypto/rsa"
        "crypto/rand"
    )

    func generarClavesRSA() (*rsa.PrivateKey, *rsa.PublicKey, error) {
        privateKey, err := rsa.GenerateKey(rand.Reader, 2048)
        if err != nil {
            return nil, nil, err
        }
        publicKey := &privateKey.PublicKey
        return privateKey, publicKey, nil
    }

    ```

## Certificados SSL/TLS

Los certificados SSL/TLS son fundamentales para garantizar conexiones seguras a través de HTTPS. Estos certificados utilizan cifrado asimétrico para proteger la comunicación entre el cliente y el servidor, y evitar que los datos sean interceptados por terceros.

- SSL (Secure Sockets Layer) y TLS (Transport Layer Security) garantizan la integridad y la confidencialidad de los datos en tránsito.
- Let's Encrypt: Es una autoridad de certificación gratuita que facilita la implementación de SSL en aplicaciones.

## Prevención de Vulnerabilidades

Proteger una aplicación implica tomar medidas contra ataques comunes que podrían comprometer la seguridad de los sistemas.

- ### Inyección de SQL

  La inyección de SQL ocurre cuando un atacante inserta código SQL malicioso en una consulta. Esto puede evitarse utilizando consultas preparadas (prepared statements) que separan los datos de la lógica de la consulta.

  ```go
  import (
      "database/sql"
      _ "github.com/lib/pq"
  )

  func obtenerUsuario(db *sql.DB, id int) (*Usuario, error) {
      var usuario Usuario
      err := db.QueryRow("SELECT nombre, email FROM usuarios WHERE id = $1", id).Scan(&usuario.Nombre, &usuario.Email)
      return &usuario, err
  }

  ```

- ### Cross-Site Scripting (XSS)

  El XSS ocurre cuando un atacante inyecta código JavaScript malicioso en una aplicación web. Esto puede ser prevenido sanitizando y escapando adecuadamente la salida de cualquier dato proporcionado por el usuario.

  ```go
  import (
      "html"
      "github.com/gin-gonic/gin"
  )

  func renderHTML(c *gin.Context) {
      data := c.Query("input")
      escapedData := html.EscapeString(data)
      c.String(200, "Entrada segura: %s", escapedData)
  }

  ```

- ### Cross-Site Request Forgery (CSRF)

  El ataque CSRF ocurre cuando un atacante hace que un usuario autenticado realice una acción no deseada en una aplicación en la que está autenticado. Para mitigar este ataque, se pueden usar tokens CSRF, que aseguran que la solicitud provenga de una fuente legítima.

  ```go
  import (
      "github.com/gin-gonic/gin"
      "github.com/utrack/gin-csrf"
  )

  func main() {
      r := gin.Default()

      // Inicializar middleware CSRF
      r.Use(csrf.Middleware(csrf.Options{
          Secret: "mi_csrf_secreto",
      }))

      r.POST("/submit", func(c *gin.Context) {
          token := csrf.GetToken(c)
          c.JSON(200, gin.H{
              "token": token,
          })
      })

      r.Run()
  }
  ```

- ### CORS Cross-Origin Resource Sharing (CORS)

  CORS (Cross-Origin Resource Sharing) es un mecanismo de seguridad que restringe cómo los navegadores permiten que una página web haga peticiones a un dominio distinto al que la sirvió.

  - Por defecto, el navegador bloquea las peticiones entre orígenes diferentes (Cross-Origin).

  - CORS define cabeceras HTTP para indicar qué orígenes están permitidos para acceder a ciertos recursos

  ```go
  package main

    import (
        "net/http"
        "github.com/rs/cors"
    )

    func main() {
        mux := http.NewServeMux()

        mux.HandleFunc("/api", func(w http.ResponseWriter, r *http.Request) {
            w.Write([]byte("Hello CORS!"))
        })

        // Configuración de CORS
        c := cors.New(cors.Options{
            AllowedOrigins:   []string{"https://example.com"}, // Orígenes permitidos
            AllowedMethods:   []string{"GET", "POST", "OPTIONS"},
            AllowedHeaders:   []string{"Authorization", "Content-Type"},
            AllowCredentials: true,
        })

        handler := c.Handler(mux)
        http.ListenAndServe(":8080", handler)
    }

  ```

- ### Open Web Application Security Project (OWASP)

  OWASP (Open Web Application Security Project) es una comunidad que publica recursos, guías y estándares para mejorar la seguridad en aplicaciones web.

  - El proyecto OWASP Top 10 lista las vulnerabilidades web más críticas.
  - CORS mal configurado puede llevar a Cross-Site Request Forgery (CSRF) y otras vulnerabilidades listadas en OWASP.

- ### Puntos importantes según OWASP para CORS

  - No usar "\*" en AllowedOrigins si usas credenciales (cookies, headers de autenticación). Siempre lista explícitamente los orígenes confiables.
  - Limita los métodos HTTP permitidos.
  - Valida y limita los headers permitidos.
  - Si usas cookies o tokens, configura AllowCredentials: true y nunca AllowedOrigins: ["*"].
  - Usa HTTPS para proteger la comunicación.
  - **Implementa otras capas de seguridad:** CSRF tokens, validación backend, autenticación robusta.
