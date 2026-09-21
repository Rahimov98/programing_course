# SQL · Урок 11. Связи между таблицами

## Цели урока
- Понять типы связей: 1:1, 1:N, M:N
- Правильно проектировать внешние ключи
- Создать связанные таблицы

## Теория

**Один ко многим (1:N)** — самая частая
Один автор → много книг.
```sql
CREATE TABLE authors (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL
);

CREATE TABLE books (
    id INTEGER PRIMARY KEY,
    title TEXT NOT NULL,
    author_id INTEGER NOT NULL,
    FOREIGN KEY (author_id) REFERENCES authors(id)
);
```

**Многие ко многим (M:N)**
Студенты ↔ Курсы через промежуточную таблицу.
```sql
CREATE TABLE students (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL
);

CREATE TABLE courses (
    id INTEGER PRIMARY KEY,
    title TEXT NOT NULL
);

CREATE TABLE enrollments (
    student_id INTEGER,
    course_id INTEGER,
    enrolled_at TEXT DEFAULT CURRENT_TIMESTAMP,
    PRIMARY KEY (student_id, course_id),
    FOREIGN KEY (student_id) REFERENCES students(id),
    FOREIGN KEY (course_id) REFERENCES courses(id)
);
```

**Один к одному (1:1)**
Редко: профиль пользователя, паспорт.
Внешний ключ с UNIQUE на стороне «зависимой» таблицы.

**Каскадные действия**
```sql
FOREIGN KEY (author_id) REFERENCES authors(id)
    ON DELETE CASCADE
    ON UPDATE CASCADE
```
- `CASCADE` — удалить/обновить связанные
- `SET NULL` — обнулить
- `RESTRICT` — запретить (по умолчанию)

## Типичные ошибки
- Хранить списки id в одном поле через запятую
- Забыть промежуточную таблицу для M:N
- Циклические зависимости без нужды

## Практика
1. Создайте authors и books (1:N).
2. Создайте students, courses, enrollments (M:N).
3. Добавьте данные: 2 автора, 3 книги, 2 студента, записи на курсы.

## Проверь себя
1. Когда нужна промежуточная таблица?
2. Что делает ON DELETE CASCADE?
3. Чем 1:N отличается от M:N?

---
[← Урок 10](lesson-10.md) · [Программа курса](README.md) · [Урок 12 →](lesson-12.md)
