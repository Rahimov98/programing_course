# PHP · Урок 19. CRUD-операции

## Цели урока
- Создавать, читать, обновлять и удалять записи через PDO
- Использовать подготовленные запросы
- Понять основы SQL-инъекций и защиты от них

## Теория

**CREATE (INSERT)**
```php
$stmt = $pdo->prepare("INSERT INTO users (name, email) VALUES (?, ?)");
$stmt->execute(["Мадина", "madina@example.com"]);
$id = $pdo->lastInsertId();
```

Или именованные параметры:
```php
$stmt = $pdo->prepare("INSERT INTO users (name, email) VALUES (:name, :email)");
$stmt->execute(["name" => "Мадина", "email" => "madina@example.com"]);
```

**READ (SELECT)**
```php
$stmt = $pdo->prepare("SELECT * FROM users WHERE id = ?");
$stmt->execute([$id]);
$user = $stmt->fetch();

// все
$stmt = $pdo->query("SELECT * FROM users ORDER BY id DESC");
$users = $stmt->fetchAll();
```

**UPDATE**
```php
$stmt = $pdo->prepare("UPDATE users SET name = ?, email = ? WHERE id = ?");
$stmt->execute([$name, $email, $id]);
```

**DELETE**
```php
$stmt = $pdo->prepare("DELETE FROM users WHERE id = ?");
$stmt->execute([$id]);
```

**Почему prepare?**
```php
// ПЛОХО — SQL-инъекция
$id = $_GET["id"];
$pdo->query("SELECT * FROM users WHERE id = $id");

// ХОРОШО
$stmt = $pdo->prepare("SELECT * FROM users WHERE id = ?");
$stmt->execute([$id]);
```

## Типичные ошибки
- Конкатенация пользовательских данных в SQL
- Забыли `execute()`
- `fetch()` после `fetchAll()` — курсор уже в конце

## Практика
1. Скрипт добавления пользователя из формы.
2. Страница списка всех пользователей.
3. Форма редактирования и кнопка удаления по `id`.

## Проверь себя
1. Что такое CRUD?
2. Зачем подготовленные запросы?
3. Как получить id только что вставленной записи?

---
[← Урок 18](lesson-18.md) · [Программа курса](README.md) · [Урок 20 →](lesson-20.md)
