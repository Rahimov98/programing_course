# C++ · Урок 19. Полиморфизм и виртуальные функции

## Цели урока
- Вызывать нужную реализацию метода через указатель на базовый класс
- Писать абстрактные классы

## Проблема
```cpp
Animal* a = new Dog("Рекс", "овчарка");
a->speak();      // без virtual вызовется Animal::speak!
```

## virtual и override
```cpp
#include <iostream>
#include <memory>
#include <vector>

class Shape {
public:
    virtual double area() const = 0;         // чисто виртуальная → класс абстрактный
    virtual void print() const {
        std::cout << "Площадь: " << area() << "\n";
    }
    virtual ~Shape() = default;              // виртуальный деструктор обязателен
};

class Circle : public Shape {
    double r;
public:
    Circle(double r) : r(r) {}
    double area() const override { return 3.14159 * r * r; }
};

class Rect : public Shape {
    double w, h;
public:
    Rect(double w, double h) : w(w), h(h) {}
    double area() const override { return w * h; }
};

int main() {
    std::vector<std::unique_ptr<Shape>> shapes;
    shapes.push_back(std::make_unique<Circle>(2));
    shapes.push_back(std::make_unique<Rect>(3, 4));

    for (const auto& s : shapes) s->print();     // вызывается нужная версия
}
```

## Ключевые правила
- `virtual` — вызов определяется типом **объекта**, а не указателя (позднее связывание)
- `override` — компилятор проверит, что вы действительно переопределяете виртуальный метод
- Класс с хотя бы одной чисто виртуальной функцией (`= 0`) — **абстрактный**, создать его объект нельзя
- **Деструктор базового класса должен быть виртуальным**, иначе `delete` через указатель на базовый класс не вызовет деструктор наследника

## Интерфейсы
Класс только с чисто виртуальными функциями играет роль интерфейса:
```cpp
class ILogger {
public:
    virtual void log(const std::string& msg) = 0;
    virtual ~ILogger() = default;
};
```

## dynamic_cast
```cpp
if (auto* c = dynamic_cast<Circle*>(shape.get())) { /* это круг */ }
```

## Типичные ошибки
- Забыли `virtual` у деструктора базового класса
- Разные сигнатуры (например, отсутствие `const`) — метод не переопределяется; `override` найдёт такую ошибку
- Хранение объектов производных классов в `vector<Shape>` — «срезка», нужны указатели

## Практика
1. Иерархия `Shape` с `Triangle`; найдите фигуру с наибольшей площадью.
2. Интерфейс `IPayment` и реализации `Card`, `Cash`.
3. Абстрактный класс `Employee` с виртуальным `salary()`.

## Проверь себя
1. Что делает `virtual`?
2. Почему деструктор должен быть виртуальным?
3. Что такое абстрактный класс?

---
[← Урок 18](lesson-18.md) · [Программа курса](README.md) · [Урок 20 →](lesson-20.md)
