# Patrones de Diseño

Los patrones de diseño de software son soluciones reutilizables a problemas comunes en el diseño de aplicaciones. Son independientes del lenguaje de programación y ayudan a construir sistemas más robustos, mantenibles y escalables.

## Patrones Creacionales

Controlan cómo se crean los objetos.

- ### Singleton

  El patrón Singleton garantiza una única instancia global de una clase, comúnmente utilizado en configuraciones de aplicaciones, loggers y conexiones a bases de datos; es especialmente importante en lenguajes como Go, Python y Node.js para manejar servicios únicos de manera eficiente, como por ejemplo: `DatabaseConnection.getInstance()`.

  ```js
  class DatabaseConnection {
    constructor() {
      if (DatabaseConnection.instance) {
        return DatabaseConnection.instance;
      }

      this.connection = this.connectToDatabase(); // Simulación de conexión
      DatabaseConnection.instance = this;
    }

    connectToDatabase() {
      console.log("Conectando a la base de datos...");
      // Aquí iría la lógica real, como mongoose.connect() o pg.connect()
      return { status: "connected", time: new Date() };
    }

    getConnection() {
      return this.connection;
    }
  }

  module.exports = DatabaseConnection;
  ```

- ### Factory method

  El patrón Factory Method delega la creación de objetos a subclases especializadas, permitiendo crear diferentes tipos de objetos según el contexto. Es especialmente útil en frameworks y librerías extensibles donde se necesita flexibilidad para generar distintos productos sin acoplar el código a clases concretas, por ejemplo, ParserFactory.createParser("json").

  ```py
  from abc import ABC, abstractmethod

    # Interfaz o clase base para los parsers
    class Parser(ABC):
        @abstractmethod
        def parse(self, data):
            pass

    # Parser para JSON
    class JSONParser(Parser):
        def parse(self, data):
            import json
            return json.loads(data)

    # Parser para XML (simplificado)
    class XMLParser(Parser):
        def parse(self, data):
            # Aquí podrías usar xml.etree.ElementTree o similar
            return f"Parsed XML: {data}"

    # Factory
    class ParserFactory:
        @staticmethod
        def create_parser(type_):
            if type_ == "json":
                return JSONParser()
            elif type_ == "xml":
                return XMLParser()
            else:
                raise ValueError("Parser no soportado")

    # Uso
    if __name__ == "__main__":
        json_parser = ParserFactory.create_parser("json")
        print(json_parser.parse('{"name": "ChatGPT", "type": "AI"}'))

        xml_parser = ParserFactory.create_parser("xml")
        print(xml_parser.parse("<name>ChatGPT</name>"))
  ```

- ### Builder

  El patrón Builder construye objetos complejos paso a paso, permitiendo una creación flexible y controlada. Es especialmente útil para construir DTOs, consultas SQL complejas o configuraciones de objetos. Un ejemplo real es RequestBuilder().setUrl().setHeaders().build(). Es importante en APIs, desarrollo frontend y configuración de clases.

  ```go
    package main

    import "fmt"

    // Producto complejo: Request HTTP simulado
    type Request struct {
        URL     string
        Headers map[string]string
        Body    string
    }

    // Builder para construir Request paso a paso
    type RequestBuilder struct {
        request *Request
    }

    func NewRequestBuilder() *RequestBuilder {
        return &RequestBuilder{request: &Request{Headers: make(map[string]string)}}
    }

    func (b *RequestBuilder) SetURL(url string) *RequestBuilder {
        b.request.URL = url
        return b
    }

    func (b *RequestBuilder) AddHeader(key, value string) *RequestBuilder {
        b.request.Headers[key] = value
        return b
    }

    func (b *RequestBuilder) SetBody(body string) *RequestBuilder {
        b.request.Body = body
        return b
    }

    func (b *RequestBuilder) Build() *Request {
        return b.request
    }

    // Uso
    func main() {
        builder := NewRequestBuilder()
        req := builder.
            SetURL("https://api.example.com/data").
            AddHeader("Authorization", "Bearer token123").
            AddHeader("Content-Type", "application/json").
            SetBody(`{"key":"value"}`).
            Build()

        fmt.Println("Request URL:", req.URL)
        fmt.Println("Headers:", req.Headers)
        fmt.Println("Body:", req.Body)
    }
  ```

