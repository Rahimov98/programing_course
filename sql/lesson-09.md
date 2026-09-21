# SQL · Урок 9. UPDATE и DELETE

## Цели урока
- Изменять существующие строки
- Удалять строки
- Делать это безопасно (с WHERE)

## Теория

**UPDATE**
```sql
UPDATE students
SET age = 22
WHERE name = 'Алишер';

UPDATE students
SET city = 'Душанбе', age = age + 1
WHERE city = 'Худжанд';
```

**DELETE**
```sql
DELETE FROM students WHERE age < 18;
DELETE FROM students WHERE id = 3;
```

**Без WHERE — опасно!**
```sql
UPDATE students SET age = 0;     -- изменит ВСЕ строки
DELETE FROM students;               -- удалит ВСЕ строки
```

**Проверка перед изменением**
```sql
-- сначала SELECT с тем же WHERE
SELECT * FROM students WHERE city = 'Худжанд';
-- потом UPDATE/DELETE
```

**Ограничение количества (SQLite / MySQL)**
```sql
DELETE FROM students WHERE city = 'Куляб' LIMIT 1;
```

## Типичные ошибки
- Забыли WHERE → обновили/удалили всё
- Опечатка в условии → затронуты не те строки
- Нет резервной копии перед массовым DELETE

## Практика
1. Увеличьте возраст всех студентов на 1.
2. Измените город одного конкретного студента.
3. Удалите студентов младше 19 лет (сначала проверьте SELECT).

## Проверь себя
1. Что будет, если выполнить UPDATE без WHERE?
2. Как безопасно проверить, что удалится?
3. Можно ли обновить несколько столбцов за раз?

---
[← Урок 8](lesson-08.md) · [Программа курса](README.md) · [Урок 10 →](lesson-10.md)
