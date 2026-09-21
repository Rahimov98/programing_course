# PHP · Урок 18. MySQL и PDO: подключение

## Цели урока
- Подключиться к MySQL через PDO
- Выполнять простые запросы
- Обрабатывать ошибки подключения

## Теория

**PDO** — единый интерфейс для разных СУБД. Предпочтительнее устаревшего `mysqli` для новых проектов.

**Подключение**
```php
<?php
$host = "localhost";
$db   = "mydb";
$user = "root";
$pass = "";
$charset = "utf8mb4";

$dsn = "mysql:host=$host;dbname=$db;charset=$charset";
$options = [
    PDO::ATTR_ERRMODE            => PDO::ERRMODE_EXCEPTION,
    PDO::ATTR_DEFAULT_FETCH_MODE => PDO::FETCH_ASSOC,
    PDO::ATTR_EMULATE_PREPARES   => false,
];

try {
    $pdo = new PDO($dsn, $user, $pass, $options);
} catch (PDOException $e) {
    die("Ошибка подключения: " . $e->getMessage());
}
```

**Простой запрос**
```php
$stmt = $pdo->query("SELECT id, name FROM users LIMIT 10");
while ($row = $stmt->fetch()) {
    echo $row["id"] . ": " . $row["name"] . "\n";
}

// или все сразу
$users = $pdo->query("SELECT * FROM users")->fetchAll();
```

**Создание таблицы (для тестов)**
```sql
CREATE TABLE users (
    id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

**Вынос в config**
```php
// config/database.php
return [
    "host" => "localhost",
    "dbname" => "mydb",
    "user" => "root",
    "pass" => "",
];
```

## Типичные ошибки
- Неверный пароль / имя БД
- Забыли создать базу
- `ATTR_ERRMODE` не включён — ошибки «проглатываются»
- Подключение в каждом скрипте заново (лучше один раз)

## Практика
1. Создайте БД и таблицу `users` в phpMyAdmin или консоли.
2. Напишите скрипт подключения и выведите «Connected».
3. Выполните `SELECT` и выведите список пользователей (или пустой результат).

## Проверь себя
1. Что такое DSN?
2. Зачем `PDO::ERRMODE_EXCEPTION`?
3. Чем PDO лучше `mysql_*` функций?

---
[← Урок 17](lesson-17.md) · [Программа курса](README.md) · [Урок 19 →](lesson-19.md)
