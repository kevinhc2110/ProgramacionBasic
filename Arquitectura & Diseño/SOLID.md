# Principios SOLID

## Introducción a SOLID

SOLID es un conjunto de principios de diseño de software que mejora la legibilidad, escalabilidad y mantenibilidad del código. Estos principios fueron introducidos por Robert C. Martin (Uncle Bob) y se aplican principalmente en programación orientada a objetos.

### Los principios SOLID son

1. **S** - Single Responsibility Principle (SRP)
2. **O** - Open/Closed Principle (OCP)
3. **L** - Liskov Substitution Principle (LSP)
4. **I** - Interface Segregation Principle (ISP)
5. **D** - Dependency Inversion Principle (DIP)

## 1. **Single Responsibility Principle (SRP)**

Cada clase o módulo debe tener una única responsabilidad o motivo para cambiar. Esto significa que debe existir una única razón para que un módulo o clase sea modificado.

### Ejemplo en Go (SRP)

```go
package main

import "fmt"

// Mala práctica: Esta clase tiene más de una responsabilidad
type User struct {
    name     string
    email    string
}

func (u *User) save() {
    fmt.Println("Saving user to the database")
}

func (u *User) sendEmail() {
    fmt.Println("Sending email to user")
}

// Buena práctica: Separar las responsabilidades
type User struct {
    name  string
    email string
}

type UserRepository struct{}

func (r *UserRepository) save(u *User) {
    fmt.Println("Saving user to the database")
}

type EmailService struct{}

func (e *EmailService) sendEmail(u *User) {
    fmt.Println("Sending email to user")
}
```

### Ejemplo en Python (SRP)

```py
# Violando SRP: la clase hace demasiado
class User:
    def __init__(self, name, email):
        self.name = name
        self.email = email

    def save_to_database(self):
        # Lógica para guardar usuario en la base de datos
        pass

    def send_welcome_email(self):
        # Lógica para enviar correo de bienvenida
        pass

# Correcto: clases separadas para responsabilidades distintas
class User:
    def __init__(self, name, email):
        self.name = name
        self.email = email

class UserRepository:
    def save_to_database(self, user):
        # Lógica para guardar usuario en la base de datos
        pass

class EmailService:
    def send_welcome_email(self, user):
        # Lógica para enviar correo de bienvenida
        pass

```

### Ejemplo en Typescript (SRP)

```ts
// Violando SRP
class User {
  constructor(public name: string, public email: string) {}

  saveToDatabase() {
    console.log("Saving user to the database");
  }

  sendEmail() {
    console.log("Sending welcome email");
  }
}

// Correcto: separación de responsabilidades

class User {
  constructor(public name: string, public email: string) {}
}

class UserRepository {
  save(user: User) {
    console.log(`Saving user ${user.name} to the database`);
  }
}

class EmailService {
  sendWelcomeEmail(user: User) {
    console.log(`Sending welcome email to ${user.email}`);
  }
}
```

## 2. **Open/Closed Principle (OCP)**

Las clases deben estar abiertas para la extensión pero cerradas para la modificación. Esto significa que podemos extender el comportamiento de una clase sin modificar su código fuente.

### Ejemplo en Go (OCP)

```go
// Violando OCP: modificamos la clase para añadir funcionalidad
type Shape struct {
    Type string
}

func (s Shape) Area() float64 {
    if s.Type == "circle" {
        return 3.14 * 5 * 5 // Área de círculo
    }
    if s.Type == "square" {
        return 4 * 4 // Área de cuadrado
    }
    return 0
}

// Correcto: clases extendidas para diferentes formas
type Shape interface {
    Area() float64
}

type Circle struct {
    Radius float64
}

func (c Circle) Area() float64 {
    return 3.14 * c.Radius * c.Radius
}

type Square struct {
    Side float64
}

func (s Square) Area() float64 {
    return s.Side * s.Side
}

```

### Ejemplo en Python (OCP)

