# SQL · Урок 6. ORDER BY и LIMIT

## Цели урока
- Сортировать результаты
- Ограничивать количество строк
- Делать постраничный вывод

## Теория

**Сортировка**
```sql
SELECT * FROM students ORDER BY age;           -- по возрастанию (ASC)
SELECT * FROM students ORDER BY age DESC;      -- по убыванию
SELECT * FROM students ORDER BY city, age DESC; -- сначала город, потом возраст
```

**LIMIT**
```sql
SELECT * FROM students ORDER BY age DESC LIMIT 3;  -- топ-3 старших
```

**OFFSET (пропуск строк)**
```sql
-- страница 2, по 5 записей
SELECT * FROM students ORDER BY id LIMIT 5 OFFSET 5;
-- или в MySQL: LIMIT 5, 5  (offset, count)
```

**NULL в сортировке**
В SQLite NULL идут первыми при ASC. Можно явно:
```sql
ORDER BY age ASC NULLS LAST;   -- PostgreSQL
```

## Типичные ошибки
- `ORDER BY` после `LIMIT` — порядок важен: WHERE → ORDER BY → LIMIT
- Забыли `DESC`/`ASC` и удивились порядку
- Большой `OFFSET` на огромных таблицах медленный

## Практика
1. Выведите студентов по возрасту (от старших к младшим).
2. Покажите 2 самые дорогие книги.
3. Сделайте «страницу 2» списка студентов (по 3 на страницу).

## Проверь себя
1. Что делает `ORDER BY ... DESC`?
2. Чем `LIMIT 5 OFFSET 10` отличается от `LIMIT 10`?
3. Можно ли сортировать по нескольким столбцам?

---
[← Урок 5](lesson-05.md) · [Программа курса](README.md) · [Урок 7 →](lesson-07.md)
