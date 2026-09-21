# Python · Урок 21. SQLite в Python

## Цели урока
- Подключаться к базе SQLite
- Выполнять запросы и безопасно передавать параметры

## Теория
SQLite — встроенная база в одном файле, не требует сервера. Модуль `sqlite3` входит в стандартную библиотеку.

```python
import sqlite3

conn = sqlite3.connect("app.db")
cur = conn.cursor()

cur.execute("""
    CREATE TABLE IF NOT EXISTS students (
        id INTEGER PRIMARY KEY AUTOINCREMENT,
        name TEXT NOT NULL,
        age INTEGER
    )
""")

cur.execute("INSERT INTO students (name, age) VALUES (?, ?)", ("Алишер", 21))
cur.executemany("INSERT INTO students (name, age) VALUES (?, ?)",
                [("Мадина", 19), ("Фируз", 22)])
conn.commit()

cur.execute("SELECT id, name, age FROM students WHERE age > ?", (20,))
for row in cur.fetchall():
    print(row)

cur.execute("UPDATE students SET age = ? WHERE id = ?", (23, 1))
cur.execute("DELETE FROM students WHERE id = ?", (2,))
conn.commit()
conn.close()
```

## Удобно: with и Row
```python
with sqlite3.connect("app.db") as conn:
    conn.row_factory = sqlite3.Row
    for r in conn.execute("SELECT * FROM students"):
        print(r["name"], r["age"])
```

## Безопасность
**Никогда** не собирайте запрос через f-строку с данными пользователя — это SQL-инъекция. Только параметры `?`.

## Типичные ошибки
- Забыли `commit()` — изменения не сохранились
- Не закрыли соединение
- Данные подставляются в запрос через f-строку

## Практика
1. Создайте таблицу `books` и добавьте 5 записей.
2. Выведите книги, изданные после 2010 года.
3. Напишите консольное меню: добавить, показать, удалить.

## Проверь себя
1. Зачем нужен `commit()`?
2. Что такое SQL-инъекция и как от неё защититься?
3. Чем `fetchone` отличается от `fetchall`?

---
[← Урок 20](lesson-20.md) · [Программа курса](README.md) · [Урок 22 →](lesson-22.md)