```py
# Violando OCP: modificamos la clase para añadir funcionalidad
class Shape:
    def __init__(self, shape_type):
        self.shape_type = shape_type

    def area(self):
        if self.shape_type == "circle":
            return 3.14 * 5 * 5  # Área de círculo
        elif self.shape_type == "square":
            return 4 * 4  # Área de cuadrado
        return 0

# Correcto: clases extendidas para diferentes formas
class Shape:
    def area(self):
        pass

class Circle(Shape):
    def __init__(self, radius):
        self.radius = radius

    def area(self):
        return 3.14 * self.radius * self.radius

class Square(Shape):
    def __init__(self, side):
        self.side = side

    def area(self):
        return self.side * self.side

```

### Ejemplo en Typescript (OCP)

```ts
// Violando OCP
class Shape {
  constructor(public type: string) {}

  area(): number {
    if (this.type === "circle") {
      return Math.PI * 5 * 5;
    } else if (this.type === "square") {
      return 4 * 4;
    }
    return 0;
  }
}

// Correcto
interface Shape {
  area(): number;
}

class Circle implements Shape {
  constructor(public radius: number) {}

  area(): number {
    return Math.PI * this.radius * this.radius;
  }
}

class Square implements Shape {
  constructor(public side: number) {}

  area(): number {
    return this.side * this.side;
  }
}
```

## 3. **Liskov Substitution Principle (LSP)**

Los objetos de una clase base deben poder ser reemplazados por objetos de sus subclases sin alterar el comportamiento correcto del programa.

### Ejemplo en Go (LSP)

```go
// Violando LSP: Square altera el comportamiento de Rectangle
type Rectangle struct {
    Width, Height float64
}

func (r Rectangle) Area() float64 {
    return r.Width * r.Height
}

type Square struct {
    Rectangle
}

func (s Square) Area() float64 {
    // Lógica incorrecta para área de cuadrado
    return s.Width * s.Width
}

// Correcto: Square y Rectangle siguen comportamientos adecuados
type Shape interface {
    Area() float64
}

type Rectangle struct {
    Width, Height float64
}

func (r Rectangle) Area() float64 {
    return r.Width * r.Height
}

type Square struct {
    Side float64
}

func (s Square) Area() float64 {
    return s.Side * s.Side
}

```

### Ejemplo en Python (LSP)

```py
# Violando LSP: Square altera el comportamiento de Rectangle
class Rectangle:
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

class Square(Rectangle):
    def __init__(self, side):
        super().__init__(side, side)

    def area(self):
        return self.width * self.width  # Lógica incorrecta

# Correcto: Square y Rectangle siguen comportamientos adecuados
class Shape:
    def area(self):
        pass

class Rectangle(Shape):
    def __init__(self, width, height):
        self.width = width
        self.height = height

    def area(self):
        return self.width * self.height

class Square(Shape):
    def __init__(self, side):
        self.side = side

    def area(self):
        return self.side * self.side

```

### Ejemplo en Typescript (LSP)

```ts
// Violando LSP
class Rectangle {
  constructor(public width: number, public height: number) {}

  area(): number {
    return this.width * this.height;
  }
}

class Square extends Rectangle {
  constructor(side: number) {
    super(side, side);
  }
}

// Correcto
interface Shape {
  area(): number;
}

class Rectangle implements Shape {
  constructor(public width: number, public height: number) {}

  area(): number {
    return this.width * this.height;
  }
}

class Square implements Shape {
  constructor(public side: number) {}

  area(): number {
    return this.side * this.side;
  }
}
```

## 4. **Interface Segregation Principle (ISP)**

Los clientes no deberían estar forzados a depender de interfaces que no utilizan. Es mejor tener interfaces pequeñas y específicas que una interfaz general y grande.

### Ejemplo en Go (ISP)

