# Python · Урок 24. Итоговый проект: менеджер задач

## Цель
Собрать полноценное консольное приложение, используя всё изученное: функции, классы, файлы, JSON, исключения.

## Требования
- Добавление, просмотр, отметка выполненной и удаление задач
- Хранение в `tasks.json`
- Защита от неверного ввода
- Код разбит на функции/классы

## Структура проекта
```
task-manager/
├── main.py
├── storage.py
└── tasks.json
```

## storage.py
```python
import json
from pathlib import Path

FILE = Path("tasks.json")

def load():
    if not FILE.exists():
        return []
    with open(FILE, encoding="utf-8") as f:
        return json.load(f)

def save(tasks):
    with open(FILE, "w", encoding="utf-8") as f:
        json.dump(tasks, f, ensure_ascii=False, indent=2)
```

## main.py
```python
import storage

def show(tasks):
    if not tasks:
        print("Список пуст")
    for i, t in enumerate(tasks, 1):
        mark = "✔" if t["done"] else " "
        print(f"{i}. [{mark}] {t['title']}")

def ask_number(prompt, limit):
    while True:
        try:
            n = int(input(prompt))
            if 1 <= n <= limit:
                return n
        except ValueError:
            pass
        print("Введите корректный номер")

def main():
    tasks = storage.load()
    while True:
        print("\n1. Показать  2. Добавить  3. Выполнить  4. Удалить  0. Выход")
        choice = input("Выбор: ")
        if choice == "1":
            show(tasks)
        elif choice == "2":
            title = input("Название: ").strip()
            if title:
                tasks.append({"title": title, "done": False})
        elif choice == "3" and tasks:
            show(tasks)
            tasks[ask_number("Номер: ", len(tasks)) - 1]["done"] = True
        elif choice == "4" and tasks:
            show(tasks)
            tasks.pop(ask_number("Номер: ", len(tasks)) - 1)
        elif choice == "0":
            break
        else:
            print("Неизвестная команда")
        storage.save(tasks)

if __name__ == "__main__":
    main()
```

## Задания на усложнение
1. Добавьте дату создания и срок выполнения.
2. Фильтр: показывать только невыполненные.
3. Перепишите хранение на SQLite (урок 21).
4. Сделайте графический интерфейс на Tkinter (урок 23).
5. Оформите `README.md` проекта и выложите на GitHub.

## Поздравляем!
Вы прошли курс Python. Следующие шаги: Flask/Django, анализ данных (pandas), автоматизация, телеграм-боты.

---
[← Урок 23](lesson-23.md) · [Программа курса](README.md)
