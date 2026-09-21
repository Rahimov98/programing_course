# C++ · Урок 20. Шаблоны (templates)

## Цели урока
- Писать код, независимый от типа данных

## Шаблон функции
```cpp
#include <iostream>

template <typename T>
T maxOf(T a, T b) {
    return (a > b) ? a : b;
}

int main() {
    std::cout << maxOf(3, 7) << "\n";          // T = int
    std::cout << maxOf(2.5, 1.5) << "\n";      // T = double
    std::cout << maxOf<std::string>("a", "b") << "\n";
}
```
Компилятор создаёт версию функции для каждого использованного типа.

## Несколько параметров
```cpp
template <typename T, typename U>
auto add(T a, U b) { return a + b; }
```

## Шаблон класса
```cpp
template <typename T>
class Stack {
    std::vector<T> items;
public:
    void push(const T& v) { items.push_back(v); }
    T pop() {
        if (items.empty()) throw std::runtime_error("Стек пуст");
        T v = items.back();
        items.pop_back();
        return v;
    }
    bool empty() const { return items.empty(); }
    size_t size() const { return items.size(); }
};

Stack<int> s;
s.push(1); s.push(2);
std::cout << s.pop();     // 2

Stack<std::string> names;
```

## Шаблон с нетиповым параметром
```cpp
template <typename T, size_t N>
class FixedArray {
    T data[N];
public:
    T& operator[](size_t i) { return data[i]; }
    constexpr size_t size() const { return N; }
};
FixedArray<int, 5> arr;
```

## Ограничения (C++20 concepts)
```cpp
#include <concepts>
template <std::integral T>
T twice(T x) { return x * 2; }
```

## Особенность
Шаблоны обычно полностью размещают в заголовочных файлах (`.h`/`.hpp`), потому что компилятору нужен весь код в момент создания экземпляра.

## Типичные ошибки
- Тип не поддерживает операцию (`>`, `+`) — длинное сообщение об ошибке при компиляции
- Определение методов шаблона класса в `.cpp` — ошибки линковки
- Разные типы аргументов при одном `T` (`maxOf(3, 2.5)`)

## Практика
1. Шаблон функции `swapValues(T&, T&)`.
2. Шаблон класса `Queue<T>` на основе `std::deque`.
3. Шаблон `Pair<T, U>` с методом вывода.

## Проверь себя
1. Что такое шаблон?
2. Почему шаблоны размещают в заголовочных файлах?
3. Чем `template <typename T>` отличается от `template <class T>`?

---
[← Урок 19](lesson-19.md) · [Программа курса](README.md) · [Урок 21 →](lesson-21.md)
