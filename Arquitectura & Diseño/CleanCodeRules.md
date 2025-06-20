# Clean code rules

## Separation of Concerns (SOC)

- Divide el sistema en partes que tengan responsabilidades independientes.
- Cada módulo o componente se enfoca en una única tarea o grupo de tareas relacionadas.
- Facilita mantenimiento, pruebas y reutilización.

```py
# Lógica de negocio
def calcular_precio_total(productos):
    return sum(p['precio'] for p in productos)

# Lógica de presentación (UI)
def mostrar_total(productos):
    total = calcular_precio_total(productos)
    print(f"Total: ${total}")
```

## Don’t Repeat Yourself (DRY)

- Evita la duplicación de código o lógica.
- Cada conocimiento debe tener una única representación en el sistema.
- Reduce errores y facilita cambios.

```py
def calcular_total(lista):
    return sum(p['precio'] for p in lista)

total1 = calcular_total(lista1)
total2 = calcular_total(lista2)
```

## Keep It Simple, Stupid (Don’t Repeat Yourself )

- Prefiere soluciones simples y claras sobre complejas.
- Evita complicar el código innecesariamente.
- Código sencillo es más fácil de entender y mantener.

```py
def es_par(n):
    return n % 2 == 0
```

## Test Driven Development (TDD)

- Primero escribes pruebas automatizadas que definen la funcionalidad deseada.
- Luego escribes el código mínimo para pasar esas pruebas.
- Después refactorizas manteniendo los tests.
- Promueve código más limpio y menos errores.

```py
import unittest

class TestSuma(unittest.TestCase):
    def test_suma(self):
        self.assertEqual(suma(2, 3), 5)
```

## You Aren’t Gonna Need It (YAGNI)

- No implementes funcionalidades hasta que realmente sean necesarias.
- Evita sobreingeniería y código inflado con funciones que no se usan.
- Mantiene el código más simple y manejable.
