# SQL · Урок 5. WHERE: фильтрация

## Цели урока
- Фильтровать строки по условиям
- Использовать операторы сравнения и логические
- Работать с `NULL`, `IN`, `BETWEEN`, `LIKE`

## Теория

**Базовые условия**
```sql
SELECT * FROM students WHERE age >= 20;
SELECT * FROM students WHERE city = 'Душанбе';
SELECT * FROM students WHERE age != 21;   -- или <>
```

**Логические операторы**
```sql
SELECT * FROM students
WHERE age >= 18 AND city = 'Душанбе';

SELECT * FROM students
WHERE city = 'Душанбе' OR city = 'Худжанд';

SELECT * FROM students WHERE NOT age < 20;
```

**IN, BETWEEN, LIKE**
```sql
SELECT * FROM students WHERE city IN ('Душанбе', 'Худжанд', 'Куляб');
SELECT * FROM students WHERE age BETWEEN 18 AND 22;
SELECT * FROM students WHERE name LIKE 'А%';     -- начинается с А
SELECT * FROM students WHERE name LIKE '%на';    -- заканчивается на на
SELECT * FROM students WHERE name LIKE '%ли%';   -- содержит ли
```

**NULL**
```sql
SELECT * FROM students WHERE city IS NULL;
SELECT * FROM students WHERE city IS NOT NULL;
-- city = NULL не работает!
```

## Типичные ошибки
- `=` вместо `IS` для NULL
- `LIKE` без `%` ищет точное совпадение
- Строки без кавычек

## Практика
1. Найдите студентов старше 20 лет из Душанбе.
2. Выберите книги 2020–2024 годов.
3. Найдите имена, начинающиеся на «М».

## Проверь себя
1. Чем `AND` отличается от `OR`?
2. Почему `= NULL` не работает?
3. Что означает `%` в `LIKE`?

---
[← Урок 4](lesson-04.md) · [Программа курса](README.md) · [Урок 6 →](lesson-06.md)