## 1.2. Patrones Estructurales

Enfocados en cómo se organizan las clases y objetos.

- ### Adapter

  El patrón Adapter permite que una clase con una interfaz incompatible funcione con otra esperada por el cliente. Es comúnmente utilizado para integrar APIs externas o sistemas legacy. Un ejemplo real es adaptar un servicio REST a una interfaz local. Es especialmente importante en entornos con microservicios, pruebas o cuando se trabaja con librerías de terceros.

  ```js
  // Interfaz local esperada por tu app
  class LocalUserService {
    getUser(id) {
      throw new Error("Método no implementado");
    }
  }

  // Este es un servicio externo (simulado)
  class ExternalUserApi {
    fetchUserFromApi(userId) {
      return Promise.resolve({ id: userId, name: "Usuario desde API" });
    }
  }

  // El Adapter hace que ExternalUserApi funcione como LocalUserService
  class UserServiceAdapter extends LocalUserService {
    constructor() {
      super();
      this.externalApi = new ExternalUserApi();
    }

    async getUser(id) {
      return await this.externalApi.fetchUserFromApi(id);
    }
  }

  (async () => {
    const userService = new UserServiceAdapter();
    const user = await userService.getUser(123);
    console.log(user); // { id: 123, name: 'Usuario desde API' }
  })();
  ```

- ### Decorator

  El patrón Decorator permite agregar funcionalidades a un objeto sin modificar su estructura original. Es ideal para tareas como logging, autorización y caching. Un ejemplo real sería @WithCache o @AuthRequired. Es ampliamente utilizado en el backend, especialmente en middlewares de frameworks como Express, Go Fiber o Flask.

  ```py
    def get_user_data(user_id):
        return f"Datos del usuario con ID {user_id}"

    def auth_required(func):
        def wrapper(user_id, is_authenticated):
            if not is_authenticated:
                return "❌ Acceso denegado: autenticación requerida"
            return func(user_id)
        return wrapper

    def log_request(func):
        def wrapper(*args, **kwargs):
            print(f"📘 Llamando a {func.__name__} con args={args} kwargs={kwargs}")
            result = func(*args, **kwargs)
            print(f"✅ Resultado: {result}")
            return result
        return wrapper

    @log_request
    @auth_required
    def get_user_data(user_id):
        return f"Datos del usuario con ID {user_id}"

    print(get_user_data(101, True))     # ✅ Autenticado
    print(get_user_data(102, False))    # ❌ No autenticado
  ```

