# C++ · Урок 10. Векторы (std::vector)

## Цели урока
- Использовать динамические массивы

## Основы
`std::vector` — массив, который сам меняет размер.
```cpp
#include <vector>
#include <iostream>

int main() {
    std::vector<int> v = {5, 2, 9};
    v.push_back(7);              // добавить в конец
    v.pop_back();                // удалить последний
    std::cout << v.size() << " " << v[0] << " " << v.at(1) << "\n";
    v.insert(v.begin() + 1, 100);
    v.erase(v.begin());
    v.clear();
    bool e = v.empty();
}
```

## Создание
```cpp
std::vector<int> a;                 // пустой
std::vector<int> b(5);              // 5 нулей
std::vector<int> c(5, 7);           // пять семёрок
std::vector<std::string> names = {"Али", "Мадина"};
```

## Перебор
```cpp
for (int x : v) std::cout << x << " ";
for (auto& x : v) x *= 2;           // изменение элементов (по ссылке)
for (size_t i = 0; i < v.size(); i++) std::cout << v[i];
for (auto it = v.begin(); it != v.end(); ++it) std::cout << *it;
```

## Алгоритмы
```cpp
#include <algorithm>
#include <numeric>

std::sort(v.begin(), v.end());
std::sort(v.begin(), v.end(), std::greater<int>());   // по убыванию
std::reverse(v.begin(), v.end());
int mx = *std::max_element(v.begin(), v.end());
int sum = std::accumulate(v.begin(), v.end(), 0);
auto it = std::find(v.begin(), v.end(), 9);
```

## Двумерный вектор
```cpp
std::vector<std::vector<int>> matrix(3, std::vector<int>(4, 0));
matrix[1][2] = 5;
```

## Передача в функцию
```cpp
void print(const std::vector<int>& v) {      // по константной ссылке, без копирования
    for (int x : v) std::cout << x << " ";
}
```

## Типичные ошибки
- `v[10]` для вектора из 3 элементов — неопределённое поведение (`at()` бросает исключение)
- Изменение вектора (`push_back`) во время итерации по нему — итераторы становятся недействительными
- Передача вектора по значению — лишнее копирование

## Практика
1. Считайте `n` чисел в вектор, выведите отсортированными и их среднее.
2. Удалите из вектора все чётные числа (`erase` + `remove_if`).
3. Найдите наиболее частое число.

## Проверь себя
1. Чем `vector` лучше обычного массива?
2. Что делает `push_back`?
3. Почему вектор лучше передавать по `const&`?

---
[← Урок 9](lesson-09.md) · [Программа курса](README.md) · [Урок 11 →](lesson-11.md)
