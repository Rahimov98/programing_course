# SQL · Урок 24. Итоговый проект: база интернет-магазина

## Цель
Спроектировать и реализовать схему БД интернет-магазина, наполнить данными и написать полезные запросы.

## Требования к схеме
- Пользователи (покупатели)
- Категории товаров
- Товары (связь с категорией)
- Заказы
- Позиции заказа (товар + количество + цена на момент покупки)
- (Опционально) отзывы или адреса доставки

## Рекомендуемые таблицы

```sql
CREATE TABLE users (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    email TEXT NOT NULL UNIQUE,
    created_at TEXT DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE categories (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL UNIQUE
);

CREATE TABLE products (
    id INTEGER PRIMARY KEY,
    name TEXT NOT NULL,
    price REAL NOT NULL CHECK (price > 0),
    stock INTEGER NOT NULL DEFAULT 0 CHECK (stock >= 0),
    category_id INTEGER NOT NULL,
    FOREIGN KEY (category_id) REFERENCES categories(id)
);

CREATE TABLE orders (
    id INTEGER PRIMARY KEY,
    user_id INTEGER NOT NULL,
    status TEXT NOT NULL DEFAULT 'new',  -- new, paid, shipped, cancelled
    created_at TEXT DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (user_id) REFERENCES users(id)
);

CREATE TABLE order_items (
    order_id INTEGER NOT NULL,
    product_id INTEGER NOT NULL,
    quantity INTEGER NOT NULL CHECK (quantity > 0),
    price REAL NOT NULL,  -- цена на момент заказа
    PRIMARY KEY (order_id, product_id),
    FOREIGN KEY (order_id) REFERENCES orders(id),
    FOREIGN KEY (product_id) REFERENCES products(id)
);
```

## Задания

**1. Создание и наполнение**
- Создайте все таблицы с ограничениями.
- Добавьте 3–5 пользователей, 3 категории, 8–10 товаров, 4–6 заказов с позициями.

**2. Запросы**
1. Список товаров с названием категории.
2. Заказы пользователя (по email) с суммой каждого заказа.
3. Топ-5 самых продаваемых товаров (по количеству).
4. Пользователи, которые ничего не заказывали (LEFT JOIN).
5. Выручка по категориям.
6. Товары, которых осталось меньше 5 штук.

**3. Изменения**
- Оформите «оплату» заказа: смените status и уменьшите stock (в транзакции).
- Добавьте индекс на `orders(user_id)` и `order_items(product_id)`.

**4. Представление**
```sql
CREATE VIEW order_summary AS
SELECT o.id, u.name AS customer, o.status, o.created_at,
       SUM(oi.quantity * oi.price) AS total
FROM orders o
JOIN users u ON u.id = o.user_id
JOIN order_items oi ON oi.order_id = o.id
GROUP BY o.id;
```

## Критерии готовности
- [ ] Схема без явной избыточности (3НФ)
- [ ] Внешние ключи и CHECK
- [ ] Тестовые данные
- [ ] Минимум 6 рабочих SELECT/JOIN/агрегатов
- [ ] Хотя бы одна транзакция и один индекс
- [ ] VIEW order_summary

## Дополнительно
- Триггер: при INSERT в order_items уменьшать stock
- История статусов заказа
- Полнотекстовый поиск по названию товара (FTS в SQLite)

**Поздравляем!** Вы прошли курс SQL с нуля до проектирования рабочей базы.

---
[← Урок 23](lesson-23.md) · [Программа курса](README.md)
