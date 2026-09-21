# SQL · Урок 18. Индексы

## Цели урока
- Понять, зачем нужны индексы
- Создавать и удалять индексы
- Знать, когда индекс помогает, а когда мешает

## Теория

**Индекс** — структура, ускоряющая поиск (как оглавление в книге).

```sql
CREATE INDEX idx_students_city ON students(city);
CREATE UNIQUE INDEX idx_users_email ON users(email);
CREATE INDEX idx_books_author_year ON books(author_id, year);  -- составной
```

**Удаление**
```sql
DROP INDEX idx_students_city;
```

**Когда индекс полезен**
- WHERE по столбцу
- JOIN по столбцу
- ORDER BY
- UNIQUE-ограничения (создают индекс автоматически)

**Когда индекс мешает**
- Частые INSERT/UPDATE/DELETE (индекс нужно обновлять)
- Маленькие таблицы
- Столбцы с малой селективностью (например, boolean)

**Просмотр**
```sql
-- SQLite
.indices students
EXPLAIN QUERY PLAN SELECT * FROM students WHERE city = 'Душанбе';
```

**PRIMARY KEY и UNIQUE** уже имеют индекс.

## Типичные ошибки
- Индекс на каждый столбец «на всякий случай»
- Забыли индекс на внешний ключ при больших JOIN
- Ожидание ускорения SELECT * без WHERE

## Практика
1. Создайте индекс по city в students.
2. Создайте уникальный индекс по email (если есть таблица users).
3. Выполните EXPLAIN QUERY PLAN для запроса с WHERE по city.

## Проверь себя
1. Зачем нужны индексы?
2. Почему много индексов замедляет запись?
3. Создаётся ли индекс автоматически для PRIMARY KEY?

---
[← Урок 17](lesson-17.md) · [Программа курса](README.md) · [Урок 19 →](lesson-19.md)
