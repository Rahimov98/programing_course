# C++ · Урок 3. Ввод и вывод (cin / cout)

## Цели урока
- Считывать данные с клавиатуры
- Форматировать вывод

## cin и cout
```cpp
#include <iostream>
#include <string>

int main() {
    std::string name;
    int age;

    std::cout << "Как вас зовут? ";
    std::cin >> name;
    std::cout << "Сколько вам лет? ";
    std::cin >> age;

    std::cout << "Привет, " << name << "! Через 5 лет вам будет " << age + 5 << "\n";
    return 0;
}
```
`>>` считывает до пробела. Для целой строки используйте `getline`:
```cpp
std::string fullName;
std::cin >> age;
std::cin.ignore();                     // убрать оставшийся '\n'
std::getline(std::cin, fullName);
```

## using namespace std
```cpp
using namespace std;    // тогда можно писать cout вместо std::cout
```
В учебных программах это допустимо, в больших проектах — не рекомендуется.

## Форматирование
```cpp
#include <iomanip>

double pi = 3.14159265;
std::cout << std::fixed << std::setprecision(2) << pi << "\n";   // 3.14
std::cout << std::setw(8) << 42 << "\n";                          // "      42"
std::cout << std::setfill('0') << std::setw(5) << 7 << "\n";      // 00007
```

## Проверка успешности ввода
```cpp
int n;
if (!(std::cin >> n)) {
    std::cout << "Это не число\n";
    std::cin.clear();
    std::cin.ignore(10000, '\n');
}
```

## Типичные ошибки
- После `cin >> x` в потоке остаётся `\n` — `getline` читает пустую строку
- Забыли `#include <string>` или `<iomanip>`
- Ввод буквы вместо числа «ломает» поток

## Практика
1. Считайте два числа и выведите сумму, разность, произведение и частное (с двумя знаками).
2. Считайте имя и фамилию одной строкой через `getline`.
3. Выведите таблицу из 3 столбцов с выравниванием через `setw`.

## Проверь себя
1. Чем `cin >> s` отличается от `getline`?
2. Для чего нужен `cin.ignore()`?
3. Как вывести число с тремя знаками после запятой?

---
[← Урок 2](lesson-02.md) · [Программа курса](README.md) · [Урок 4 →](lesson-04.md)