- ### Facade

  El patrón Facade proporciona una interfaz simple y unificada para interactuar con un subsistema complejo. Es ideal para simplificar llamadas a múltiples servicios, ocultando la complejidad detrás de un método fácil de usar. Un ejemplo real es PaymentService.processPayment(), que internamente coordina validaciones, interacción con el banco y envío de notificaciones. Este patrón es crucial en APIs, microservicios y SDKs.

  ```go
    package main

    import (
        "fmt"
    )

    type BankAPI struct{}

    func (b *BankAPI) Charge(cardNumber string, amount float64) bool {
        fmt.Printf("💳 Banco: Cobro de $%.2f a la tarjeta %s\n", amount, cardNumber)
        return true // Simulación
    }

    type Validator struct{}

    func (v *Validator) ValidateCard(cardNumber string) bool {
        fmt.Printf("✅ Validación: Tarjeta %s válida\n", cardNumber)
        return true
    }

    type Notifier struct{}

    func (n *Notifier) SendReceipt(email string, amount float64) {
        fmt.Printf("📧 Notificación: Enviando recibo de $%.2f a %s\n", amount, email)
    }

    type PaymentService struct {
        bank     *BankAPI
        validator *Validator
        notifier *Notifier
    }

    func NewPaymentService() *PaymentService {
        return &PaymentService{
            bank:     &BankAPI{},
            validator: &Validator{},
            notifier: &Notifier{},
        }
    }

    func (ps *PaymentService) ProcessPayment(cardNumber, email string, amount float64) bool {
        fmt.Println("🔁 Procesando pago...")

        if !ps.validator.ValidateCard(cardNumber) {
            fmt.Println("❌ Tarjeta inválida")
            return false
        }

        if ps.bank.Charge(cardNumber, amount) {
            ps.notifier.SendReceipt(email, amount)
            fmt.Println("✅ Pago procesado con éxito")
            return true
        }

        fmt.Println("❌ Fallo en el proceso de pago")
        return false
    }

    func main() {
        paymentService := NewPaymentService()
        paymentService.ProcessPayment("4111-1111-1111-1111", "cliente@ejemplo.com", 49.99)
    }
  ```

## 1.3. Patrones Comportamentales

Describen cómo los objetos interactúan entre sí.

- ### Observer

  El patrón Observer permite que varios objetos se suscriban a un sujeto (observable) y sean notificados automáticamente cuando ocurre un evento. Es muy útil para manejar eventos, UI reactiva y comunicación mediante WebSockets. Un ejemplo real es EventEmitter.on('login'). Es esencial en frontend (React, Vue), eventos en backend (Node.js), y en tiempo real con sockets.

  ```js
  class EventEmitter {
    constructor() {
      this.events = {};
    }

    // Suscribirse a un evento
    on(event, listener) {
      if (!this.events[event]) {
        this.events[event] = [];
      }
      this.events[event].push(listener);
    }

    // Notificar a todos los suscriptores
    emit(event, data) {
      if (this.events[event]) {
        this.events[event].forEach((listener) => listener(data));
      }
    }

    // Cancelar la suscripción
    off(event, listenerToRemove) {
      if (!this.events[event]) return;
      this.events[event] = this.events[event].filter(
        (listener) => listener !== listenerToRemove
      );
    }
  }

  const emitter = new EventEmitter();

  function onLogin(user) {
    console.log(`👋 Bienvenido, ${user.name}`);
  }

  function logLogin(user) {
    console.log(`📝 Registro: Usuario ${user.name} inició sesión`);
  }

  // Suscribirse al evento
  emitter.on("login", onLogin);
  emitter.on("login", logLogin);

  // Disparar evento
  emitter.emit("login", { name: "Carlos" });

  // Desuscribirse
  emitter.off("login", onLogin);

  // Disparar de nuevo (solo queda 1 listener)
  emitter.emit("login", { name: "Ana" });
  ```

- ### Strategy en Go

  El patrón Strategy permite seleccionar dinámicamente entre diferentes algoritmos o comportamientos en tiempo de ejecución. En lugar de condicionar con múltiples if, encapsulas cada estrategia en una clase o función intercambiable. Es común en validaciones, autenticación o lógica de negocio flexible. Un ejemplo real sería AuthStrategy = JWT | OAuth | APIKey.

  ```py
    from abc import ABC, abstractmethod

    class AuthStrategy(ABC):
    @abstractmethod
    def authenticate(self, request):
        pass

    class JWTAuth(AuthStrategy):
    def authenticate(self, request):
        token = request.get("token")
        print(f"🔐 Autenticando con JWT: {token}")
        return token == "jwt123"  # Simulación


    class OAuthAuth(AuthStrategy):
        def authenticate(self, request):
            code = request.get("oauth_code")
            print(f"🔐 Autenticando con OAuth: {code}")
            return code == "oauth456"  # Simulación


    class APIKeyAuth(AuthStrategy):
        def authenticate(self, request):
            key = request.get("api_key")
            print(f"🔐 Autenticando con API Key: {key}")
            return key == "apikey789"  # Simulación

    class Authenticator:
    def __init__(self, strategy: AuthStrategy):
        self.strategy = strategy

    def set_strategy(self, strategy: AuthStrategy):
        self.strategy = strategy

    def login(self, request):
        success = self.strategy.authenticate(request)
        if success:
            print("✅ Autenticación exitosa")
        else:
            print("❌ Fallo en autenticación")

    if __name__ == "__main__":
    auth = Authenticator(JWTAuth())
    auth.login({"token": "jwt123"})

    auth.set_strategy(OAuthAuth())
    auth.login({"oauth_code": "oauth456"})

    auth.set_strategy(APIKeyAuth())
    auth.login({"api_key": "apikey789"})
  ```

