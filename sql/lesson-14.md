# SQL · Урок 14. Подзапросы

## Цели урока
- Писать подзапросы в WHERE, FROM, SELECT
- Использовать IN, EXISTS, сравнение с агрегатом
- Понимать коррелированные подзапросы

## Теория

**Подзапрос в WHERE**
```sql
-- студенты старше среднего возраста
SELECT name, age FROM students
WHERE age > (SELECT AVG(age) FROM students);

-- книги авторов из списка
SELECT title FROM books
WHERE author_id IN (SELECT id FROM authors WHERE name LIKE 'Т%');
```

**EXISTS**
```sql
SELECT name FROM authors a
WHERE EXISTS (
    SELECT 1 FROM books b WHERE b.author_id = a.id
);
```

**Подзапрос в FROM (производная таблица)**
```sql
SELECT city, avg_age
FROM (
    SELECT city, AVG(age) AS avg_age
    FROM students
    GROUP BY city
) AS city_stats
WHERE avg_age > 20;
```

**Подзапрос в SELECT**
```sql
SELECT name,
    (SELECT COUNT(*) FROM books b WHERE b.author_id = a.id) AS book_count
FROM authors a;
```

**Коррелированный** — зависит от внешней строки (как выше с book_count).

## Типичные ошибки
- Подзапрос возвращает несколько строк при сравнении с `=`
- Забыли скобки
- Слишком глубокая вложенность вместо JOIN

## Практика
1. Найдите студентов с возрастом выше среднего.
2. Выведите авторов, у которых есть хотя бы одна книга (EXISTS).
3. Для каждого автора покажите количество книг (подзапрос в SELECT).

## Проверь себя
1. Когда удобнее подзапрос, а когда JOIN?
2. Чем IN отличается от EXISTS?
3. Что такое коррелированный подзапрос?

---
[← Урок 13](lesson-13.md) · [Программа курса](README.md) · [Урок 15 →](lesson-15.md)
