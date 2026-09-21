# SQL · Урок 8. GROUP BY и HAVING

## Цели урока
- Группировать данные
- Фильтровать группы через HAVING
- Сочетать агрегаты с группировкой

## Теория

**GROUP BY**
```sql
SELECT city, COUNT(*) AS cnt
FROM students
GROUP BY city;
```

**Несколько столбцов**
```sql
SELECT city, age, COUNT(*) 
FROM students
GROUP BY city, age;
```

**HAVING — фильтр после группировки**
```sql
SELECT city, COUNT(*) AS cnt
FROM students
GROUP BY city
HAVING COUNT(*) >= 2;
```

**WHERE vs HAVING**
- `WHERE` — фильтрует строки **до** группировки
- `HAVING` — фильтрует группы **после**

```sql
SELECT city, AVG(age) AS avg_age
FROM students
WHERE age >= 18          -- сначала отсекаем
GROUP BY city
HAVING AVG(age) > 20;    -- потом фильтруем группы
```

**Порядок выполнения**
FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT

## Типичные ошибки
- В SELECT столбцы, которых нет в GROUP BY и не агрегаты
- `WHERE COUNT(*) > 1` вместо `HAVING`
- Группировка по алиасу (в некоторых СУБД нельзя)

## Практика
1. Посчитайте студентов в каждом городе.
2. Покажите города, где больше 1 студента.
3. Средний возраст по городам, только где avg > 20.

## Проверь себя
1. Чем WHERE отличается от HAVING?
2. Можно ли в SELECT писать столбец не из GROUP BY?
3. В каком порядке выполняются WHERE и HAVING?

---
[← Урок 7](lesson-07.md) · [Программа курса](README.md) · [Урок 9 →](lesson-09.md)
