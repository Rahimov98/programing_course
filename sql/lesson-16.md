# SQL · Урок 16. CASE и NULL

## Цели урока
- Использовать CASE для условной логики
- Обрабатывать NULL через COALESCE, IFNULL, NULLIF
- Писать читаемые выражения

## Теория

**CASE (простой)**
```sql
SELECT name, age,
    CASE
        WHEN age < 18 THEN 'несовершеннолетний'
        WHEN age < 30 THEN 'молодой'
        ELSE 'взрослый'
    END AS age_group
FROM students;
```

**CASE в агрегатах**
```sql
SELECT
    COUNT(CASE WHEN city = 'Душанбе' THEN 1 END) AS dushanbe,
    COUNT(CASE WHEN city = 'Худжанд' THEN 1 END) AS khujand
FROM students;
```

**COALESCE — первое не-NULL**
```sql
SELECT name, COALESCE(city, 'Неизвестно') AS city
FROM students;
```

**IFNULL (SQLite/MySQL)**
```sql
SELECT IFNULL(city, 'Неизвестно') FROM students;
```

**NULLIF**
```sql
SELECT NULLIF(age, 0);  -- если age = 0, вернёт NULL
```

**Сортировка NULL**
```sql
ORDER BY city NULLS LAST;   -- PostgreSQL
-- SQLite: ORDER BY city IS NULL, city
```

## Типичные ошибки
- Забыли END у CASE
- Сравнение с NULL через `=`
- Вложенные CASE без нужды (лучше COALESCE)

## Практика
1. Добавьте столбец «категория возраста» через CASE.
2. Замените NULL в city на «Не указан».
3. Посчитайте, сколько студентов из каждого «типа» города (столица / другой).

## Проверь себя
1. Чем COALESCE отличается от IFNULL?
2. Можно ли использовать CASE в ORDER BY?
3. Что вернёт NULLIF(5, 5)?

---
[← Урок 15](lesson-15.md) · [Программа курса](README.md) · [Урок 17 →](lesson-17.md)
