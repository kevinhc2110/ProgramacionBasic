# Protocolos

## Redes

- **IP (Internet Protocol)**: Protocolo principal para el envío de datos entre redes en Internet.
- **TCP (Transmission Control Protocol)**: Protocolo confiable para la transmisión de datos, garantiza la entrega ordenada y sin errores.
- **UDP (User Datagram Protocol)**: Protocolo sin conexión que permite comunicaciones rápidas, utilizado en aplicaciones que requieren baja latencia, como streaming y juegos en línea.
- **ICMP (Internet Control Message Protocol)**: Utilizado para el envío de mensajes de control y diagnóstico en redes, como el comando `ping`.

---

## Seguridad

- **SSL/TLS (Secure Sockets Layer / Transport Layer Security)**: Protocolos que aseguran las comunicaciones mediante cifrado.
- **IPsec (Internet Protocol Security)**: Cifra y autentica los paquetes IP para comunicaciones seguras.
- **SSH (Secure Shell)**: Protocolo para acceso remoto seguro mediante cifrado y autenticación.
- **OAuth**: Protocolo de autorización que permite a aplicaciones de terceros acceder a recursos sin compartir contraseñas.
- **Kerberos**: Protocolo de autenticación basado en tickets, utilizado para la comunicación segura en redes corporativas.

---

## Correo Electrónico

- **SMTP (Simple Mail Transfer Protocol)**: Protocolo para el envío de correos electrónicos entre servidores.
- **IMAP (Internet Message Access Protocol)**: Permite gestionar correos electrónicos directamente en servidores sin descargarlos.
- **POP3 (Post Office Protocol 3)**: Descarga correos electrónicos desde un servidor para su acceso local.

---

## Web

- **HTTP (Hypertext Transfer Protocol)**: Protocolo para la transferencia de datos en la web.
- **HTTPS (Hypertext Transfer Protocol Secure)**: Versión segura de HTTP que utiliza TLS para cifrar las comunicaciones.
- **HTTP/2**: Versión mejorada de HTTP que permite un rendimiento más eficiente mediante características como la multiplexación de conexiones.

---

## Mensajería y APIs

- **gRPC**: Framework de RPC (Remote Procedure Call) basado en HTTP/2 y Protocol Buffers, optimizado para la comunicación entre microservicios.
- **MQTT (Message Queuing Telemetry Transport)**: Protocolo de mensajería ligero, ideal para dispositivos IoT y comunicaciones de baja latencia.

---

## Redes Inalámbricas

- **Wi-Fi (Wireless Fidelity)**: Estándar para la comunicación inalámbrica en redes locales.
- **Bluetooth**: Protocolo para la transmisión de datos a corta distancia, utilizado en dispositivos móviles y periféricos.

---

## Transferencia de Archivos

- **FTP (File Transfer Protocol)**: Protocolo para la transferencia de archivos entre servidores y clientes en redes.
- **SFTP (SSH File Transfer Protocol)**: Versión segura de FTP, basada en el protocolo SSH.
- **TFTP (Trivial File Transfer Protocol)**: Protocolo simple para la transferencia de archivos sin autenticación, utilizado comúnmente en redes locales.

---

## Dirección y Resolución de Nombres

- **DNS (Domain Name System)**: Traduce nombres de dominio en direcciones IP.
- **DHCP (Dynamic Host Configuration Protocol)**: Asigna direcciones IP dinámicamente a dispositivos en una red.

---

## Video en Tiempo Real

- **RTP (Real-Time Protocol)**: Protocolo para la transmisión de datos multimedia en tiempo real, como audio y video.
- **RTCP (Real-Time Control Protocol)**: Protocolo complementario a RTP, utilizado para monitorear la calidad del servicio.
- **RTSP (Real-Time Streaming Protocol)**: Protocolo para controlar la transmisión de contenido multimedia en tiempo real.
- **HLS (HTTP Live Streaming)**: Protocolo de streaming de video que distribuye video en fragmentos para mejorar la experiencia de transmisión.
- **MPEG-DASH (Dynamic Adaptive Streaming over HTTP)**: Estándar para la transmisión de video adaptativa en tiempo real.

---

## Mensajería Instantánea y VoIP

- **SIP (Session Initiation Protocol)**: Protocolo para iniciar y gestionar sesiones de comunicación en tiempo real, como llamadas de voz y video.
- **XMPP (Extensible Messaging and Presence Protocol)**: Protocolo utilizado para mensajería instantánea y comunicación en tiempo real.
- **H.323**: Estándar para la transmisión de audio, video y datos sobre redes IP, ampliamente usado en videoconferencias.

