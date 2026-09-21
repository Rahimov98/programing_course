# C++ · Урок 14. Структуры (struct)

## Цели урока
- Объединять данные разных типов в одну сущность

## Определение
```cpp
#include <iostream>
#include <string>
#include <vector>

struct Student {
    std::string name;
    int age;
    double gpa;
};

int main() {
    Student s1{"Алишер", 21, 4.5};
    Student s2;
    s2.name = "Мадина";
    s2.age = 19;
    s2.gpa = 4.8;

    std::cout << s1.name << ", " << s1.age << ", " << s1.gpa << "\n";
}
```

## Указатель на структуру
```cpp
Student* p = &s1;
std::cout << p->name << " " << (*p).age << "\n";   // -> для доступа через указатель
```

## Массивы структур
```cpp
std::vector<Student> group = {
    {"Алишер", 21, 4.5},
    {"Мадина", 19, 4.8},
    {"Фируз", 22, 3.9},
};

for (const auto& st : group)
    std::cout << st.name << " — " << st.gpa << "\n";

// сортировка по среднему баллу
std::sort(group.begin(), group.end(),
          [](const Student& a, const Student& b) { return a.gpa > b.gpa; });
```
Для `std::sort` нужен `#include <algorithm>`.

## Функции и структуры
```cpp
void print(const Student& s) {
    std::cout << s.name << " (" << s.age << ")\n";
}

Student createStudent(const std::string& name, int age) {
    return Student{name, age, 0.0};
}
```

## Вложенные структуры
```cpp
struct Address { std::string city; std::string street; };
struct Person  { std::string name; Address address; };

Person p{"Али", {"Душанбе", "Рудаки"}};
std::cout << p.address.city;
```

## struct и class
В C++ `struct` — то же, что `class`, но члены по умолчанию открытые (`public`). Структуры принято использовать для простых наборов данных.

## Типичные ошибки
- Забыли `;` после закрывающей `}` определения
- Использование `.` вместо `->` для указателя
- Сравнение структур через `==` без перегрузки оператора

## Практика
1. Структура `Book` (название, автор, год); выведите книги, изданные после 2000 года.
2. Найдите студента с наибольшим GPA.
3. Структура `Point` и функция расстояния между двумя точками.

## Проверь себя
1. Когда использовать `->`?
2. Чем `struct` отличается от `class`?
3. Как отсортировать вектор структур по полю?

---
[← Урок 13](lesson-13.md) · [Программа курса](README.md) · [Урок 15 →](lesson-15.md)
