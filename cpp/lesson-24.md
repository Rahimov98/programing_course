# C++ · Урок 24. Итоговый проект: учёт студентов

## Цель
Консольное приложение с использованием классов, STL, файлов и исключений.

## Требования
- Добавление, удаление и поиск студентов
- Вывод списка, сортировка по среднему баллу
- Сохранение и загрузка из файла `students.txt`
- Проверка корректности ввода

## Структура проекта
```
student-manager/
├── main.cpp
├── Student.h
├── StudentManager.h
├── StudentManager.cpp
└── students.txt
```

## Student.h
```cpp
#pragma once
#include <string>

struct Student {
    int id;
    std::string name;
    double gpa;
};
```

## StudentManager.h
```cpp
#pragma once
#include "Student.h"
#include <vector>
#include <string>

class StudentManager {
    std::vector<Student> students;
    int nextId = 1;
public:
    void add(const std::string& name, double gpa);
    bool remove(int id);
    const Student* find(int id) const;
    void printAll() const;
    void sortByGpa();
    void save(const std::string& path) const;
    void load(const std::string& path);
};
```

## StudentManager.cpp
```cpp
#include "StudentManager.h"
#include <algorithm>
#include <fstream>
#include <iomanip>
#include <iostream>
#include <stdexcept>

void StudentManager::add(const std::string& name, double gpa) {
    if (name.empty()) throw std::invalid_argument("Имя не может быть пустым");
    if (gpa < 0 || gpa > 5) throw std::invalid_argument("Балл должен быть от 0 до 5");
    students.push_back({nextId++, name, gpa});
}

bool StudentManager::remove(int id) {
    auto it = std::remove_if(students.begin(), students.end(),
                             [id](const Student& s) { return s.id == id; });
    if (it == students.end()) return false;
    students.erase(it, students.end());
    return true;
}

const Student* StudentManager::find(int id) const {
    for (const auto& s : students)
        if (s.id == id) return &s;
    return nullptr;
}

void StudentManager::printAll() const {
    if (students.empty()) { std::cout << "Список пуст\n"; return; }
    for (const auto& s : students)
        std::cout << std::setw(3) << s.id << " | " << std::setw(15) << std::left
                  << s.name << std::right << " | " << std::fixed
                  << std::setprecision(2) << s.gpa << "\n";
}

void StudentManager::sortByGpa() {
    std::sort(students.begin(), students.end(),
              [](const Student& a, const Student& b) { return a.gpa > b.gpa; });
}

void StudentManager::save(const std::string& path) const {
    std::ofstream out(path);
    if (!out) throw std::runtime_error("Не удалось открыть файл для записи");
    for (const auto& s : students) out << s.id << ';' << s.name << ';' << s.gpa << '\n';
}

void StudentManager::load(const std::string& path) {
    std::ifstream in(path);
    if (!in) return;                       // файла ещё нет — это нормально
    students.clear();
    std::string line;
    while (std::getline(in, line)) {
        auto p1 = line.find(';');
        auto p2 = line.rfind(';');
        if (p1 == std::string::npos || p1 == p2) continue;
        Student s{std::stoi(line.substr(0, p1)),
                  line.substr(p1 + 1, p2 - p1 - 1),
                  std::stod(line.substr(p2 + 1))};
        students.push_back(s);
        nextId = std::max(nextId, s.id + 1);
    }
}
```

## main.cpp
```cpp
#include "StudentManager.h"
#include <iostream>
#include <limits>

int main() {
    StudentManager mgr;
    mgr.load("students.txt");

    int choice = -1;
    while (choice != 0) {
        std::cout << "\n1. Список  2. Добавить  3. Удалить  4. Сортировать  0. Выход\n> ";
        if (!(std::cin >> choice)) {
            std::cin.clear();
            std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n');
            continue;
        }
        try {
            if (choice == 1) mgr.printAll();
            else if (choice == 2) {
                std::string name; double gpa;
                std::cout << "Имя: ";  std::cin >> name;
                std::cout << "Балл: "; std::cin >> gpa;
                mgr.add(name, gpa);
            } else if (choice == 3) {
                int id; std::cout << "ID: "; std::cin >> id;
                if (!mgr.remove(id)) std::cout << "Не найден\n";
            } else if (choice == 4) mgr.sortByGpa();
        } catch (const std::exception& e) {
            std::cout << "Ошибка: " << e.what() << "\n";
        }
    }
    mgr.save("students.txt");
}
```

## Компиляция
```bash
g++ -std=c++17 main.cpp StudentManager.cpp -o app
./app
```

## Задания на усложнение
1. Редактирование данных студента.
2. Поиск по части имени.
3. Замена `vector` на `map<int, Student>`.
4. Класс `Group`, содержащий студентов.
5. CMake-файл для сборки проекта и загрузка на GitHub.

## Поздравляем!
Вы прошли курс C++. Следующие шаги: CMake, потоки (`std::thread`), сети (Boost.Asio), Qt для GUI, алгоритмы и структуры данных.

---
[← Урок 23](lesson-23.md) · [Программа курса](README.md)