---

## Multimedia y Difusión

- **DLNA (Digital Living Network Alliance)**: Protocolo para compartir medios digitales entre dispositivos dentro de una red doméstica.
- **UPnP (Universal Plug and Play)**: Protocolo que permite que los dispositivos se descubran y establezcan servicios automáticamente en redes locales.

## Puertos Comunes y Protocolos

| Protocolo      | Puerto Estándar | Descripción                                                                          |
| -------------- | --------------- | ------------------------------------------------------------------------------------ |
| **HTTP**       | 80              | Protocolo de Transferencia de Hipertexto, usado para navegación web.                 |
| **HTTPS**      | 443             | HTTP seguro, cifrado con TLS/SSL.                                                    |
| **FTP**        | 21              | Protocolo de Transferencia de Archivos.                                              |
| **SFTP**       | 22              | FTP sobre SSH, protocolo seguro para transferencia de archivos.                      |
| **SSH**        | 22              | Protocolo de Shell Seguro, para acceso remoto seguro.                                |
| **Telnet**     | 23              | Protocolo para acceso remoto (no seguro).                                            |
| **SMTP**       | 25              | Protocolo para envío de correos electrónicos.                                        |
| **POP3**       | 110             | Protocolo para recepción de correos electrónicos.                                    |
| **IMAP**       | 143             | Protocolo de acceso a correos electrónicos con capacidades avanzadas.                |
| **DNS**        | 53              | Sistema de Nombres de Dominio, para resolución de nombres de dominio.                |
| **DHCP**       | 67/68           | Protocolo de Configuración Dinámica de Host, para asignación automática de IPs.      |
| **MySQL**      | 3306            | Puerto utilizado por el sistema de gestión de bases de datos MySQL.                  |
| **PostgreSQL** | 5432            | Puerto utilizado por el sistema de gestión de bases de datos PostgreSQL.             |
| **Redis**      | 6379            | Sistema de almacenamiento en caché y base de datos en memoria.                       |
| **MongoDB**    | 27017           | Puerto utilizado por el sistema de gestión de bases de datos MongoDB.                |
| **LDAP**       | 389             | Protocolo de Acceso Ligero a Directorios, utilizado para servicios de directorio.    |
| **SNMP**       | 161             | Protocolo de Administración de Red Simple, utilizado para monitoreo de redes.        |
| **NTP**        | 123             | Protocolo de Tiempo de Red, utilizado para sincronización de relojes en red.         |
| **RDP**        | 3389            | Protocolo de Escritorio Remoto de Microsoft, para acceso remoto a escritorios.       |
| **VNC**        | 5900            | Protocolo de Red de Computadoras Virtuales, para control remoto de escritorios.      |
| **HTTP/2**     | 443             | Versión mejorada del protocolo HTTP, generalmente utiliza el mismo puerto que HTTPS. |

---

## Importancia de Conocer los Puertos de los Protocolos

### Comunicación de Red

- **Asignación de Puertos:**

  Los protocolos de red utilizan puertos para enviar y recibir datos.

- **Interoperabilidad:**

  Saber qué puertos utilizan los diferentes servicios te asegura que tu aplicación pueda interactuar con otros servicios y sistemas que estén utilizando los mismos puertos.

### Configuración y Seguridad

- **Configuración de Firewall:**
  Los firewalls y otras medidas de seguridad de red utilizan reglas basadas en puertos para permitir o bloquear tráfico.

- **Seguridad:**
  La exposición de ciertos puertos puede representar un riesgo de seguridad.

### Depuración y Resolución de Problemas

- **Diagnóstico de Problemas:**

  Si encuentras problemas de conectividad o rendimiento en tu aplicación, conocer los puertos utilizados te ayuda a diagnosticar y solucionar estos problemas, ya que puedes verificar si el tráfico está llegando al puerto correcto y si hay conflictos o bloqueos.

### Diseño de Arquitectura

- **Diseño de Servicios:**

  Al diseñar servicios y APIs, necesitas decidir qué puertos utilizar. Conocer los puertos estándar y sus usos puede ayudarte a elegir puertos adecuados y evitar conflictos con otros servicios.

- **Escalabilidad:**

  En sistemas distribuidos y en la nube, los puertos son clave para la comunicación entre servicios y nodos. Entender su uso te ayuda a diseñar arquitecturas escalables y eficientes.
