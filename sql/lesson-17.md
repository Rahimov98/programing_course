# SQL · Урок 17. UNION

## Цели урока
- Объединять результаты нескольких SELECT
- Понимать UNION vs UNION ALL
- Согласовывать количество и типы столбцов

## Теория

**UNION** — объединение с удалением дубликатов
```sql
SELECT name, city FROM students
UNION
SELECT name, city FROM teachers;
```

**UNION ALL** — без удаления дубликатов (быстрее)
```sql
SELECT name FROM students
UNION ALL
SELECT name FROM teachers;
```

**Правила**
- Одинаковое количество столбцов
- Совместимые типы (слева направо)
- Имена столбцов берутся из первого SELECT
- ORDER BY только в конце

```sql
SELECT name AS person, 'student' AS role FROM students
UNION ALL
SELECT name, 'teacher' FROM teachers
ORDER BY person;
```

**Когда использовать**
- Отчёты из похожих таблиц
- Объединение архива и актуальных данных
- Разные источники с одной структурой

## Типичные ошибки
- Разное число столбцов
- ORDER BY внутри отдельных SELECT (не сработает как ожидается)
- UNION там, где нужен JOIN

## Практика
1. Объедините имена студентов и авторов книг в один список.
2. Добавьте столбец-метку (student / author).
3. Сделайте то же с UNION ALL и сравните результат.

## Проверь себя
1. Чем UNION отличается от UNION ALL?
2. Можно ли ORDER BY в середине?
3. Откуда берутся имена столбцов результата?

---
[← Урок 16](lesson-16.md) · [Программа курса](README.md) · [Урок 18 →](lesson-18.md)
