# SQL · Урок 12. INNER JOIN

## Цели урока
- Объединять таблицы через INNER JOIN
- Понимать, когда строки отбрасываются
- Использовать псевдонимы таблиц

## Теория

**INNER JOIN** возвращает только строки, у которых есть совпадение в обеих таблицах.

```sql
SELECT books.title, authors.name AS author
FROM books
INNER JOIN authors ON books.author_id = authors.id;
```

**Кратко**
```sql
SELECT b.title, a.name
FROM books b
JOIN authors a ON b.author_id = a.id;   -- INNER можно опустить
```

**Несколько JOIN**
```sql
SELECT s.name, c.title
FROM enrollments e
JOIN students s ON e.student_id = s.id
JOIN courses c ON e.course_id = c.id;
```

**С условием**
```sql
SELECT b.title, a.name
FROM books b
JOIN authors a ON b.author_id = a.id
WHERE a.name = 'Толстой';
```

**Без JOIN (старый стиль — не рекомендуется)**
```sql
SELECT b.title, a.name
FROM books b, authors a
WHERE b.author_id = a.id;
```

## Типичные ошибки
- Забыли условие ON → декартово произведение
- Путаница в порядке таблиц (для INNER не критично)
- Одинаковые имена столбцов без уточнения таблицы

## Практика
1. Выведите название книги и имя автора.
2. Выведите студентов и названия курсов, на которые они записаны.
3. Добавьте WHERE: только книги определённого автора.

## Проверь себя
1. Что возвращает INNER JOIN, если совпадения нет?
2. Зачем псевдонимы таблиц (b, a)?
3. Чем JOIN отличается от WHERE с двумя таблицами?

---
[← Урок 11](lesson-11.md) · [Программа курса](README.md) · [Урок 13 →](lesson-13.md)
