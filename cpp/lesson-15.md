# C++ · Урок 15. Классы и объекты

## Цели урока
- Описывать классы с полями и методами
- Использовать спецификаторы доступа

## Класс
```cpp
#include <iostream>
#include <string>

class Account {
private:                       // недоступно снаружи
    std::string owner;
    double balance;

public:                        // доступно всем
    Account(const std::string& owner, double balance)
        : owner(owner), balance(balance) {}

    void deposit(double amount) {
        if (amount > 0) balance += amount;
    }

    bool withdraw(double amount) {
        if (amount <= 0 || amount > balance) return false;
        balance -= amount;
        return true;
    }

    double getBalance() const { return balance; }
    const std::string& getOwner() const { return owner; }

    void print() const {
        std::cout << owner << ": " << balance << "\n";
    }
};

int main() {
    Account acc("Алишер", 1000);
    acc.deposit(500);
    if (!acc.withdraw(5000)) std::cout << "Недостаточно средств\n";
    acc.print();
}
```

## Ключевые идеи
- **Инкапсуляция:** данные `private`, доступ через методы (get/set) с проверками
- **`const` метод** (`getBalance() const`) обещает не менять объект
- **Список инициализации** `: owner(owner), balance(balance)` — предпочтительный способ инициализации полей
- **`this`** — указатель на текущий объект

## Разделение на файлы
`Account.h`:
```cpp
#pragma once
#include <string>

class Account {
    std::string owner;
    double balance;
public:
    Account(const std::string& owner, double balance);
    void deposit(double amount);
    double getBalance() const;
};
```
`Account.cpp`:
```cpp
#include "Account.h"

Account::Account(const std::string& o, double b) : owner(o), balance(b) {}
void Account::deposit(double amount) { if (amount > 0) balance += amount; }
double Account::getBalance() const { return balance; }
```

## Типичные ошибки
- Обращение к `private` полю извне
- Забыли `;` после `}` класса
- Метод, не меняющий объект, не помечен `const` — его нельзя вызвать для `const` объекта

## Практика
1. Класс `Rectangle` с методами `area()` и `perimeter()`.
2. Класс `Book` с проверкой года издания.
3. Класс `Counter` с методами `increment()`, `reset()`.

## Проверь себя
1. Зачем нужны `private` поля?
2. Что означает `const` после метода?
3. Что делает `this`?

---
[← Урок 14](lesson-14.md) · [Программа курса](README.md) · [Урок 16 →](lesson-16.md)
