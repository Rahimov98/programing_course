# SQL · Урок 21. Хранимые процедуры и триггеры

## Цели урока
- Понять идею хранимых процедур и функций
- Создавать простые триггеры
- Знать ограничения SQLite vs MySQL/PostgreSQL

## Теория

**Хранимые процедуры** (MySQL / PostgreSQL)
Логика на стороне БД. В чистом SQLite процедур нет (есть расширения).

Пример MySQL:
```sql
DELIMITER //
CREATE PROCEDURE add_student(IN p_name TEXT, IN p_age INT)
BEGIN
    INSERT INTO students (name, age) VALUES (p_name, p_age);
END //
DELIMITER ;

CALL add_student('Алишер', 21);
```

**Триггеры** — автоматические действия при INSERT/UPDATE/DELETE.

**SQLite**
```sql
CREATE TRIGGER trg_books_log
AFTER INSERT ON books
BEGIN
    INSERT INTO audit_log (action, book_id, created_at)
    VALUES ('insert', NEW.id, datetime('now'));
END;
```

**NEW и OLD**
- `NEW` — новое значение (INSERT/UPDATE)
- `OLD` — старое значение (UPDATE/DELETE)

**Пример: запрет отрицательного остатка**
```sql
CREATE TRIGGER trg_stock_check
BEFORE UPDATE ON products
WHEN NEW.stock < 0
BEGIN
    SELECT RAISE(ABORT, 'Остаток не может быть отрицательным');
END;
```

**Удаление**
```sql
DROP TRIGGER trg_books_log;
```

## Типичные ошибки
- Триггер вызывает сам себя (рекурсия)
- Сложная бизнес-логика только в триггерах (трудно отлаживать)
- Забыли, что в SQLite ограниченный набор возможностей

## Практика
1. Создайте таблицу audit_log и триггер на INSERT в books.
2. Добавьте книгу и проверьте запись в логе.
3. (Опционально) Триггер, запрещающий удаление авторов с книгами.

## Проверь себя
1. Когда срабатывает триггер?
2. Чем NEW отличается от OLD?
3. Есть ли хранимые процедуры в обычном SQLite?

---
[← Урок 20](lesson-20.md) · [Программа курса](README.md) · [Урок 22 →](lesson-22.md)
