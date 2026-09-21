# C++ · Урок 22. Работа с файлами

## Цели урока
- Читать и записывать текстовые файлы
- Проверять успешность операций

## Запись
```cpp
#include <fstream>
#include <iostream>
#include <string>

int main() {
    std::ofstream out("notes.txt");
    if (!out) {
        std::cerr << "Не удалось открыть файл\n";
        return 1;
    }
    out << "Первая строка\n";
    out << "Число: " << 42 << "\n";
}                               // файл закрывается автоматически
```
Добавление в конец: `std::ofstream out("notes.txt", std::ios::app);`

## Чтение построчно
```cpp
std::ifstream in("notes.txt");
std::string line;
while (std::getline(in, line)) {
    std::cout << line << "\n";
}
```

## Чтение чисел
```cpp
std::ifstream in("numbers.txt");
int x, sum = 0;
while (in >> x) sum += x;
std::cout << "Сумма: " << sum << "\n";
```

## Чтение всего файла
```cpp
#include <sstream>
std::ifstream in("notes.txt");
std::stringstream ss;
ss << in.rdbuf();
std::string text = ss.str();
```

## Сохранение и загрузка структур
```cpp
struct Student { std::string name; int age; };

void save(const std::vector<Student>& v, const std::string& path) {
    std::ofstream out(path);
    for (const auto& s : v) out << s.name << ";" << s.age << "\n";
}

std::vector<Student> load(const std::string& path) {
    std::vector<Student> v;
    std::ifstream in(path);
    std::string line;
    while (std::getline(in, line)) {
        auto pos = line.find(';');
        if (pos == std::string::npos) continue;
        v.push_back({line.substr(0, pos), std::stoi(line.substr(pos + 1))});
    }
    return v;
}
```

## Файловая система (C++17)
```cpp
#include <filesystem>
namespace fs = std::filesystem;
fs::exists("notes.txt");
fs::file_size("notes.txt");
fs::create_directory("data");
```

## Бинарные файлы
```cpp
std::ofstream out("data.bin", std::ios::binary);
int n = 123;
out.write(reinterpret_cast<const char*>(&n), sizeof(n));
```

## Типичные ошибки
- Не проверили `if (!in)` — программа работает с несуществующим файлом
- Относительный путь считается от рабочей папки, а не от места `.cpp`
- Смешение `>>` и `getline` (остаётся `\n`)

## Практика
1. Запишите в файл 10 случайных чисел и прочитайте их обратно.
2. Посчитайте строки и слова в текстовом файле.
3. Программа «записная книжка» с сохранением в файл.

## Проверь себя
1. Чем `ofstream` отличается от `ifstream`?
2. Как открыть файл на добавление?
3. Как считать файл построчно?

---
[← Урок 21](lesson-21.md) · [Программа курса](README.md) · [Урок 23 →](lesson-23.md)
