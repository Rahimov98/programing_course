# Python · Урок 15. ООП: классы и объекты

## Цели урока
- Создавать классы и объекты
- Понимать атрибуты, методы и `self`

## Теория
Класс — шаблон, объект — его экземпляр.

```python
class Student:
    school = "Университет"          # атрибут класса

    def __init__(self, name, age):  # конструктор
        self.name = name            # атрибуты объекта
        self.age = age
        self.grades = []

    def add_grade(self, grade):
        self.grades.append(grade)

    def average(self):
        return sum(self.grades) / len(self.grades) if self.grades else 0

    def __str__(self):
        return f"{self.name} ({self.age})"

s = Student("Алишер", 21)
s.add_grade(5)
s.add_grade(4)
print(s, s.average())   # Алишер (21) 4.5
```

**Инкапсуляция по соглашению**
```python
class Account:
    def __init__(self, balance):
        self._balance = balance      # «защищённый» атрибут

    @property
    def balance(self):
        return self._balance

    def deposit(self, amount):
        if amount > 0:
            self._balance += amount
```

**Статические методы и методы класса**
```python
class Math:
    @staticmethod
    def add(a, b):
        return a + b
```

## Типичные ошибки
- Забыли `self` в первом параметре метода
- Атрибут создан без `self.` — виден только внутри метода
- Изменяемые атрибуты класса (списки) общие для всех объектов

## Практика
1. Класс `Rectangle` с методами `area()` и `perimeter()`.
2. Класс `BankAccount` с пополнением и снятием (без ухода в минус).
3. Класс `Book`, `__str__` выводит «Название — Автор».

## Проверь себя
1. Что делает `__init__`?
2. Для чего нужен `self`?
3. Чем атрибут класса отличается от атрибута объекта?

---
[← Урок 14](lesson-14.md) · [Программа курса](README.md) · [Урок 16 →](lesson-16.md)
