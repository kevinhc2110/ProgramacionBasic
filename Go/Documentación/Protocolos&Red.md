# Redes en Go

Go ofrece herramientas para trabajar con redes, como:

_net:_ Paquete principal para trabajar con sockets y protocolos de red.
_net/http:_ Paquete para crear servidores HTTP y clientes HTTP.
_crypto/tls:_ Paquete para implementar conexiones seguras utilizando TLS.
_encoding/json:_ Paquete para codificar y decodificar datos JSON.

**Además de estos conceptos, Go ofrece soporte para:**

_Concurrencia:_ Goroutines y canales permiten crear aplicaciones altamente concurrentes y escalables.
_Interfaces de red:_ Go puede interactuar con diferentes interfaces de red y configurarlas. Puede enumerar las interfaces de red disponibles, obtener su dirección IP, configurarlas, etc.
_Tunneling:_ Creación de túneles seguros a través de redes(SSH), para acceder a servicios remotos de forma segura.

## Redes

### net

_Sockets:_ Permite la comunicación directa a nivel de socket, tanto TCP como UDP.

### net/http

_Servidores HTTP:_ Facilita la creación de servidores web para servir contenido estático o dinámico.
_Clientes HTTP:_ Permite realizar solicitudes HTTP a otros servidores.

### crypto/tls

_Conexiones seguras:_ Implementa el protocolo TLS para cifrar la comunicación y proteger datos sensibles.

```go
package main

import (
        "crypto/tls"
        "net/http"
)

func main() {
        cert, err := tls.LoadX509KeyPair("cert.pem", "key.pem")
        if err != nil {
            // Manejar error
        }

        config := &tls.Config{Certificates: []tls.Certificate{cert}}
        server := &http.Server{Addr: ":443", TLSConfig: config}
        log.Fatal(server.ListenAndServeTLS("", ""))
}
```

### encoding/json

_Serialización y deserialización:_ Codifica y decodifica datos en formato JSON, permitiendo la interoperabilidad con otros sistemas.

## Protocolos

**Redes:**

_IP (Internet Protocol):_ Protocolo principal para el envío de datos entre redes en Internet.
_TCP (Transmission Control Protocol):_ Protocolo confiable para la transmisión de datos.
_UDP (User Datagram Protocol):_ Protocolo de datagramas que permite comunicaciones rápidas sin conexión, utilizado en aplicaciones que requieren baja latencia, como streaming y juegos en línea.
_ICMP (Internet Control Message Protocol):_ Utilizado para el envío de mensajes de control y diagnóstico en redes.

**Seguridad:**

_SSL/TLS (Secure Sockets Layer / Transport Layer Security):_ Protocolos para asegurar las comunicaciones cifradas.
_IPsec (Internet Protocol Security):_ Cifra y autentica los paquetes IP para comunicaciones seguras.
_SSH (Secure Shell):_ Protocolo para acceso remoto seguro mediante cifrado y autenticación.
_OAuth:_ Protocolo de autorización que permite a aplicaciones de terceros acceder a recursos sin compartir contraseñas.
_Kerberos:_ Protocolo de autenticación basado en tickets, usado para la comunicación segura.

**Correo electrónico:**

_SMTP (Simple Mail Transfer Protocol):_ Envío de correos electrónicos entre servidores.
_IMAP (Internet Message Access Protocol):_ Gestión de correos en servidores.
_POP3 (Post Office Protocol 3):_ Descarga de correos desde servidores.

**Web:**

_HTTP (Hypertext Transfer Protocol):_ Protocolo para transferir datos en la web.
_HTTPS (Hypertext Transfer Protocol Secure):_ Versión segura de HTTP, usando TLS.
_HTTP/2:_ Versión mejorada de HTTP que permite un rendimiento más eficiente, con características como la multiplexación de conexiones.

**Mensajería y APIs:**

_gRPC:_ Framework RPC basado en HTTP/2 y Protocol Buffers, optimizado para la comunicación entre microservicios.
_MQTT (Message Queuing Telemetry Transport):_ Protocolo de mensajería ligero, ideal para dispositivos IoT y comunicaciones de baja latencia.

**Redes Inalámbricas:**

_Wi-Fi (Wireless Fidelity):_ Estándar para la comunicación inalámbrica en redes locales.
_Bluetooth:_ Protocolo para la transmisión de datos a corta distancia.

**Transferencia de archivos:**

_FTP (File Transfer Protocol):_ Protocolo para la transferencia de archivos en redes.
_SFTP (SSH File Transfer Protocol):_ Versión segura de FTP, basada en SSH.
_TFTP (Trivial File Transfer Protocol):_ Protocolo simple para la transferencia de archivos sin autenticación.

**Dirección y resolución de nombres:**

_DNS (Domain Name System):_ Traduce nombres de dominio en direcciones IP.
_DHCP (Dynamic Host Configuration Protocol):_ Asigna direcciones IP dinámicamente a dispositivos en redes.

**Video en tiempo real:**

_RTP (Real-Time Protocol):_ Protocolo para la transmisión de datos multimedia en tiempo real, como audio y video.
_RTCP (Real-Time Control Protocol):_ Protocolo complementario a RTP para monitorear la calidad del servicio.
_RTSP (Real-Time Streaming Protocol):_ Protocolo para controlar la transmisión de contenido multimedia en tiempo real.
_HLS (HTTP Live Streaming):_ Protocolo de streaming de video que distribuye video en fragmentos.
_MPEG-DASH (Dynamic Adaptive Streaming over HTTP):_ Estándar para la transmisión de video adaptativa en tiempo real.

**Mensajería instantánea y VoIP:**

_SIP (Session Initiation Protocol):_ Protocolo para iniciar y terminar sesiones de comunicación en tiempo real, como llamadas de voz y video.
_XMPP (Extensible Messaging and Presence Protocol):_ Protocolo para mensajería instantánea y comunicación en tiempo real.
_H.323:_ Estándar para la transmisión de audio, video y datos sobre redes IP, usado en videoconferencias.

**Multimedia y difusión:**

_DLNA (Digital Living Network Alliance):_ Protocolo para compartir medios digitales entre dispositivos dentro de una red doméstica.
_UPnP (Universal Plug and Play):_ Protocolo que permite que los dispositivos se descubran y establezcan servicios en redes locales.
