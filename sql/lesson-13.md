# SQL · Урок 13. LEFT и RIGHT JOIN

## Цели урока
- Использовать LEFT JOIN для «всех из левой + совпадения»
- Понимать RIGHT JOIN и FULL OUTER JOIN
- Находить строки без пары

## Теория

**LEFT JOIN** — все строки левой таблицы + совпадения справа (иначе NULL).

```sql
SELECT a.name, b.title
FROM authors a
LEFT JOIN books b ON a.id = b.author_id;
-- авторы без книг тоже будут, title = NULL
```

**Найти авторов без книг**
```sql
SELECT a.name
FROM authors a
LEFT JOIN books b ON a.id = b.author_id
WHERE b.id IS NULL;
```

**RIGHT JOIN** — зеркало LEFT (все из правой).
```sql
SELECT a.name, b.title
FROM authors a
RIGHT JOIN books b ON a.id = b.author_id;
```
В SQLite RIGHT JOIN нет (эмулируют сменой порядка таблиц + LEFT).

**FULL OUTER JOIN** — все из обеих (PostgreSQL, не SQLite).
```sql
SELECT ...
FROM a FULL OUTER JOIN b ON ...
```

**Сравнение**
| Тип | Левая без пары | Правая без пары |
|-----|----------------|-----------------|
| INNER | нет | нет |
| LEFT | да (NULL) | нет |
| RIGHT | нет | да (NULL) |
| FULL | да | да |

## Типичные ошибки
- `WHERE b.id = NULL` вместо `IS NULL`
- Ожидание, что LEFT вернёт только совпадения

## Практика
1. Выведите всех авторов и их книги (включая авторов без книг).
2. Найдите авторов, у которых нет ни одной книги.
3. Выведите все курсы и студентов на них (курсы без студентов тоже).

## Проверь себя
1. Чем LEFT JOIN отличается от INNER JOIN?
2. Как найти строки без пары?
3. Есть ли RIGHT JOIN в SQLite?

---
[← Урок 12](lesson-12.md) · [Программа курса](README.md) · [Урок 14 →](lesson-14.md)
