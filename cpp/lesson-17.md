# C++ · Урок 17. Инкапсуляция и перегрузка операторов

## Цели урока
- Перегружать операторы для своих классов
- Использовать `friend` и статические члены

## Перегрузка операторов
```cpp
#include <iostream>

class Vector2 {
public:
    double x, y;
    Vector2(double x = 0, double y = 0) : x(x), y(y) {}

    Vector2 operator+(const Vector2& o) const { return {x + o.x, y + o.y}; }
    Vector2 operator-(const Vector2& o) const { return {x - o.x, y - o.y}; }
    Vector2 operator*(double k) const { return {x * k, y * k}; }
    bool operator==(const Vector2& o) const { return x == o.x && y == o.y; }
    Vector2& operator+=(const Vector2& o) { x += o.x; y += o.y; return *this; }
};

int main() {
    Vector2 a(1, 2), b(3, 4);
    Vector2 c = a + b * 2;
    std::cout << c.x << ", " << c.y << "\n";     // 7, 10
}
```

## Оператор вывода `<<`
Перегружается как внешняя функция:
```cpp
std::ostream& operator<<(std::ostream& os, const Vector2& v) {
    return os << "(" << v.x << ", " << v.y << ")";
}
std::cout << a + b << "\n";
```

## Оператор индексации и вызова
```cpp
class Array3 {
    int data[3]{};
public:
    int& operator[](int i) { return data[i]; }
    const int& operator[](int i) const { return data[i]; }
};
```

## friend
Дружественная функция имеет доступ к `private`:
```cpp
class Money {
    int cents;
public:
    Money(int c) : cents(c) {}
    friend std::ostream& operator<<(std::ostream& os, const Money& m) {
        return os << m.cents / 100 << "." << m.cents % 100;
    }
};
```

## static
```cpp
class Counter {
    static int count;            // одно значение на весь класс
public:
    Counter() { ++count; }
    static int getCount() { return count; }
};
int Counter::count = 0;          // определение вне класса

Counter a, b;
std::cout << Counter::getCount();   // 2
```

## Что нельзя перегружать
`::`, `.`, `.*`, `?:`, `sizeof`. Не меняйте привычный смысл операторов (`+` не должен вычитать).

## Типичные ошибки
- `operator+` не помечен `const`
- `operator=` без проверки самоприсваивания
- Перегрузка ради перегрузки — ухудшает читаемость

## Практика
1. Класс `Fraction` (дробь) с операторами `+`, `-`, `*`, `/`, `<<`.
2. Класс `Complex` (комплексные числа).
3. Класс `Money` с операторами сравнения и `+=`.

## Проверь себя
1. Как перегрузить `<<` для вывода объекта?
2. Что такое `friend`?
3. Чем `static` поле отличается от обычного?

---
[← Урок 16](lesson-16.md) · [Программа курса](README.md) · [Урок 18 →](lesson-18.md)
