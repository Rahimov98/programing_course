# SQL · Урок 4. SELECT: выборка данных

## Цели урока
- Выбирать все или отдельные столбцы
- Давать столбцам псевдонимы
- Использовать выражения в SELECT

## Теория

**Все столбцы**
```sql
SELECT * FROM students;
```

**Отдельные столбцы**
```sql
SELECT name, age FROM students;
```

**Псевдонимы (AS)**
```sql
SELECT name AS student_name, age AS years
FROM students;

SELECT name || ' из ' || city AS info FROM students;  -- SQLite
-- MySQL: CONCAT(name, ' из ', city)
```

**Выражения и константы**
```sql
SELECT name, age, age + 1 AS next_year FROM students;
SELECT 'Студент' AS role, name FROM students;
```

**Уникальные значения**
```sql
SELECT DISTINCT city FROM students;
```

**Количество строк**
```sql
SELECT COUNT(*) FROM students;
```

## Типичные ошибки
- `SELECT name age` без запятой
- Псевдоним с пробелом без кавычек: `AS student name` → ошибка
- Забыли `FROM`

## Практика
1. Выберите только `title` и `author` из таблицы books.
2. Выведите имя и возраст с псевдонимами на русском.
3. Покажите уникальные города студентов.

## Проверь себя
1. Что делает `DISTINCT`?
2. Зачем нужен `AS`?
3. Чем `SELECT *` отличается от перечисления столбцов?

---
[← Урок 3](lesson-03.md) · [Программа курса](README.md) · [Урок 5 →](lesson-05.md)
