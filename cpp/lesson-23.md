# C++ · Урок 23. Обработка исключений

## Цели урока
- Перехватывать и выбрасывать исключения
- Писать безопасный код

## try / catch / throw
```cpp
#include <iostream>
#include <stdexcept>

double divide(double a, double b) {
    if (b == 0) throw std::invalid_argument("Деление на ноль");
    return a / b;
}

int main() {
    try {
        std::cout << divide(10, 0);
    } catch (const std::invalid_argument& e) {
        std::cout << "Ошибка: " << e.what() << "\n";
    } catch (const std::exception& e) {
        std::cout << "Другая ошибка: " << e.what() << "\n";
    } catch (...) {
        std::cout << "Неизвестная ошибка\n";
    }
}
```
Перехватывайте исключения **по константной ссылке**.

## Стандартные исключения
Все наследуют `std::exception`: `std::runtime_error`, `std::logic_error`, `std::out_of_range`, `std::invalid_argument`, `std::bad_alloc`.

```cpp
std::vector<int> v{1, 2, 3};
try {
    v.at(10);
} catch (const std::out_of_range& e) {
    std::cout << e.what();
}

try {
    int n = std::stoi("abc");
} catch (const std::invalid_argument&) {
    std::cout << "Не число\n";
}
```

## Собственное исключение
```cpp
class InsufficientFunds : public std::runtime_error {
    double needed;
public:
    InsufficientFunds(double needed)
        : std::runtime_error("Недостаточно средств"), needed(needed) {}
    double getNeeded() const { return needed; }
};

void withdraw(double& balance, double amount) {
    if (amount > balance) throw InsufficientFunds(amount - balance);
    balance -= amount;
}
```

## Безопасность и RAII
При выбросе исключения вызываются деструкторы локальных объектов («раскрутка стека»). Поэтому ресурсы нужно оборачивать в объекты (`vector`, `unique_ptr`, `ifstream`), а не управлять через голые `new/delete`.

## noexcept
```cpp
void safe() noexcept { /* не бросает исключений */ }
```

## Типичные ошибки
- Перехват по значению (`catch (std::exception e)`) — срезка
- Порядок `catch`: сначала конкретные, потом общие
- Исключения для обычного управления потоком выполнения — медленно и неудобно
- Выброс исключения из деструктора

## Практика
1. Функция `parseInt(string)` с обработкой ошибок.
2. Класс `Stack` с исключением при `pop()` из пустого стека.
3. Программа считывает число из файла и обрабатывает все возможные ошибки.

## Проверь себя
1. Как перехватить любое исключение?
2. Почему `catch` лучше делать по ссылке?
3. Что такое RAII?

---
[← Урок 22](lesson-22.md) · [Программа курса](README.md) · [Урок 24 →](lesson-24.md)
