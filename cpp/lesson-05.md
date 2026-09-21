# C++ · Урок 5. Условия: if / else и switch

## Цели урока
- Принимать решения в программе

## if / else if / else
```cpp
#include <iostream>
using namespace std;

int main() {
    int age;
    cout << "Возраст: ";
    cin >> age;

    if (age < 12) {
        cout << "Ребёнок\n";
    } else if (age < 18) {
        cout << "Подросток\n";
    } else if (age < 65) {
        cout << "Взрослый\n";
    } else {
        cout << "Пожилой\n";
    }
    return 0;
}
```

## Сложные условия
```cpp
if (age >= 18 && hasPassport) { /* ... */ }
if (!(x > 0)) { /* x <= 0 */ }
```

## Тернарный оператор
```cpp
string status = (age >= 18) ? "взрослый" : "несовершеннолетний";
```

## switch
Работает с целыми числами и символами:
```cpp
char op;
double a, b;
cin >> a >> op >> b;

switch (op) {
    case '+': cout << a + b << "\n"; break;
    case '-': cout << a - b << "\n"; break;
    case '*': cout << a * b << "\n"; break;
    case '/':
        if (b != 0) cout << a / b << "\n";
        else cout << "Деление на ноль\n";
        break;
    default:
        cout << "Неизвестная операция\n";
}
```
Без `break` выполнение «проваливается» в следующий `case`.

## if с инициализацией (C++17)
```cpp
if (int n = compute(); n > 0) { cout << n; }
```

## Типичные ошибки
- Точка с запятой после `if (...);` — блок выполняется всегда
- Забыли `break` в `switch`
- `=` вместо `==`

## Практика
1. Калькулятор на `switch` с обработкой деления на ноль.
2. Программа определяет тип треугольника по трём сторонам.
3. Определите, високосный ли год.

## Проверь себя
1. Для каких типов работает `switch`?
2. Что произойдёт без `break`?
3. Как записать «x от 1 до 10 включительно»?

---
[← Урок 4](lesson-04.md) · [Программа курса](README.md) · [Урок 6 →](lesson-06.md)
