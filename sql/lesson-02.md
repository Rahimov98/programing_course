# SQL · Урок 2. CREATE TABLE и типы данных

## Цели урока
- Создавать таблицы с разными типами столбцов
- Понимать основные типы данных
- Удалять и изменять таблицы

## Теория

**Основные типы (SQLite / общие)**
| Тип | Описание | Пример |
|-----|----------|--------|
| INTEGER | Целое число | 21, -5 |
| REAL | Дробное | 19.99 |
| TEXT | Строка | 'Алишер' |
| BLOB | Двоичные данные | файлы |
| NUMERIC | Числа / даты | '2024-01-15' |

В MySQL/PostgreSQL чаще встречаются: `INT`, `VARCHAR(n)`, `DECIMAL(10,2)`, `DATE`, `BOOLEAN`, `TIMESTAMP`.

**Создание таблицы**
```sql
CREATE TABLE products (
    id          INTEGER PRIMARY KEY,
    name        TEXT NOT NULL,
    price       REAL NOT NULL,
    in_stock    INTEGER DEFAULT 0,
    created_at  TEXT DEFAULT CURRENT_TIMESTAMP
);
```

**Ограничения при создании**
- `NOT NULL` — значение обязательно
- `DEFAULT` — значение по умолчанию
- `UNIQUE` — уникальность
- `PRIMARY KEY` — первичный ключ (уникален + NOT NULL)

**Изменение и удаление**
```sql
ALTER TABLE products ADD COLUMN category TEXT;
ALTER TABLE products RENAME TO goods;   -- SQLite 3.25+
DROP TABLE products;                    -- удаляет таблицу целиком
```

**Просмотр структуры**
```sql
-- SQLite
.schema products
PRAGMA table_info(products);

-- MySQL
DESCRIBE products;
SHOW CREATE TABLE products;
```

## Типичные ошибки
- Запятая после последнего столбца
- `INTEGER` написан как `INTIGER`
- Попытка `DROP` несуществующей таблицы без `IF EXISTS`

## Практика
1. Создайте таблицу `employees` (id, name, position, salary, hired_at).
2. Добавьте столбец `department` через `ALTER TABLE`.
3. Удалите таблицу и создайте заново с `NOT NULL` на name и salary.

## Проверь себя
1. Чем `TEXT` отличается от `VARCHAR`?
2. Зачем `DEFAULT`?
3. Что делает `DROP TABLE`?

---
[← Урок 1](lesson-01.md) · [Программа курса](README.md) · [Урок 3 →](lesson-03.md)
