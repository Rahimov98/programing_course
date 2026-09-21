# SQL · Урок 10. Ключи и ограничения

## Цели урока
- Понимать PRIMARY KEY, FOREIGN KEY, UNIQUE, CHECK
- Задавать ограничения при создании таблицы
- Видеть, как СУБД защищает данные

## Теория

**PRIMARY KEY**
```sql
CREATE TABLE users (
    id INTEGER PRIMARY KEY,          -- уникален, NOT NULL
    email TEXT NOT NULL UNIQUE
);
-- или составной:
-- PRIMARY KEY (order_id, product_id)
```

**FOREIGN KEY**
```sql
CREATE TABLE orders (
    id INTEGER PRIMARY KEY,
    user_id INTEGER NOT NULL,
    total REAL,
    FOREIGN KEY (user_id) REFERENCES users(id)
);
```

**CHECK**
```sql
CREATE TABLE products (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    price REAL CHECK (price > 0),
    stock INTEGER CHECK (stock >= 0)
);
```

**NOT NULL и DEFAULT**
```sql
status TEXT NOT NULL DEFAULT 'new'
```

**Включение FK в SQLite**
```sql
PRAGMA foreign_keys = ON;
```

**Что происходит при нарушении**
- Дубликат PRIMARY KEY / UNIQUE → ошибка
- FK на несуществующий id → ошибка
- CHECK не выполнен → ошибка

## Типичные ошибки
- Забыли включить foreign_keys в SQLite
- Ссылаться на столбец, который не UNIQUE/PK
- CHECK с синтаксической ошибкой

## Практика
1. Создайте `authors` (id, name) и `books` (id, title, author_id) со связью.
2. Добавьте CHECK: price > 0.
3. Попробуйте вставить книгу с несуществующим author_id — должна быть ошибка.

## Проверь себя
1. Чем PRIMARY KEY отличается от UNIQUE?
2. Зачем FOREIGN KEY?
3. Что делает CHECK?

---
[← Урок 9](lesson-09.md) · [Программа курса](README.md) · [Урок 11 →](lesson-11.md)
