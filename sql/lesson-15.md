# SQL · Урок 15. Строковые функции и функции даты

## Цели урока
- Работать со строками: длина, регистр, поиск, замена
- Работать с датами: извлечение частей, разница
- Форматировать вывод

## Теория

**Строки (SQLite / общие)**
```sql
SELECT UPPER(name), LOWER(name) FROM students;
SELECT LENGTH(name) FROM students;           -- байты/символы зависит от СУБД
SELECT SUBSTR(name, 1, 3) FROM students;     -- с 1-го, 3 символа
SELECT REPLACE(city, 'Душанбе', 'Dushanbe') FROM students;
SELECT TRIM('  hello  ');                    -- убрать пробелы
SELECT name || ' - ' || city FROM students;  -- конкатенация (SQLite)
```

**LIKE уже знаем; дополнительно**
```sql
SELECT * FROM students WHERE name GLOB 'А*';  -- SQLite: регистрозависимо
```

**Даты**
```sql
-- SQLite
SELECT date('now');
SELECT datetime('now', '+3 hours');
SELECT strftime('%Y-%m-%d', 'now');
SELECT strftime('%Y', created_at) AS year FROM orders;

-- разница
SELECT julianday('now') - julianday(created_at) AS days FROM orders;
```

**MySQL примеры**
```sql
SELECT CONCAT(name, ' ', city);
SELECT YEAR(created_at), MONTH(created_at);
SELECT DATE_ADD(created_at, INTERVAL 7 DAY);
SELECT DATEDIFF(NOW(), created_at);
```

## Типичные ошибки
- Путаница функций разных СУБД
- `LENGTH` vs `CHAR_LENGTH` для Unicode
- Сравнение дат как строк без единого формата

## Практика
1. Выведите имена студентов заглавными буквами.
2. Покажите первые 5 символов названия книги.
3. Выведите текущую дату и год из столбца с датой.

## Проверь себя
1. Как объединить две строки в SQLite?
2. Чем SUBSTR отличается от LEFT/RIGHT (в других СУБД)?
3. Как получить только год из даты?

---
[← Урок 14](lesson-14.md) · [Программа курса](README.md) · [Урок 16 →](lesson-16.md)
