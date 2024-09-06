# Patrones de Diseño en Go

Los patrones de diseño son soluciones reutilizables a problemas comunes en el desarrollo de software. Go, con su enfoque en la eficiencia y la simplicidad, se presta bien para la aplicación de estos patrones.

## Patrones Creacionales

Se enfoca en cómo crear objetos. Define diferentes formas de instanciar objetos, haciendo el proceso más flexible y reutilizable.

_Singleton:_ Garantiza que una clase solo tenga una instancia y proporciona un punto de acceso global a ella.
_Factory:_ Abstrae la creación de objetos, permitiendo cambiar el tipo de objeto creado sin modificar el código cliente.
_Abstract Factory:_ Proporciona una interfaz para crear familias de objetos relacionados o dependientes sin especificar sus clases concretas.  
_Builder:_ Separa la construcción de un objeto complejo de su representación, permitiendo crear diferentes representaciones del mismo objeto.

## Patrones Estructurales

Se ocupa de cómo las clases y objetos se combinan para formar estructuras más grandes. Definen maneras de componer objetos para formar estructuras más complejas.

_Adapter:_ Convierte la interfaz de una clase en otra interfaz que los clientes esperan.
_Decorator:_ Agrega responsabilidades adicionales a un objeto dinámicamente.
_Proxy:_ Proporciona un sustituto para otro objeto para controlar el acceso a él.

## Patrones Comportamentales

Describe cómo las clases y objetos interactúan. Se enfoca en la asignación de responsabilidades entre objetos y cómo se comunican.

_Observer:_ Define una dependencia uno a muchos entre objetos, de modo que cuando un objeto cambia de estado, todos sus dependientes son notificados y actualizados automáticamente.  
_Strategy:_ Define una familia de algoritmos, encapsula cada uno y los hace intercambiables.  
_Command:_ Encapsula una solicitud como un objeto, lo que permite parametrizar clientes con diferentes solicitudes, encolar o registrar solicitudes, y apoyar operaciones reversibles.

## Arquitecturas de Software

La arquitectura de software es la estructura de alto nivel de un sistema de software. Define cómo se organizan los componentes del sistema y cómo interactúan entre sí.

_MVC (Model-View-Controller):_ Separa la aplicación en tres componentes principales: Modelo (datos), Vista (interfaz de usuario) y Controlador (lógica de negocio).
_MVVM (Model-View-ViewModel):_ Similar a MVC, pero introduce un ViewModel para actuar como intermediario entre el Modelo y la Vista, mejorando la testabilidad y la mantenibilidad.
_Microservicios:_ Divide una aplicación en pequeños servicios independientes que se comunican a través de APIs.
_Arquitectura Hexagonal:_ También conocida como Ports and Adapters, enfoca la aplicación en su núcleo de negocio y lo aísla de los detalles externos como la persistencia de datos y la interfaz de usuario.
