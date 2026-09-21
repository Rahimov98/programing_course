# Python · Урок 16. Наследование и магические методы

## Цели урока
- Создавать классы-наследники
- Переопределять методы, вызывать `super()`
- Использовать магические методы

## Наследование
```python
class Animal:
    def __init__(self, name):
        self.name = name

    def speak(self):
        return "..."

class Dog(Animal):
    def speak(self):
        return "Гав!"

class Cat(Animal):
    def __init__(self, name, color):
        super().__init__(name)      # вызов конструктора родителя
        self.color = color

    def speak(self):
        return "Мяу!"

for a in [Dog("Рекс"), Cat("Мурка", "серая")]:
    print(a.name, a.speak())        # полиморфизм
```

Проверки: `isinstance(a, Animal)`, `issubclass(Dog, Animal)`.

## Магические методы
```python
class Vector:
    def __init__(self, x, y):
        self.x, self.y = x, y

    def __add__(self, other):
        return Vector(self.x + other.x, self.y + other.y)

    def __eq__(self, other):
        return self.x == other.x and self.y == other.y

    def __len__(self):
        return 2

    def __repr__(self):
        return f"Vector({self.x}, {self.y})"

print(Vector(1, 2) + Vector(3, 4))   # Vector(4, 6)
```
Часто используют: `__str__`, `__repr__`, `__eq__`, `__lt__`, `__len__`, `__getitem__`, `__add__`.

## Типичные ошибки
- Не вызвали `super().__init__()` — родительские атрибуты не создались
- Глубокие иерархии наследования — лучше композиция
- Путаница `__str__` (для пользователя) и `__repr__` (для разработчика)

## Практика
1. Иерархия `Shape` → `Circle`, `Square` с методом `area()`.
2. Класс `Employee` и наследник `Manager` с бонусом.
3. Реализуйте сравнение `<` для класса `Student` по среднему баллу.

## Проверь себя
1. Что делает `super()`?
2. Что такое полиморфизм?
3. Зачем нужен `__repr__`?

---
[← Урок 15](lesson-15.md) · [Программа курса](README.md) · [Урок 17 →](lesson-17.md)
