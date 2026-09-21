# SQL · Урок 3. INSERT: добавление данных

## Цели урока
- Добавлять одну и несколько строк
- Указывать столбцы явно
- Использовать `DEFAULT` и `NULL`

## Теория

**Одна строка**
```sql
INSERT INTO students (name, city, age)
VALUES ('Алишер', 'Душанбе', 21);
```

**Несколько строк**
```sql
INSERT INTO students (name, city, age) VALUES
    ('Мадина', 'Худжанд', 19),
    ('Руслан', 'Душанбе', 22),
    ('Зарина', 'Куляб', 20);
```

**Без списка столбцов** (нужно указать все по порядку)
```sql
INSERT INTO students VALUES (NULL, 'Саид', 'Хорог', 18);
-- NULL для AUTOINCREMENT / PRIMARY KEY
```

**Вставка с DEFAULT**
```sql
INSERT INTO products (name, price) VALUES ('Чай', 15.50);
-- in_stock и created_at возьмутся из DEFAULT
```

**Вставка из другой таблицы**
```sql
INSERT INTO archive (name, city)
SELECT name, city FROM students WHERE age < 20;
```

**Получение id последней вставки (SQLite)**
```sql
SELECT last_insert_rowid();
```

## Типичные ошибки
- Количество значений ≠ количеству столбцов
- Текст без кавычек: `Алишер` вместо `'Алишер'`
- Вставка в `NOT NULL` столбец значения `NULL`

## Практика
1. Создайте таблицу `books` (id, title, author, year, pages).
2. Добавьте 5 книг одним запросом.
3. Добавьте книгу, указав только title и author (остальное — DEFAULT или NULL).

## Проверь себя
1. Зачем явно перечислять столбцы в `INSERT`?
2. Как вставить несколько строк за раз?
3. Что будет, если вставить `NULL` в `NOT NULL` столбец?

---
[← Урок 2](lesson-02.md) · [Программа курса](README.md) · [Урок 4 →](lesson-04.md)
