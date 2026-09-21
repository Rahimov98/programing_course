# SQL · Урок 7. Агрегатные функции

## Цели урока
- Считать количество, сумму, среднее, минимум и максимум
- Понимать, как агрегаты работают с NULL

## Теория

**Основные функции**
```sql
SELECT COUNT(*) FROM students;           -- все строки
SELECT COUNT(city) FROM students;        -- не-NULL значения city
SELECT COUNT(DISTINCT city) FROM students;

SELECT SUM(age) FROM students;
SELECT AVG(age) FROM students;
SELECT MIN(age), MAX(age) FROM students;
```

**С алиасами**
```sql
SELECT
    COUNT(*) AS total,
    AVG(age) AS avg_age,
    MIN(age) AS youngest,
    MAX(age) AS oldest
FROM students;
```

**С WHERE**
```sql
SELECT AVG(age) FROM students WHERE city = 'Душанбе';
SELECT COUNT(*) FROM books WHERE year >= 2020;
```

**NULL и агрегаты**
- `COUNT(*)` считает все строки
- `COUNT(column)` игнорирует NULL
- `SUM` / `AVG` игнорируют NULL
- `MIN` / `MAX` игнорируют NULL

## Типичные ошибки
- `SELECT name, COUNT(*) FROM students` без GROUP BY — ошибка
- Ожидание, что `AVG` учитывает NULL как 0

## Практика
1. Посчитайте количество студентов.
2. Найдите средний, минимальный и максимальный возраст.
3. Сколько уникальных городов?

## Проверь себя
1. Чем `COUNT(*)` отличается от `COUNT(column)`?
2. Что вернёт `SUM` по столбцу с NULL?
3. Можно ли использовать агрегаты без GROUP BY?

---
[← Урок 6](lesson-06.md) · [Программа курса](README.md) · [Урок 8 →](lesson-08.md)