```go
// Violando ISP: la interfaz obliga a implementar métodos innecesarios
type Worker interface {
    Work()
    Eat()
}

type Developer struct{}

func (d Developer) Work() {
    // Lógica para trabajar
}

func (d Developer) Eat() {
    // No necesita comer en este contexto
}

// Correcto: interfaces segregadas
type Worker interface {
    Work()
}

type Eater interface {
    Eat()
}

type Developer struct{}

func (d Developer) Work() {
    // Lógica para trabajar
}

```

### Ejemplo en Python (ISP)

```py
# Violando ISP: la clase debe implementar métodos que no necesita
class Worker:
    def work(self):
        pass

    def eat(self):
        pass

class Developer(Worker):
    def work(self):
        # Lógica para trabajar
        pass

    def eat(self):
        # No necesita comer
        pass

# Correcto: interfaces (protocolos) segregados
from abc import ABC, abstractmethod

class Worker(ABC):
    @abstractmethod
    def work(self):
        pass

class Eater(ABC):
    @abstractmethod
    def eat(self):
        pass

class Developer(Worker):
    def work(self):
        # Lógica para trabajar
        pass

```

### Ejemplo en Typescript (ISP)

```ts
// Violando ISP
interface Worker {
  work(): void;
  eat(): void;
}

class Developer implements Worker {
  work() {
    console.log("Coding...");
  }

  eat() {
    // No necesario en este contexto
  }
}

// Correcto
interface Workable {
  work(): void;
}

interface Eatable {
  eat(): void;
}

class Developer implements Workable {
  work() {
    console.log("Coding...");
  }
}

class Human implements Workable, Eatable {
  work() {
    console.log("Working...");
  }

  eat() {
    console.log("Eating...");
  }
}
```

## 5. **Dependency Inversion Principle (DIP)**

Las clases de alto nivel no deberían depender de clases de bajo nivel. Ambas deberían depender de abstracciones. Las abstracciones no deberían depender de los detalles, sino que los detalles deberían depender de las abstracciones.

### Ejemplo en Go (DIP)

```go
// Violando DIP: la clase de alto nivel depende directamente de la clase de bajo nivel
type MySQLDatabase struct{}

func (db MySQLDatabase) Connect() {
    // Conexión a base de datos MySQL
}

type App struct {
    db MySQLDatabase
}

func (a *App) Start() {
    a.db.Connect()
}

// Correcto: ambas clases dependen de una abstracción
type Database interface {
    Connect()
}

type MySQLDatabase struct{}

func (db MySQLDatabase) Connect() {
    // Conexión a base de datos MySQL
}

type App struct {
    db Database
}

func (a *App) Start() {
    a.db.Connect()
}

```

### Ejemplo en Python (DIP)

```py
# Violando DIP: la clase de alto nivel depende de una implementación de bajo nivel
class MySQLDatabase:
    def connect(self):
        # Conexión a base de datos MySQL
        pass

class App:
    def __init__(self, db):
        self.db = db

    def start(self):
        self.db.connect()

# Correcto: se usa una abstracción
class Database(ABC):
    @abstractmethod
    def connect(self):
        pass

class MySQLDatabase(Database):
    def connect(self):
        # Conexión a base de datos MySQL
        pass

class App:
    def __init__(self, db: Database):
        self.db = db

    def start(self):
        self.db.connect()

```

### Ejemplo en Typescript (DIP)

```ts
// Violando DIP
class MySQLDatabase {
  connect() {
    console.log("Connecting to MySQL...");
  }
}

class App {
  private db = new MySQLDatabase();

  start() {
    this.db.connect();
  }
}

// Correcto
interface Database {
  connect(): void;
}

class MySQLDatabase implements Database {
  connect() {
    console.log("Connecting to MySQL...");
  }
}

class PostgreSQLDatabase implements Database {
  connect() {
    console.log("Connecting to PostgreSQL...");
  }
}

class App {
  constructor(private db: Database) {}

  start() {
    this.db.connect();
  }
}

// Uso
const db = new MySQLDatabase();
const app = new App(db);
app.start();
```
