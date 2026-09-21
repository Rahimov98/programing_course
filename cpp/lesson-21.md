# C++ · Урок 21. STL: контейнеры и алгоритмы

## Цели урока
- Использовать стандартные контейнеры и алгоритмы

## Контейнеры
| Контейнер | Особенность |
|---|---|
| `vector` | динамический массив, быстрый доступ по индексу |
| `array` | массив фиксированного размера |
| `deque` | двусторонняя очередь |
| `list` | двусвязный список |
| `map` | ключ → значение, отсортирован по ключу |
| `unordered_map` | хеш-таблица, быстрее в среднем |
| `set` / `unordered_set` | уникальные элементы |
| `stack`, `queue`, `priority_queue` | адаптеры |

## map
```cpp
#include <map>
#include <string>
#include <iostream>

std::map<std::string, int> ages;
ages["Алишер"] = 21;
ages["Мадина"] = 19;
ages.insert({"Фируз", 22});

for (const auto& [name, age] : ages)
    std::cout << name << ": " << age << "\n";

if (ages.count("Алишер")) std::cout << "Есть\n";
auto it = ages.find("Фируз");
if (it != ages.end()) std::cout << it->second;
ages.erase("Мадина");
```

## Подсчёт слов
```cpp
std::unordered_map<std::string, int> freq;
for (const auto& w : words) freq[w]++;
```

## set
```cpp
#include <set>
std::set<int> s = {3, 1, 2, 3};    // {1, 2, 3}
s.insert(10);
s.contains(2);                     // C++20; ранее: s.count(2)
```

## stack, queue
```cpp
#include <stack>
#include <queue>
std::stack<int> st; st.push(1); st.top(); st.pop();
std::queue<int> q;  q.push(1); q.front(); q.pop();
std::priority_queue<int> pq; pq.push(5); pq.top();
```

## Алгоритмы
```cpp
#include <algorithm>
#include <numeric>

std::vector<int> v = {5, 2, 8, 1};
std::sort(v.begin(), v.end());
std::reverse(v.begin(), v.end());
auto it = std::find(v.begin(), v.end(), 8);
int cnt = std::count_if(v.begin(), v.end(), [](int x) { return x > 2; });
int sum = std::accumulate(v.begin(), v.end(), 0);
bool any = std::any_of(v.begin(), v.end(), [](int x) { return x < 0; });
std::binary_search(v.begin(), v.end(), 5);      // на отсортированных данных

v.erase(std::remove_if(v.begin(), v.end(),
        [](int x) { return x % 2 == 0; }), v.end());       // удалить чётные
```

## Лямбда-выражения
```cpp
auto sq = [](int x) { return x * x; };
int k = 10;
auto addK = [k](int x) { return x + k; };     // захват по значению
auto inc  = [&k]() { k++; };                  // захват по ссылке
```

## Типичные ошибки
- `map[key]` создаёт элемент, если ключа нет
- Бинарный поиск на неотсортированных данных
- Недействительные итераторы после изменения контейнера

## Практика
1. Подсчитайте частоту слов в тексте и выведите топ-3.
2. Уберите дубли из вектора через `set`.
3. Отсортируйте вектор строк по длине лямбдой.

## Проверь себя
1. Чем `map` отличается от `unordered_map`?
2. Что делает `std::sort` и что нужно ему передать?
3. Как захватить переменную в лямбду по ссылке?

---
[← Урок 20](lesson-20.md) · [Программа курса](README.md) · [Урок 22 →](lesson-22.md)
