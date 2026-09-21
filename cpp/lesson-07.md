# C++ · Урок 7. Функции

## Цели урока
- Выносить код в функции
- Понимать прототипы, перегрузку и значения по умолчанию

## Определение и вызов
```cpp
#include <iostream>

int square(int x) {
    return x * x;
}

void greet(const std::string& name) {
    std::cout << "Привет, " << name << "!\n";
}

int main() {
    std::cout << square(5) << "\n";
    greet("Мадина");
    return 0;
}
```
`void` — функция ничего не возвращает.

## Прототип (объявление)
Функция должна быть объявлена до использования:
```cpp
int add(int a, int b);          // прототип

int main() {
    std::cout << add(2, 3);
}

int add(int a, int b) {         // определение
    return a + b;
}
```
Обычно прототипы выносят в заголовочные файлы `.h`.

## Значения по умолчанию
```cpp
double power(double base, int exp = 2) {
    double r = 1;
    for (int i = 0; i < exp; i++) r *= base;
    return r;
}
power(3);      // 9
power(2, 10);  // 1024
```

## Перегрузка
Одно имя, разные параметры:
```cpp
int max(int a, int b)             { return a > b ? a : b; }
double max(double a, double b)    { return a > b ? a : b; }
```

## Область видимости
Локальные переменные существуют только внутри функции. Глобальных переменных стоит избегать.

## Рекурсия
```cpp
long long factorial(int n) {
    return n <= 1 ? 1 : n * factorial(n - 1);
}
```

## inline и constexpr
```cpp
constexpr int cube(int x) { return x * x * x; }   // может вычисляться при компиляции
```

## Типичные ошибки
- Забыли `return` в функции с не-`void` типом
- Вызвали функцию до её объявления
- Рекурсия без базового случая → переполнение стека

## Практика
1. `bool isPrime(int n)`.
2. `int gcd(int a, int b)` рекурсивно.
3. Перегрузите `print` для `int`, `double` и `std::string`.

## Проверь себя
1. Что такое прототип функции?
2. Что такое перегрузка?
3. Зачем нужен базовый случай в рекурсии?

---
[← Урок 6](lesson-06.md) · [Программа курса](README.md) · [Урок 8 →](lesson-08.md)