- ### Command

  El patrón Command encapsula una solicitud o acción como un objeto, permitiendo parametrizar métodos con diferentes acciones, ponerlas en cola o deshacerlas. Es muy útil para implementar colas de tareas, historial de acciones o sistemas CQRS. Un ejemplo real sería CommandQueue.Enqueue(UploadFileCommand).

  ```go
    package main

    import "fmt"

    type Command interface {
      Execute()
    }

    type UploadFileCommand struct {
        filename string
    }

    func (c *UploadFileCommand) Execute() {
        fmt.Printf("⬆️ Subiendo archivo %s...\n", c.filename)
        // Aquí iría la lógica real de subir archivo
    }

    type DeleteFileCommand struct {
        filename string
    }

    func (c *DeleteFileCommand) Execute() {
        fmt.Printf("🗑 Eliminando archivo %s...\n", c.filename)
        // Aquí iría la lógica real de eliminar archivo
    }

    type CommandQueue struct {
        commands []Command
    }

    func (q *CommandQueue) Enqueue(cmd Command) {
        q.commands = append(q.commands, cmd)
    }

    func (q *CommandQueue) Run() {
        for _, cmd := range q.commands {
            cmd.Execute()
        }
        // Limpiar cola después de ejecutar
        q.commands = []Command{}
    }

    func main() {
        queue := &CommandQueue{}

        queue.Enqueue(&UploadFileCommand{filename: "documento.pdf"})
        queue.Enqueue(&DeleteFileCommand{filename: "imagen.png"})

        queue.Run()
    }
  ```

- ### Chain of Responsibility

  El patrón Chain of Responsibility permite pasar una solicitud a través de una cadena de manejadores hasta que uno la procese o todos la recorran. Es muy usado en middlewares, pipelines de validación o procesamiento. Un ejemplo real es una request HTTP que pasa por autenticación, logging y finalmente responde.

  ```js
  class Handler {
    setNext(handler) {
      this.nextHandler = handler;
      return handler;
    }

    handle(request) {
      if (this.nextHandler) {
        return this.nextHandler.handle(request);
      }
      return null;
    }
  }

  class AuthHandler extends Handler {
    handle(request) {
      if (!request.user) {
        return "❌ No autorizado";
      }
      console.log("🔐 Autenticación exitosa");
      return super.handle(request);
    }
  }

  class LoggerHandler extends Handler {
    handle(request) {
      console.log(`📝 Logueando request para usuario ${request.user}`);
      return super.handle(request);
    }
  }

  class ResponseHandler extends Handler {
    handle(request) {
      console.log("✅ Procesando respuesta");
      return "Respuesta enviada";
    }
  }

  const auth = new AuthHandler();
  const logger = new LoggerHandler();
  const response = new ResponseHandler();

  // Construir la cadena
  auth.setNext(logger).setNext(response);

  // Probar request con usuario válido
  let result = auth.handle({ user: "Carlos" });
  console.log(result);

  // Probar request sin usuario
  result = auth.handle({});
  console.log(result);
  ```
